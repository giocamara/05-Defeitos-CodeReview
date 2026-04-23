# 📦 Relatório Final

> **Atividade:** Bug Report Profissional + Code Review Guiado
> **Curso:** Qualidade de Software
> **Professor:** Prof. Claudio Nunes

---

## 👥 Identificação da dupla

| Nome completo | RA | GitHub |
|---|---|---|
| Giovana Nogueira | 226759 | @giocamara |
| [Nome 2] | [000000] | [@rafarar |

**Ambiente de testes:** Chrome 121 no Windows 10, GitHub Pages do fork, editor web do GitHub

---

## 📋 Sumário

- [Parte A — Bug Reports](#parte-a--bug-reports)
- [Parte B — Code Review](#parte-b--code-review)
- [Reflexão final](#-reflexão-final)
- [Declarações](#-declarações)

---

## Parte A — Bug Reports

# 🐛 Bug Reports — Parte A

> Preencha uma seção completa para cada defeito encontrado. O mínimo
> exigido é **3 bug reports**. Apague este bloco antes de entregar.

**Dupla:** Giovana Câmara + 226759 + Rafael Ribeiro + 226058
**Data da exploração:*/04/2026
**Navegador usado:** Chrome 121
**Sistema operacional:** Windows 10

---

## BUG-001

**Título:** [Criação de Tarefa] Possível criar tarefa com título vazio

**Severidade:** Medio
**Justificativa da severidade:** não bloqueia o usuário

**Prioridade:** P4
**Justificativa da prioridade:** não bloqueia o usuário

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1.	Deixe o título vazio
2.	Escolha uma categoria, um prazo e uma prioridade
3.	Clique no botão ‘Adicionar Tarefa’

**Resultado esperado:**
Não deveria ser possível inserir uma tarefa com título vazio

**Resultado obtido:**
É possível inserir título vazio

**Evidência:**
É possível ver que a tarefa está sem título ao compararmos com a tarefa de baixo
<img width="886" height="221" alt="image" src="https://github.com/user-attachments/assets/8334a721-37b8-4f5f-9f31-ead35ee0a0b6" />

**Sugestão de causa raiz (opcional):**
Deixar o campo obrigatório

---

## BUG-002

**Título:** [Guardar Tarefa] A tarefa não é salva após reiniciar a pagina

**Severidade:** Critico
**Justificativa da severidade:** Tudo será perdido após reiniciar a pagina

**Prioridade:** P1
**Justificativa da prioridade:** Bloqueia o uso contínuo do usuário

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Preencha os campos para inserir uma tarefa
2. Clique em 'Adicionar Tarefa'
3. Reinicie a página

**Resultado esperado:** Dados serem salvos mesmo após reiniciar a página

**Resultado obtido:** Dados são perdidos após reiniciar a página

**Evidência:**Após reiniciar, é perdido
<img width="824" height="838" alt="image" src="https://github.com/user-attachments/assets/988818fd-3e3c-4a33-b0e6-807e0bc63d97" />
<img width="829" height="891" alt="image" src="https://github.com/user-attachments/assets/61846d85-e1a7-45a8-a8d3-b6103ec6aa34" />

---

## BUG-003

**Título:** [Prioridade] É possível definiar prioridade fora da escala permitida

**Severidade:** Alto
**Justificativa da severidade:** ao definir prioridade fora da escala permitida, uma regra de negócio é quebrada

**Prioridade:** P2
**Justificativa da prioridade:** tem de ser corrigido rapidamente porque uma regra de negócio está sendo infringida

**Ambiente:**
- Navegador: Chrome 121.0
- Sistema Operacional: Windows 10
- Versão da aplicação: TarefaQS v1.0.0

**Passos para reprodução:**
1. Preencha 'Titulo', 'Categoria', 'Prazo'
2. Preencha 'Prioridade' com um número MAIOR que 5, ou menor que 1
3.

**Resultado esperado:** Possível inserir prazo apenas no "Range" permitido (1 a 5)

**Resultado obtido:** Possível inserir prazo menor que 1 ou maior que 5

**Evidência:**

<img width="788" height="266" alt="image" src="https://github.com/user-attachments/assets/673b5674-e806-447e-984f-7f712f5ba5e7" />


---

## Parte B — Code Review

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

### Resumo

| # | Linha | Dimensão | Rótulo | Severidade |
|---|-------|----------|--------|------------|
| 1 |       |          |        |            |
| 2 |       |          |        |            |
| 3 |       |          |        |            |
| 4 |       |          |        |            |
| 5 |       |          |        |            |
| 6 |       |          |        |            |

### Findings detalhadas

> Cole integralmente aqui suas findings copiadas do formulário.

---

## 💭 Reflexão final

> Responda em 1-2 parágrafos. Esta reflexão **é obrigatória**.

**Qual dimensão do checklist foi mais difícil aplicar? Por quê?**

[Escrevam aqui.]

**O que vocês fariam diferente se revisassem o código novamente?**

[Escrevam aqui.]

---

## 📣 Declarações


### Uso de IA como parceiro de trabalho

- [ ] Não usamos IA nesta atividade.
- [ ] Usamos IA para esclarecer conceitos teóricos.
- [ ] Usamos IA para revisar a redação dos bug reports.
- [ ] Usamos IA para discutir se um achado era ou não um defeito.
- [ ] Uso específico: [descreva]

### Declaração de autoria

Declaramos que este relatório é de autoria da dupla, que exploramos
pessoalmente a aplicação da Parte A e lemos o código da Parte B. As
findings aqui registradas representam nosso próprio julgamento
técnico.
