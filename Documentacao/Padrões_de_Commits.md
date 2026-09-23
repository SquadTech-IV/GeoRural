# 📝 Padrões de Commits

Um commit registra uma alteração feita no código e o motivo dela, funcionando como um checkpoint no histórico do projeto. Para manter esse histórico claro e fácil de navegar, a equipe **SquadTech** adota commits semânticos, seguindo o padrão [Conventional Commits](https://www.conventionalcommits.org/): cada commit começa com uma palavra-chave que indica o tipo da mudança e referencia o item do backlog correspondente.

---

## 📐 Formato do commit

Cada commit segue este formato, em uma única linha:

```
tipo(ID): descrição
```

- **tipo** — a categoria da alteração (ver seções abaixo).
- **(ID)** — identificador do item do backlog relacionado à alteração, como User Story, Bug, Task, tarefa técnica ou documentação.
- **descrição** — frase curta e objetiva, no imperativo (adiciona, corrige, remove…), começando com letra minúscula, preferencialmente com até 50 caracteres.
---

## 🔗 Rastreabilidade

Todo commit deve estar vinculado a um item do backlog que represente o objetivo da alteração. O item pode ser uma **User Story, Bug, Task, tarefa técnica ou documentação**.

**Exemplos:**
```
feat(US-102): adiciona página de login
fix(BUG-08): corrige validação de email
docs(DOC-07): adiciona padrão de commits
chore(TECH-12): atualiza dependências
```

---

## 🏷️ Tipos de commit

| Tipo | O que é | Exemplo |
|---|---|---|
| `feat` | Alterações que adicionam uma funcionalidade nova ao projeto | `feat(US-102): adiciona login` |
| `fix` | Correção de um bug ou comportamento errado em algo já existente | `fix(BUG-08): corrige validação` |
| `docs` | Alterações exclusivamente de documentação (README, manuais ou comentários) que não alteram o comportamento do código | `docs(DOC-07): atualiza README` |
| `style` | Alterações exclusivamente de formatação do código, sem modificar seu comportamento (indentação, espaços, lint) | `style(TECH-15): ajusta identação` |
| `refactor` | Melhora a estrutura ou organização do código sem alterar seu comportamento | `refactor(TECH-20): extrai função` |
| `test` | Cria, altera ou remove testes, sem mexer no código de produção | `test(US-122): adiciona testes` |
| `chore` | Manutenção que não adiciona funcionalidade nem corrige bug: configurações, dependências, `.gitignore` e outras tarefas técnicas | `chore(TECH-12): atualiza dependências` |
| `revert` | Desfaz um commit anterior, criando um novo commit com o inverso das mudanças (mantém o histórico) | `revert(BUG-15): reverte alteração do login` |

---

## 🤔 Quando usar cada tipo

Em caso de dúvida, comece pela tabela de decisão:

| Se você… | Use |
|---|---|
| Criou uma funcionalidade | `feat` |
| Corrigiu um bug | `fix` |
| Alterou somente documentação | `docs` |
| Alterou somente formatação | `style` |
| Reorganizou o código sem alterar o comportamento | `refactor` |
| Criou ou alterou testes | `test` |
| Fez manutenção ou configuração | `chore` |
| Precisou desfazer um commit já enviado | `revert` |

**Com mais detalhe:**

- **`feat`** — quando adiciona algo que o sistema não fazia antes (uma tela, um endpoint, um filtro). Se você está consertando algo que já existia, é `fix`, não `feat`.
- **`fix`** — quando corrige um comportamento errado ou bug em algo que já existe (uma validação que falhava, um cálculo incorreto). Se a mudança acrescenta algo novo, é `feat`.
- **`docs`** — quando altera apenas documentação (README, manuais, comentários), sem mudar o comportamento do código. Se você mexeu no código e também no comentário, o tipo é o da alteração principal (o código), não `docs`.
- **`style`** — quando muda apenas a forma do código (indentação, espaços, ponto e vírgula, lint), sem tocar na lógica. Se o comportamento muda, não é `style`.
- **`refactor`** — quando melhora a estrutura ou organização do código sem mudar o que ele faz por fora (extrair função, renomear, remover duplicação). Diferente de `style` (só formatação) e de `fix` (que corrige um erro).
- **`test`** — quando cria, altera ou remove testes, sem mexer no código de produção. Se você criou a funcionalidade e o teste na mesma entrega, o objetivo principal costuma ser `feat`.
- **`chore`** — para manutenção e tarefas técnicas que não adicionam funcionalidade nem corrigem bug: dependências, configurações, `.gitignore`, scripts. É o tipo para o que não se encaixa nos demais.
- **`revert`** — quando precisa desfazer um commit que já foi enviado ou mergeado. O revert cria um novo commit com o inverso das mudanças e mantém o histórico. Para um commit local que ainda não foi enviado, prefira corrigir com amend/rebase (ver seção abaixo).

---

## ⚡ Regras rápidas

- ✅ **Um commit = uma mudança lógica.** Cada commit deve representar um único objetivo. Alterações diferentes e independentes devem ser feitas em commits separados.
- ✅ **Imperativo, minúsculo e curto.** Comece a descrição com verbo no imperativo e letra minúscula ("adiciona", "corrige", "remove"), preferencialmente com até 50 caracteres. Nomes próprios, tecnologias e siglas mantêm a grafia correta (ex.: GitHub, MySQL).
- ✅ **Sempre vincule ao backlog.** Todo commit leva o ID de um item do backlog no escopo.
- ❌ **Não combine tipos.** Um commit tem um único tipo — exemplo inválido: `feat/fix(US-102)`. Se a alteração envolver vários aspectos, use o tipo que melhor representa o objetivo principal; se forem mudanças independentes, separe-as em commits diferentes.

---

## ❌ Certo × Errado

| Commit incorreto | Problema |
|---|---|
| `update` | Sem tipo, sem escopo e sem objetivo |
| `alterações` | Genérico; não diz o que mudou |
| `fix: corrige coisas` | Vago e sem o ID do backlog |
| `feat(US-102): mudanças` | A descrição não explica nada |
| `feat/fix(US-102): login` | Combina dois tipos — não permitido |

**Correto:**
```
feat(US-102): adiciona validação de login
```
Tipo, ID e descrição clara.

---

## 🛠️ Commits fora do padrão

Quando for identificado um commit fora do padrão definido neste documento, o **próprio autor do commit** é o responsável por corrigi-lo, adequando-o às regras aqui estabelecidas pela equipe.

A correção deve ser feita **antes do merge ou da abertura do Pull Request**, usando recursos do Git como:

- `git commit --amend` (para o último commit)
- rebase interativo (para commits anteriores)

Assim, o histórico do projeto permanece consistente e rastreável.

---

## 📌 Resumo

**Formato:** `tipo(ID): descrição`

**Tipos:** `feat` · `fix` · `docs` · `style` · `refactor` · `test` · `chore` · `revert`

---

<p align="center"><sub>Equipe SquadTech</sub></p>
