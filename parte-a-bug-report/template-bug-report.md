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

<!-- Para reports adicionais, copie o bloco acima trocando o número. -->

---

## ✅ Critérios de qualidade do bug report
*(Use para conferir antes de entregar)*

- [ ] Título descritivo — outra pessoa entende o problema só pelo título?
- [ ] Passos são **numerados** e **reproduzíveis** por terceiros?
- [ ] Há **pelo menos uma evidência** (screenshot, GIF ou log)?
- [ ] Severidade tem **justificativa explícita**?
- [ ] Prioridade tem **justificativa explícita**?
- [ ] Ambiente inclui **navegador + SO**?
- [ ] "Esperado vs. Obtido" deixa o gap claro?

## ✅ Checklist de qualidade dos reports

Antes de submeter, confirme em cada report:

- [ ] Título é específico e acionável (não `"Não funciona"`).
- [ ] Passos estão **numerados** e são reproduzíveis por terceiros.
- [ ] Há **pelo menos uma evidência** por report (imagem, GIF ou log).
- [ ] Severidade tem **justificativa explícita**.
- [ ] Prioridade tem **justificativa explícita**.
- [ ] Ambiente inclui **navegador + SO**.
- [ ] "Esperado × Obtido" deixa a diferença clara.
- [ ] Os 3 defeitos reportados cobrem **categorias diferentes**
      (funcional, UX, validação, persistência, etc.)
