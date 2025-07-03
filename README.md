# Projeto de testes API com Postman - QA 

- Neste projeto, simulei um pequeno sistema de autenticação com endpoints de cadastro e login usando o Beeceptor. Com o Postman, criei requisições e testes automatizados para validar o comportamento da API, como status code, mensagens de retorno e dados esperados.

📝 Ferramentas utilizadas:
| Ferramenta      | Função no projeto                          |
| --------------- | ------------------------------------------------------------------------- |
| [Beeceptor](https://app.beeceptor.com/)    | API simulada / mock que responde requisições   |
| [Postman](https://www.postman.com/)        | Cliente para enviar requisições e rodar testes |
| README + GitHub                            | Documentação e evidências do projeto de QA     |
| JSON (body)                                | Dados enviados na requisição (simula o que o usuário digitou)
| JavaScript                                 | Scripts para validar as respostas da API (aba Tests no Postman)

📝 Casos de Teste:
| Method | Endpoint    | Cenário                                | Validações esperadas                                        |
| ------ | ----------- | -------------------------------------- | ----------------------------------------------------------- |
| POST   | `/login`    | Login com dados válidos                | Status `200`, mensagem: `"Login realizado com sucesso!"`    |
| POST   | `/login`    | Login com **senha incorreta**          | Status `401`, mensagem: `"Senha incorreta"`                 |
| POST   | `/register` | Cadastro com dados válidos             | Status `201`, mensagem: `"Cadastro realizado com sucesso!"` |
| POST   | `/register` | Cadastro com **e-mail já existente**   | Status `409`, mensagem: `"E-mail já cadastrado"`            |
| POST   | `/login`    | Validação de **tempo de resposta**     | Resposta abaixo de `700ms`                                  |
| POST   | `/login`    | Validação de **header** `Content-Type` | Header `"Content-Type"` contém `"application/json"`         |                            
| POST   | `/register` | Cadastro com **e-mail já existente**   | `409 Conflict`, mensagem:  `"E-mail já cadastrado"`         |
| POST   | `/login`    | Envio de **dados incompletos (sem senha)** | `400 Bad Request`, mensagem: `"Senha é obrigatória"`        |
| POST   | `/register  | Envio de **dados incompletos (sem e-mail)**| `400 Bad Request`, mensagem:`"E-mail é obrigatório"`        |
| POST   | `/register  | Envio com **formato inválido** (e-mail errado) | `422 Unprocessable Entity`, mensagem: `"E-mail em formato inválido"` |


## 🧪 Exemplos de Testes Automatizados

```javascript
pm.test("Status code é 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Mensagem de sucesso", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.message).to.eql("Login realizado com sucesso!");
});
```

📊 Organização geral de evolução nos testes: 

| Nível | Tipo de Teste              | Exemplo                                              |
| ----- | -------------------------- | ---------------------------------------------------- |
| 1️⃣   | Positivo básico            | Login e Cadastro com dados válidos                       |
| 2️⃣   | Negativo / erro de entrada | Login com senha errada, cadastro com email duplicado,etc |
| 3️⃣   | Validações extras          | Performance, headers, tipos de dados, token          |

### Regra: Login realizado com sucesso: 
  - Method: POST
  - Path: /login
  - Request condition: Request path exactly matches
  - Match value/expression: /login 
  - Status code: 200
  - Response body: 
     ```{
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
   ```{
      "message": "Senha incorreta"
    }


### Regra: Cadastro realizado com sucesso 

  - Method: POST
  - Path: /register
  - Request condition: Request path exactly matches
  - Match value/expression: /register
  - Status code: 200
  - Response body:
      ```{
            "message": "Usuário cadastrado com sucesso!",
            "user": {
            "id": 2,
            "email": "novo@email.com",
            "nome": "Novo Usuário"
            }
          }

#### Cursos na plataforma Alura que estão me auxiliando nos estudos, em teoria e prática:
- Padrões de API: do HTTP à modelagem de APIs
- JavaScript: implementando CRUD com requisições HTTP


