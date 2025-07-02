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
});```
