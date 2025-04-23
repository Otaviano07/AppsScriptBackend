# API para Gerenciamento de Clientes e Pedidos com Google Apps Script e Front-end HTML

Este projeto consiste em uma API desenvolvida utilizando o Google Apps Script para interagir com planilhas do Google Sheets, permitindo o gerenciamento de informações de clientes e pedidos. Adicionalmente, são fornecidos formulários HTML básicos para testar e interagir com essa API.

## Visão Geral

A API oferece funcionalidades para:

* **Clientes:** Criar, ler, atualizar e excluir informações de clientes.
* **Pedidos:** Criar, ler, atualizar e excluir informações de pedidos, associados a clientes.

Os dados são armazenados em duas abas específicas de uma planilha do Google Sheets (`Clientes` e `Pedidos`). A comunicação entre os formulários HTML e a API é realizada através de requisições HTTP `POST` com dados no formato JSON.

## Arquivos do Projeto

* **`Código.gs` (Google Apps Script):** Contém toda a lógica da API, incluindo:
    * Funções para manipular dados nas planilhas (`createCliente`, `readClientes`, `updateCliente`, `deleteCliente`, `createPedido`, `readPedidos`, `updatePedido`, `deletePedido`).
    * Funções auxiliares para acesso à planilha, tratamento de erros e formatação de dados.
    * Endpoints `doGet(e)` e `doPost(e)` para receber requisições HTTP.
    * Configuração para lidar com CORS (Cross-Origin Resource Sharing) para permitir requisições de diferentes origens (útil para testes locais).
* **`formulario_cliente.html`:** Um formulário HTML básico para criar novos clientes e enviar os dados para a API.
* **`formulario_pedido.html`:** Um formulário HTML básico para criar novos pedidos e enviar os dados para a API.

## Configuração

1.  **Google Sheets:**
    * Crie uma nova planilha no Google Sheets.
    * Renomeie a primeira aba para `Clientes`.
    * Crie uma segunda aba e renomeie para `Pedidos`.
    * Adicione os seguintes cabeçalhos na **primeira linha** da aba `Clientes`, exatamente nesta ordem:
        ```
        id,cadastro,tipo,categoria,nome,apelido,estado,cidade,cep,endereco,numero,bairro,celular,referencia,observacao,status
        ```
    * Adicione os seguintes cabeçalhos na **primeira linha** da aba `Pedidos`, exatamente nesta ordem:
        ```
        id,cadastro,data,entrega,idCliente,codigo,descricao,quantidade,preco,total,troco,solicitante,entregador,forma,pagamento,observacao,status
        ```
    * **Importante:** Anote o **ID da sua planilha**. Você pode encontrá-lo na URL da planilha (é a longa sequência de caracteres entre `/d/` e `/edit`).
2.  **Google Apps Script:**
    * Abra a planilha que você criou.
    * Vá em "Extensões" > "Apps Script".
    * Cole o conteúdo do arquivo `Código.gs` no editor de script, **substituindo** o código existente.
    * Na primeira linha do script, atualize a constante `SPREADSHEET_ID` com o ID da sua planilha:
        ```javascript
        const SPREADSHEET_ID = "SUA_SPREADSHEET_ID";
        ```
    * Salve o projeto (ex: `API_Pedidos`).
3.  **Implantação como "Web app":**
    * No editor de script, vá em "Implantar" > "Nova implantação".
    * Em "Selecionar tipo", escolha "Aplicativo da Web".
    * Em "Descrição", adicione uma descrição (opcional).
    * Em "Quem tem acesso", selecione "Qualquer pessoa" (para testes) ou "Qualquer pessoa com o link". **Tenha cuidado com essa configuração em ambientes de produção.**
    * Clique em "Implantar".
    * Autorize o script a acessar sua planilha, seguindo as instruções.
    * Copie o **"URL da web"** fornecido após a implantação bem-sucedida. Você precisará dessa URL nos arquivos HTML.
4.  **Configuração dos Formulários HTML:**
    * Abra os arquivos `formulario_cliente.html` e `formulario_pedido.html` em um editor de texto (como o VS Code).
    * Em cada arquivo, localize a seguinte linha de código JavaScript:
        ```javascript
        fetch('SUA_URL_DA_WEB_APP', {
        ```
    * **Substitua `'SUA_URL_DA_WEB_APP'` pela URL da web que você copiou na etapa 3.**
    * Salve as alterações nos arquivos HTML.

## Como Testar

1.  Abra os arquivos `formulario_cliente.html` e `formulario_pedido.html` no seu navegador web (você pode fazer isso clicando com o botão direito no arquivo no VS Code e escolhendo "Open with Live Server" ou simplesmente abrindo o arquivo diretamente).
2.  Preencha os campos dos formulários e clique no botão "Enviar".
3.  Verifique a seção abaixo do botão para ver a resposta da API (geralmente um objeto JSON indicando sucesso e o ID do item criado).
4.  Abra sua planilha do Google Sheets e verifique se os dados foram adicionados nas abas `Clientes` e `Pedidos`.

## Próximos Passos e Melhorias

* Implementar formulários para atualizar e excluir registros existentes.
* Adicionar validação de dados no lado do cliente (nos formulários HTML).
* Melhorar a interface do usuário (UI) e a experiência do usuário (UX) dos formulários com CSS mais avançado.
* Implementar mecanismos de autenticação e autorização na API para maior segurança.
* Adicionar tratamento de erros mais robusto na API.
* Considerar a criação de uma interface de administração mais completa utilizando um framework front-end.
* Documentar a API de forma mais detalhada.

## Notas

* Este é um projeto básico para demonstração e testes. Para ambientes de produção, medidas de segurança adicionais e um tratamento de erros mais completo são altamente recomendados.
* A permissão de acesso "Qualquer pessoa" na implantação da "Web app" torna a API publicamente acessível. Considere restringir o acesso conforme a necessidade.
* Para testes locais com formulários HTML (como ao usar o Live Server do VS Code), a configuração de CORS no Google Apps Script é essencial para evitar erros de bloqueio de requisições cross-origin.

Sinta-se à vontade para contribuir e expandir este projeto!
