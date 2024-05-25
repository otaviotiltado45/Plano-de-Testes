# Plano de Testes SupplySpeed

## Introdução
Este plano de testes foi criado para guiar outro grupo na validação das funcionalidades da API fornecida. A API oferece funcionalidades para o gerenciamento de usuários, pedidos e produtos. A seguir, detalharemos os casos de teste para cada rota, incluindo os dados necessários, as condições esperadas e as verificações a serem realizadas.

## Visão Geral
A API é desenvolvida utilizando Express e inclui rotas para:
- Cadastro de usuários
- Autenticação
- Gerenciamento de pedidos
- Gerenciamento de produtos

## Configuração do Ambiente
1. Clonar o repositório do projeto.
2. Instalar as dependências necessárias com `npm install`.
3. Configurar as variáveis de ambiente, se necessário.
4. Iniciar o servidor com `npm start`.

## Rotas de Usuário

### POST /users/signup
**Descrição:** Cadastra um novo usuário.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Todos os campos preenchidos corretamente.
   - **Verificação:** Receber status 200 OK e um token de autenticação.
   - **Exemplo de Request:**
     ```json
     {
       "nome": "Teste",
       "email": "teste@example.com",
       "senha": "senha123",
       "tipoUsuario": "cliente",
       "cnpj_cpf": "12345678900",
       "descricao": "Usuário de teste",
       "telefoneCelular": "999999999",
       "estado": "SP",
       "cidade": "São Paulo",
       "bairro": "Centro",
       "rua": "Rua A",
       "numero": "100",
       "cep": "01001000"
     }
     ```
2. **Erro - Campos Obrigatórios Faltando**
   - **Input:** Faltando um ou mais campos obrigatórios.
   - **Verificação:** Receber status 400 Bad Request.
   - **Exemplo de Request:** 
     ```json
     {
       "email": "teste@example.com",
       "senha": "senha123"
     }
     ```

### POST /users/login
**Descrição:** Realiza login de um usuário.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Email e senha corretos.
   - **Verificação:** Receber status 200 OK e um token de autenticação.
   - **Exemplo de Request:**
     ```json
     {
       "email": "teste@example.com",
       "senha": "senha123"
     }
     ```
2. **Erro - Email ou Senha Incorretos**
   - **Input:** Email ou senha incorretos.
   - **Verificação:** Receber status 400 Bad Request.
   - **Exemplo de Request:**
     ```json
     {
       "email": "teste@example.com",
       "senha": "senhaerrada"
     }
     ```

### GET /users/searchInformation/:numPage
**Descrição:** Busca informações de usuários, paginada.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e número de página válido.
   - **Verificação:** Receber status 200 OK e a lista de usuários.
2. **Erro - Número de Página Inválido**
   - **Input:** Token de autenticação válido e número de página inválido.
   - **Verificação:** Receber status 400 Bad Request.
3. **Erro - Sem Token de Autenticação**
   - **Input:** Sem token de autenticação.
   - **Verificação:** Receber status 401 Unauthorized.

### GET /users/getProfileInformation/:idProfile
**Descrição:** Obtém informações do perfil de um usuário específico.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do perfil válido.
   - **Verificação:** Receber status 200 OK e as informações do perfil.
2. **Erro - Usuário Não Encontrado**
   - **Input:** Token de autenticação válido e ID do perfil inválido.
   - **Verificação:** Receber status 400 Bad Request.

## Rotas de Pedidos

### GET /requests/searchOrders
**Descrição:** Busca todos os pedidos do usuário autenticado.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido.
   - **Verificação:** Receber status 200 OK e a lista de pedidos.
2. **Erro - Sem Token de Autenticação**
   - **Input:** Sem token de autenticação.
   - **Verificação:** Receber status 401 Unauthorized.

### POST /requests/sendRequest
**Descrição:** Envia um novo pedido.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e todos os campos preenchidos corretamente.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
   - **Exemplo de Request:**
     ```json
     {
       "idDistribuidora": "123",
       "dataEntrega": "2023-05-30",
       "idEndereco": "456",
       "arrayProdutos": [
         ["789", 2]
       ]
     }
     ```
