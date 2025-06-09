API de Gerenciamento de Tarefas
Este projeto apresenta uma API RESTful desenvolvida para o gerenciamento de tarefas, incluindo um sistema de autenticação de usuários baseado em JWT. A aplicação foi construída com NestJS e utiliza TypeORM com um banco de dados SQLite, o que simplifica a configuração do ambiente de desenvolvimento.

Rotas da API
A seguir estão detalhadas as rotas disponíveis na API.

1. Autenticação
Endpoints para registro e login de usuários.

Registrar um Novo Usuário

Endpoint: POST /auth/register

Corpo da Requisição:

{
  "username": "novo_usuario",
  "password": "senha_forte"
}

Retorno em caso de sucesso:

{
  "message": "Usuário registrado com sucesso"
}

Exemplo com cURL:

curl -X POST http://localhost:3000/auth/register \
-H "Content-Type: application/json" \
-d '{"username":"novo_usuario","password":"senha_forte"}'

Efetuar Login

Endpoint: POST /auth/login

Corpo da Requisição:

{
  "username": "novo_usuario",
  "password": "senha_forte"
}

Retorno em caso de sucesso:

{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6..."
}

Exemplo com cURL:

curl -X POST http://localhost:3000/auth/login \
-H "Content-Type: application/json" \
-d '{"username":"novo_usuario","password":"senha_forte"}'

2. Tarefas (Tasks)
Observação Importante: Todas as rotas de tarefas são protegidas e requerem um token de autenticação. O token JWT deve ser enviado no cabeçalho Authorization da seguinte forma: Bearer <seu_token_jwt>.

Criar uma Nova Tarefa

Endpoint: POST /tasks

Corpo da Requisição:

{
  "title": "Finalizar relatório",
  "description": "Revisar e enviar o relatório trimestral."
}

Retorno da API:

{
  "id": 1,
  "title": "Finalizar relatório",
  "description": "Revisar e enviar o relatório trimestral.",
  "status": "PENDENTE"
}

Exemplo com cURL:

curl -X POST http://localhost:3000/tasks \
-H "Authorization: Bearer <seu_token_jwt>" \
-H "Content-Type: application/json" \
-d '{"title":"Finalizar relatório","description":"Revisar e enviar o relatório trimestral."}'

Obter Todas as Tarefas do Usuário

Endpoint: GET /tasks

Retorno da API:

[
  {
    "id": 1,
    "title": "Finalizar relatório",
    "description": "Revisar e enviar o relatório trimestral.",
    "status": "PENDENTE"
  }
]

Exemplo com cURL:

curl -X GET http://localhost:3000/tasks \
-H "Authorization: Bearer <seu_token_jwt>"

Modificar o Status de uma Tarefa

Endpoint: PATCH /tasks/:id/status

Parâmetro de Rota: id (O ID da tarefa)

Corpo da Requisição:

{
  "status": "CONCLUÍDO"
}

Retorno da API:

{
  "id": 1,
  "title": "Finalizar relatório",
  "description": "Revisar e enviar o relatório trimestral.",
  "status": "CONCLUÍDO"
}

Exemplo com cURL:

curl -X PATCH http://localhost:3000/tasks/1/status \
-H "Authorization: Bearer <seu_token_jwt>" \
-H "Content-Type: application/json" \
-d '{"status":"CONCLUÍDO"}'

Excluir uma Tarefa

Endpoint: DELETE /tasks/:id

Parâmetro de Rota: id (O ID da tarefa)

Retorno em caso de sucesso: Código de status 204 No Content.

Exemplo com cURL:

curl -X DELETE http://localhost:3000/tasks/1 \
-H "Authorization: Bearer <seu_token_jwt>"

Ferramentas e Tecnologias
NestJS: Um framework Node.js para construir aplicações de servidor eficientes, escaláveis e bem arquitetadas.

TypeORM: Mapeador objeto-relacional (ORM) compatível com múltiplos bancos de dados, configurado aqui para usar SQLite.

SQLite: Um banco de dados SQL embutido, leve e que não requer um servidor dedicado, perfeito para ambientes de desenvolvimento.

JWT (JSON Web Tokens): Padrão aberto para criar tokens de acesso que permitem uma autenticação segura entre as partes.

Bcrypt: Biblioteca para a criação de hashes de senhas, assegurando que as credenciais dos usuários fiquem protegidas no banco de dados.

Jest: Framework para a execução de testes em JavaScript, utilizado para os testes unitários da aplicação.

Instalação e Configuração
Para configurar o ambiente localmente, siga estas instruções:

Clone o repositório do projeto:

git clone https://github.com/PabloVinif/2bmTopicosProgramacao7s


Instale as dependências necessárias:

npm install

Inicie a aplicação em modo de desenvolvimento:

npm run start

Após esses passos, a API estará acessível em http://localhost:3000.

Executando os Testes
Execute o seguinte comando para rodar a suíte de testes unitários e garantir a integridade do código:

npm run test

Detalhes Adicionais
A segurança das senhas é garantida pelo uso de hash com a biblioteca bcrypt.

O uso do SQLite como banco de dados agiliza a configuração inicial, pois não há necessidade de instalar ou gerenciar um serviço de banco de dados separado.

Pablo Vinicius Formagio Lima

RA: 1993321-2