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

