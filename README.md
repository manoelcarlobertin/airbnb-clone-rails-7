# 🚀 Projeto Fullstack Ruby on Rails: Clone do Airbnb

Este projeto é um guia completo para desenvolver uma aplicação Fullstack similar ao Airbnb, utilizando as mais recentes ferramentas e práticas do ecossistema Ruby on Rails. Acompanhe o desenvolvimento desde a configuração inicial até funcionalidades avançadas como autenticação, sistema de reservas e pagamentos.

\<p align="center"\>
\<img src="[https://via.placeholder.com/800x400?text=Screenshot+da+p%C3%A1gina+inicial+do+projeto](https://www.google.com/search?q=https://via.placeholder.com/800x400%3Ftext%3DScreenshot%2Bda%2Bp%25C3%25A1gina%2Binicial%2Bdo%2Bprojeto)" alt="Página inicial do projeto Rails"\>
<br>
\<em\>(Substitua esta imagem por uma captura de tela da página inicial do seu projeto)\</em\>
\</p\>

## ✨ Visão Geral do Projeto

O objetivo é replicar as funcionalidades essenciais de uma plataforma de aluguel de imóveis, como:

  * **Listagem de Imóveis:** Criar, visualizar e gerenciar anúncios de propriedades.
  * **Autenticação de Usuários:** Cadastro, login e gerenciamento de perfis.
  * **Sistema de Reservas:** Permite que usuários reservem imóveis.
  * **Processamento de Pagamentos:** Integração com Stripe para transações seguras.

