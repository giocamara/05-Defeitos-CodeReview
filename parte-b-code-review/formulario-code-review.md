# 🔎 Formulário — Parte B

> Preencha uma seção por finding. O mínimo esperado é **6 findings**.

**Dupla:** Giovana Nogueira + 226759 + Rafael Ribeiro 226058
**Data da revisão:** 22/04/2026

---

### Finding #1

**📍 Linha(s):** 11
**🏷 Rótulo:** blocker
**📂 Dimensão:** CSegurança
**⚠️ Severidade:** Crítica

**🐛 Problema:** SQL Injection
O código concatena diretamente o parâmetro nome na string da query SQL. Isso permite que um atacante manipule a consulta para extrair dados indevidos ou deletar tabelas (ex: passar ' OR '1'='1).

**💡 Sugestão de correção:**

```javascript
// Use queries parametrizadas (Prepared Statements)
async function buscarUsuarioPorNome(nome) {
  const query = "SELECT * FROM usuarios WHERE nome = ?";
  return db.executarQuery(query, [nome]);
}
```

**📚 Referência (opcional):**

---

### Finding #2

**📍 Linha(s):** 43-93
**🏷 Rótulo:** major
**📂 Dimensão:** Complexidade
**⚠️ Severidade:** Alta

**🐛 Problema:** Alta Complexidade Ciclomática.
Uso da função gets(). Esta função é obsoleta e perigosa porque não verifica o limite do buffer (tamanho do array nome). Isso permite um ataque de Buffer Overflow, onde um usuário pode inserir mais de 20 caracteres e sobrescrever áreas adjacentes da memória, podendo causar o travamento do programa ou execução de código malicioso.

**💡 Sugestão de correção:**

```javascript
// Use cláusulas de guarda (Guard Clauses) para retornar cedo e achatar a lógica
if (usuario.tipo === 'professor') {
  return calcularLimiteProfessor(usuario);
}
if (usuario.tipo === 'aluno') {
  return calcularLimiteAluno(usuario);
}
```

### Finding #3

**📍 Linha(s):** 43 e 102
**🏷 Rótulo:** major
**📂 Dimensão:** Padrôes
**⚠️ Severidade:** Média

**🐛 Problema:**
Duplicação de Código (WET - Write Everything Twice). As funções calcularLimiteEmprestimo e calcularLimiteComSuspensao repetem quase toda a lógica de negócio de limites. Se uma regra mudar, o desenvolvedor terá que lembrar de alterar em dois lugares, o que gera inconsistência.
**💡 Sugestão de correção:**

```javascript
// Unifique a lógica em uma única função ou extraia a lógica comum para um utilitário
// e apenas adicione a verificação de suspensão no início.
```

---
---

### Finding #4

**📍 Linha(s):** 16 e 19
**🏷 Rótulo:** major
**📂 Dimensão:** Erros
**⚠️ Severidade:** Média

**🐛 Problema:** Condição de Corrida (Race Condition). A função busca o usuário, altera o objeto em memória e salva de volta. Se duas requisições de atualização ocorrerem ao mesmo tempo, uma pode sobrescrever a outra. Além disso, é ineficiente buscar o objeto inteiro para atualizar apenas um campo.

**💡 Sugestão de correção:**

```javascript
// Atualize apenas o campo necessário diretamente no banco
async function atualizarEmail(id, novoEmail) {
  await db.updateField('usuarios', id, { email: novoEmail });
  logger.info('Email atualizado: ' + novoEmail);
}
```

---

### Finding #5

**📍 Linha(s):** 34 - 36
**🏷 Rótulo:** major
**📂 Dimensão:** Erros
**⚠️ Severidade:** Média

**🐛 Problema:** Condição de Corrida (Race Condition). A função busca o usuário, altera o objeto em memória e salva de volta. Se duas requisições de atualização ocorrerem ao mesmo tempo, uma pode sobrescrever a outra. Além disso, é ineficiente buscar o objeto inteiro para atualizar apenas um campo.

**💡 Sugestão de correção:**

```javascript
// Atualize apenas o campo necessário diretamente no banco
async function atualizarEmail(id, novoEmail) {
  await db.updateField('usuarios', id, { email: novoEmail });
  logger.info('Email atualizado: ' + novoEmail);
}
```

---

### Finding #6

**📍 Linha(s):** 7 
**🏷 Rótulo:** nit
**📂 Dimensão:** Padrôes
**⚠️ Severidade:** Baixa

**🐛 Problema:**
Uso de SELECT *. É uma má prática buscar todas as colunas do banco de dados. Isso consome mais banda, memória e pode expor campos sensíveis (como o hash da senha) desnecessariamente no retorno da função.

**💡 Sugestão de correção:**

```javascript
// Liste apenas as colunas necessárias para a funcionalidade
async function listarUsuariosAtivos() {
  return db.executarQuery('SELECT id, nome, email FROM usuarios WHERE ativo = 1');
}
```

---

## ✅ Checklist final

- [ ] Há pelo menos 6 findings preenchidas
- [ ] Cada finding cita linha, dimensão, rótulo e severidade
- [ ] As sugestões são concretas e acionáveis
- [ ] Pelo menos uma finding cobre segurança
- [ ] Pelo menos uma finding cobre complexidade
