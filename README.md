# Projeto QA 

- Neste projeto, simulei um pequeno sistema de autenticação com endpoints de cadastro e login usando o Beeceptor. Com o Postman, criei requisições e testes automatizados para validar o comportamento da API, como status code, mensagens de retorno e dados esperados.

📝 Ferramentas utilizadas:
- [Postman](https://www.postman.com/)
- [Beeceptor](https://app.beeceptor.com/)
- JSON
- Scripts de Teste em JavaScript

📝 Casos de Teste:
POST /login → Login com dados válidos
POST /register → Cadastro com dados válidos
Validação de status 200 e mensagens de sucesso

## 🧪 Exemplos de Testes Automatizados

```javascript
pm.test("Status code é 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Mensagem de sucesso", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.message).to.eql("Login realizado com sucesso!");
});

📊 Organização geral de evolução nos testes: 

| Nível | Tipo de Teste              | Exemplo                                              |
| ----- | -------------------------- | ---------------------------------------------------- |
| 1️⃣   | Positivo básico            | Login e Cadastro com dados válidos                   |
| 2️⃣   | Negativo / erro de entrada | Login com senha errada, cadastro com email duplicado |
| 3️⃣   | Validações extras          | Performance, headers, tipos de dados, token          |

### Regra: Login realizado com sucesso: 
  - Method: POST
  - Path: /login
  - Request condition: Request path exactly matches
  - Match value/expression: /login 
  - Status code: 200
  - Response body: 
        {
          "message": "Login realizado com sucesso!",
          "token": "abc123xyz",
          "user": {
          "id": 1,
          "email": "juliateles@email.com",
          "nome": "Júlia Teles"
          }
        }

### Regra: Login com senha incorreta

- Method: POST
- Path: /login
- Request condition: Request body contains
- Match value: `"senha": "errada"`
- Status code: 401 Unauthorized
- Response body: 
    {
      "message": "Senha incorreta"
    }


### Regra: Cadastro realizado com sucesso 

  - Method: POST
  - Path: /register
  - Request condition: Request path exactly matches
  - Match value/expression: /register
  - Status code: 200
  - Response body:
          {
            "message": "Usuário cadastrado com sucesso!",
            "user": {
            "id": 2,
            "email": "novo@email.com",
            "nome": "Novo Usuário"
            }
          }
