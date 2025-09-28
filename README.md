Primeiramente seleciona CODE para visualizar melhor essas instruções a seguir.

Tente rodar no terminal a linha de comando: rake db:seed 

(Isso servirá para popular com alguns dados o banco, com a finalidade de testar e ajustar as funcionalidades desse sistema web).

Fullstack Ruby on Rails: Guia Completo para Desenvolvimento de uma Aplicação Airbnb

O vídeo "Learn Ruby on Rails in 2025 by Building Airbnb Full Tutorial" (Aprenda Ruby on Rails em 2025 construindo um tutorial completo do Airbnb)

https://www.youtube.com/watch?v=dshxbdKzMwU

1 Configuração Inicial e Geração do Projeto
2 Geração do Modelo de Listagem (Scaffold) - Anúnios de aluguel de imóvel
3 Configurações Básicas e UI/UX 
4 URLs Amigáveis (Friendly ID)
5 Página de Detalhes da Listagem
6 Adição de Campos Detalhados para Listagem
7 Upload de Imagens Melhorado com Active Storage e Stimulus
8 Autenticação de Usuários com Devise
9 Barra de Navegação (Navbar) e Dropdown de Usuário
10 Gerenciamento de Perfil do Usuário
11 Integração com Stripe Connect (para Proprietários)
12 Associação de Usuário a Listagens e Autorização
13 Adição de Preços às Listagens
14 Sistema de Reservas (Bookings)
15 Pagamento de Reservas com Stripe Checkout Embedded
16 Gerenciamento de Status de Reserva e Validações
17 Melhorias na Modularidade e Manutenibilidade:

Service Objects: Para lógicas de negócio complexas, como a criação de uma reserva (que envolve validações, criação de booking, interação com Stripe), utilize Service Objects. Isso centraliza a lógica e mantém os controllers mais enxutos. Ex: BookingCreatorService.

Form Objects: Para formulários com muitos campos ou que interagem com múltiplos modelos (ex: cadastro de usuário com informações de perfil), crie Form Objects. Eles encapsulam a lógica de validação e salvamento, tornando o controller mais limpo.

View Components: Em vez de partials complexos, considere a utilização de View Components (como o ViewComponent da GitHub). Eles oferecem uma forma mais robusta e testável de encapsular UI com sua própria lógica e testes.

Modelo do arquivo que irá popular todo o sistema, segue um exemplo abaixo:

# db/seeds.rb (Versão Final Corrigida)

# --- CONFIGURAÇÃO INICIAL ---
require 'open-uri'
Faker::Config.locale = 'pt-BR'

# --- PASSO 1: CARREGAR OS CAMINHOS DAS IMAGENS LOCAIS ---
puts "============================================="
puts "🖼️  Procurando por imagens locais em app/assets/images..."
local_image_paths = Dir.glob(Rails.root.join('app', 'assets', 'images', '*.{jpg,jpeg,png}'))

if local_image_paths.empty?
  puts "⚠️  Nenhuma imagem local encontrada! Os anúncios serão criados sem fotos."
  puts "   -> Certifique-se de colocar arquivos .jpg ou .png em app/assets/images."
else
  puts "✅  #{local_image_paths.count} imagens encontradas."
end

# --- MÉTODO AUXILIAR PARA ANEXAR IMAGENS LOCAIS ---
def attach_local_images(anuncio, image_paths)
  return if image_paths.empty?
  quantity = [ rand(2..5), image_paths.count ].min
  images_to_attach = image_paths.sample(quantity)
  puts "    -> Anexando #{quantity} imagens locais para '#{anuncio.title}'..."
  images_to_attach.each do |image_path|
    anuncio.images.attach(
      io: File.open(image_path),
      filename: File.basename(image_path)
    )
  end
end

# --- INÍCIO DO PROCESSO DE SEED ---
puts "\n============================================="
puts "🚀 Iniciando o processo de seed..."

# --- PASSO 2: LIMPEZA DO BANCO DE DADOS ---
puts "\n🧹 Limpando o banco de dados..."
# Booking.destroy_all
Anuncio.destroy_all
User.destroy_all
ActiveStorage::Attachment.all.each { |attachment| attachment.purge }
puts "✅ Banco de dados limpo!"

# --- PASSO 3: CRIAÇÃO DE USUÁRIOS ---
puts "\n👤 Criando usuários..."
main_owner = FactoryBot.create(:user,
  # first_name: 'Ana',
  # last_name: 'Proprietária',
  email: 'dono@email.com',
  password: '123456',
  password_confirmation: '123456'
  # stripe_status: User::STRIPE_STATUS[:complete] # Usando a constante
)
# guest_users = FactoryBot.create_list(:user, 5)
puts " -> Usuário proprietário criado: #{main_owner.email}"
# puts " -> #{guest_users.count} usuários hóspedes criados."

# --- PASSO 4: CRIAÇÃO DE LISTAGENS (ANÚNCIOS) ---
puts "\n🏡 Criando Anúncios..."
12.times do
  anuncio = FactoryBot.create(:anuncio, user: main_owner)
  puts "  -> Listagem com Anúncios foi criada: '#{anuncio.title}' por #{anuncio.user.email}"
  attach_local_images(anuncio, local_image_paths)
end
puts "✅ #{Anuncio.count} listagens com os Anúncios foram todas criadas!"


# --- PASSO 5: CRIAÇÃO DE RESERVAS VÁLIDAS ---
# puts "\n Criando reservas válidas..."
# available_listings = Listing.all
# guest_users.each do |guest|
#   rand(1..3).times do
#     listing_to_book = available_listings.sample
#     10.times do
#       checkin = Faker::Date.between(from: Date.today + 1, to: Date.today + 60.days)
#       checkout = checkin + rand(2..7).days

      # --- ESTA É A LINHA QUE FOI CORRIGIDA ---
      # Antes: .confirmed
      # Agora: .where(status: Booking::STATUS[:confirmed])
      # is_overlapping = listing_to_book.bookings.where(status: Booking::STATUS[:confirmed]).where(
      #   "(checkin_date, checkout_date) OVERLAPS (?, ?)", checkin, checkout
      # ).exists?

#       unless is_overlapping
#         status_key = [:confirmed, :pending].sample
#         booking = FactoryBot.create(:booking,
#           listing: listing_to_book,
#           user: guest,
#           checkin_date: checkin,
#           checkout_date: checkout,
#           status: Booking::STATUS[status_key]
#         )
#         puts "  -> Reserva #{status_key.to_s.upcase} criada para '#{listing_to_book.title}' por #{guest.first_name}"
#         break
#       end
#     end
#   end
# end
# puts " #{Booking.count} reservas criadas."

# --- FINALIZAÇÃO ---
puts "\n============================================="
puts "🎉 Processo de seed finalizado com sucesso!"
puts "============================================="
# ... (resumo final)
