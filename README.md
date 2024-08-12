App - Reserva de Hotéis

Descrição: Este projeto é uma aplicação desenvolvida com Nuxt 3, Vue 3, TypeScript, Pinia, e Tailwind CSS para  simular um sistema de reserva de hotéis. O foco é proporcionar uma interface funcional que permita ao usuário pesquisar, comparar e reservar hotéis de forma intuitiva e eficiente.

Funcionalidades:
    - Pesquisa de Hotéis (por destino)   ✅

    - Interface para inserir critérios de pesquisa (destino, datas de check-in e check-out, número de quartos e  hóspedes).✅
    Resultados exibidos em uma lista, com opções de ordenação por preço, avaliações e nome.✅
    Comparação de opções de hotéis✅

    - Seleção de múltiplos hotéis para comparação lado a lado das características.
    - Reserva de Quartos (mock data) ✅

    - Formulário para reservar um quarto, solicitando informações do usuário e detalhes de pagamento.✅

    - Notificações para informar o usuário sobre o status de sua reserva. (Toast) ✅
    
    
Tecnologias Utilizadas:
    - Nuxt 3: Framework para desenvolvimento da aplicação.(SSR)
    - Vue 3 Composition API: Utilizado para construção dos componentes.
    - TypeScript: Tipagem estática para maior robustez do código.
    - Pinia: Gerenciamento de estado e autenticação do usuário.
    - Tailwind CSS: Estilização das páginas.
    - Nuxt Layers: Organização modular da aplicação.
    - API Mockada via SSR: Simulação de chamadas de API para busca e reserva de hotéis.
    - GitHub Actions: Pipeline CI/CD para automação de build e deploy.


    OBS: Neste projeto foi implementado auth (login) sem critérios para email e senha, ou seja, qualquer email e senha será autenticado, porém,
    existe validação para o formato de email e carateres da senha.

    OBS: Para verificação de autenticação use a rota localhost:3000/dummylogin.




    Executar o projeto:

    1- Clone o repositório, usando a branch "main";
    2- Instalar as dependências: "npm install --legacy-peer-deps"
    3- Executar o projeto: "npm run dev"
    4 -Executar testes: "npx vitest"