2. **Erro - Dados Inválidos**
   - **Input:** Token de autenticação válido e campos obrigatórios faltando.
   - **Verificação:** Receber status 400 Bad Request.

### PUT /requests/acceptRequest/:idPedido
**Descrição:** Aceita um pedido.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do pedido válido.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
2. **Erro - Pedido Não Encontrado**
   - **Input:** Token de autenticação válido e ID do pedido inválido.
   - **Verificação:** Receber status 400 Bad Request.

### PUT /requests/rejectRequest/:idPedido
**Descrição:** Rejeita um pedido.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do pedido válido.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
2. **Erro - Pedido Não Encontrado**
   - **Input:** Token de autenticação válido e ID do pedido inválido.
   - **Verificação:** Receber status 400 Bad Request.

### PUT /requests/requestDelivered/:idPedido
**Descrição:** Marca um pedido como entregue.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do pedido válido.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
2. **Erro - Pedido Não Encontrado**
   - **Input:** Token de autenticação válido e ID do pedido inválido.
   - **Verificação:** Receber status 400 Bad Request.

### DELETE /requests/cancelRequest/:idPedido
**Descrição:** Cancela um pedido.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do pedido válido.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
2. **Erro - Pedido Não Encontrado**
   - **Input:** Token de autenticação válido e ID do pedido inválido.
   - **Verificação:** Receber status 400 Bad Request.

## Rotas de Produtos

### POST /products/addProduct
**Descrição:** Adiciona um novo produto.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e todos os campos preenchidos corretamente.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
   - **Exemplo de Request:**
     ```json
     {
       "descricao": "Produto de teste",
       "valorUnidade": 100.50,
       "nomeComercial": "Comercial",
       "nomeTecnico": "Tecnico",
       "peso": "1kg",
       "material": "Metal",
       "dimensoes": "10x10x10",
       "fabricante": "Fabricante"
     }
     ```
2. **Erro - Campos Obrigatórios Faltando**
   - **Input:** Token de autenticação válido e faltando campos obrigatórios.
   - **Verificação:** Receber status 400 Bad Request.
3. **Erro - Sem Permissão**
   - **Input:** Token de autenticação válido, mas usuário não tem permissão.
   - **Verificação:** Receber status 403 Forbidden.

### PUT /products/editProduct/:idProduto
**Descrição:** Edita um produto existente.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido, ID do produto válido e campos preenchidos corretamente.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
   - **Exemplo de Request:**
     ```json
     {
       "descricao": "Produto editado",
       "valorUnidade": 200.50



,
       "nomeComercial": "Comercial Editado",
       "nomeTecnico": "Tecnico Editado",
       "peso": "2kg",
       "material": "Plástico",
       "dimensoes": "20x20x20",
       "fabricante": "Fabricante Editado",
       "statusProduto": "Disponível"
     }
     ```
2. **Erro - Nenhum Dado Fornecido**
   - **Input:** Token de autenticação válido e nenhum dado fornecido para editar.
   - **Verificação:** Receber status 400 Bad Request.
3. **Erro - Sem Permissão**
   - **Input:** Token de autenticação válido, mas usuário não tem permissão.
   - **Verificação:** Receber status 403 Forbidden.

### DELETE /products/deleteProduct/:idProduto
**Descrição:** Deleta um produto existente.

**Casos de Teste:**
1. **Sucesso**
   - **Input:** Token de autenticação válido e ID do produto válido.
   - **Verificação:** Receber status 200 OK e mensagem de sucesso.
2. **Erro - Sem Permissão**
   - **Input:** Token de autenticação válido, mas usuário não tem permissão.
   - **Verificação:** Receber status 403 Forbidden.

## Tratamento de Erros
**Descrição:** Verificar o middleware de tratamento de erros da API.

**Casos de Teste:**
1. **Erro Interno do Servidor**
   - **Input:** Forçar um erro na aplicação.
   - **Verificação:** Receber status 500 Internal Server Error e mensagem "Algo deu errado!".

## Considerações Finais
Este plano de testes cobre os principais cenários de uso da API e deve ser seguido para garantir que todas as funcionalidades estejam funcionando corretamente. Certifique-se de realizar os testes em um ambiente de desenvolvimento e verificar as respostas da API conforme esperado.