Este projeto é baseado e se inspira no tutorial em vídeo:
**"Learn Ruby on Rails in 2025 by Building Airbnb Full Tutorial"**
[Assista ao tutorial no YouTube](https://www.youtube.com/watch?v=dshxbdKzMwU)

-----

## 🛠️ Tecnologias Utilizadas

  * **Ruby on Rails 7+**
  * **RSpec:** Para testes de unidade, integração e sistema.
  * **FactoryBot:** Para a criação de objetos de teste.
  * **Faker:** Para a geração de dados de teste realistas.
  * **Friendly ID:** Para URLs amigáveis.
  * **Active Storage:** Para upload e gerenciamento de imagens.
  * **Devise:** Para autenticação de usuários.
  * **Stripe Connect & Checkout:** Para processamento de pagamentos.
  * **Stimulus:** Para interatividade no frontend.

-----

## 🚦 Como Rodar o Projeto Localmente

Siga estas etapas para configurar e executar o projeto em sua máquina:

1.  **Clone o repositório:**

    ```bash
    git clone [URL_DO_SEU_REPOSITORIO]
    cd [nome-do-seu-repositorio]
    ```

2.  **Instale as dependências:**

    ```bash
    bundle install
    ```

3.  **Configure o banco de dados:**

    ```bash
    rails db:create
    rails db:migrate
    ```

4.  **Popule o banco de dados com dados de exemplo (Seed):**

    ```bash
    rake db:seed
    ```

    Isso preencherá seu banco de dados com usuários, anúncios e imagens (se houver imagens em `app/assets/images`), permitindo que você teste as funcionalidades imediatamente.

5.  **Inicie o servidor Rails:**

    ```bash
    rails s
    ```

    O aplicativo estará disponível em `http://localhost:3000`.

-----

## 🗺️ Mapa de Desenvolvimento (Etapas do Tutorial)

O projeto foi estruturado seguindo as seguintes etapas principais:

1.  **Configuração Inicial e Geração do Projeto**
2.  **Geração do Modelo de Listagem (Scaffold):** Criação dos Anúncios de aluguel de imóvel.
3.  **Configurações Básicas e Melhorias de UI/UX**
4.  **URLs Amigáveis (Friendly ID):** Implementação de URLs legíveis baseadas no título.
5.  **Página de Detalhes da Listagem:** Visualização completa de um anúncio.
6.  **Adição de Campos Detalhados:** Enriquecimento das informações de cada listagem.
7.  **Upload de Imagens Melhorado:** Utilizando Active Storage e Stimulus para upload de fotos.
    \<p align="center"\>
    \<img src="[https://via.placeholder.com/600x300?text=Exemplo+de+upload+de+imagens](https://www.google.com/search?q=https://via.placeholder.com/600x300%3Ftext%3DExemplo%2Bde%2Bupload%2Bde%2Bimagens)" alt="Upload de imagens com Active Storage"\>
    <br>
    \<em\>(Substitua por uma imagem do formulário de upload de imagens)\</em\>
    \</p\>
8.  **Autenticação de Usuários com Devise**
9.  **Barra de Navegação (Navbar) e Dropdown de Usuário:** Elementos essenciais de navegação.
10. **Gerenciamento de Perfil do Usuário**
11. **Integração com Stripe Connect (para Proprietários):** Configuração para pagamentos a proprietários.
12. **Associação de Usuário a Listagens e Autorização:** Definindo quem pode criar/editar anúncios.
13. **Adição de Preços às Listagens**
14. **Sistema de Reservas (Bookings):** Lógica para criar e gerenciar reservas.
15. **Pagamento de Reservas com Stripe Checkout Embedded**
16. **Gerenciamento de Status de Reserva e Validações**

-----

## 🧩 Melhorias na Modularidade e Manutenibilidade

Para garantir um código limpo, testável e fácil de manter, foram aplicadas as seguintes estratégias de modularização:

  * **Service Objects:**
    Para lógicas de negócio complexas, como a criação de uma reserva (que envolve validações, criação de booking, interação com Stripe), Service Objects centralizam a lógica e mantêm os controllers mais enxutos.

      * **Exemplo:** `BookingCreatorService`.

  * **Form Objects:**
    Para formulários com muitos campos ou que interagem com múltiplos modelos (ex: cadastro de usuário com informações de perfil), Form Objects encapsulam a lógica de validação e salvamento, tornando o controller mais limpo.

  * **View Components:**
    Em vez de `partials` complexos, foram utilizados View Components (inspirados no ViewComponent do GitHub). Eles oferecem uma forma mais robusta e testável de encapsular a interface do usuário com sua própria lógica.

    \<p align="center"\>
    \<img src="[https://via.placeholder.com/600x300?text=Exemplo+de+View+Component](https://www.google.com/search?q=https://via.placeholder.com/600x300%3Ftext%3DExemplo%2Bde%2BView%2BComponent)" alt="Estrutura de View Component"\>
    <br>
    \<em\>(Substitua por um diagrama ou exemplo de View Component)\</em\>
    \</p\>

-----

## 🧪 Testes

O projeto utiliza **RSpec**, **FactoryBot** e **Faker** para garantir a qualidade do código através de uma suíte de testes robusta:

  * **Testes de Unidade:** Para validações e associações de modelos.
  * **Testes de Requisição/Controlador:** Para verificar o comportamento das requisições HTTP, redirecionamentos e respostas.
  * **Testes de Sistema/Feature:** Simulando a interação completa do usuário na interface para validar fluxos completos.

Para executar a suíte de testes:

```bash
bundle exec rspec
```

\<p align="center"\>
\<img src="[https://via.placeholder.com/600x300?text=Resultados+dos+testes+RSpec](https://www.google.com/search?q=https://via.placeholder.com/600x300%3Ftext%3DResultados%2Bdos%2Btestes%2BRSpec)" alt="Resultados dos testes RSpec no terminal"\>
<br>
\<em\>(Substitua por uma imagem do output dos testes RSpec no terminal)\</em\>
\</p\>

-----

## 🌱 `db/seeds.rb` - Exemplo de População de Dados

Este é o script `db/seeds.rb` que é executado com `rake db:seed` para popular o banco de dados com dados de teste, incluindo usuários, anúncios e anexos de imagem.

```ruby
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
  puts "    -> Certifique-se de colocar arquivos .jpg ou .png em app/assets/images."
else
  puts "✅  #{local_image_paths.count} imagens encontradas."
end

# --- MÉTODO AUXILIAR PARA ANEXAR IMAGENS LOCAIS ---
def attach_local_images(anuncio, image_paths)
  return if image_paths.empty?
  quantity = [ rand(2..5), image_paths.count ].min
  images_to_attach = image_paths.sample(quantity)
  puts "     -> Anexando #{quantity} imagens locais para '#{anuncio.title}'..."
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
```
