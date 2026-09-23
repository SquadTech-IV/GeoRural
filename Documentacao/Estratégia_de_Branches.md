# 🌳 Estratégia de Branches 

Esta estratégia organiza o trabalho no Git da equipe **SquadTech** para manter a branch `main` sempre estável e pronta para entrega, com desenvolvimento isolado por atividade, rastreabilidade e revisão de qualidade antes de cada integração.

---

## 📋 Fluxo em resumo

Do início ao fim, cada mudança percorre este caminho:

1. A partir da branch da sprint, o desenvolvedor cria uma **branch de feature** para a sua atividade.
2. Desenvolve e testa a própria implementação.
3. O par designado revisa e confirma que o **Definition of Done (DoD)** foi atendido.
4. O desenvolvedor abre um **Pull Request** e avisa a equipe.
5. Após a aprovação, a feature é mesclada na **branch da sprint**.
6. O **Product Owner** integra a branch da sprint na `main` após as features terem sido revisadas e testadas.

---

## 🌿 As branches

A equipe trabalha com três níveis de branch:

| Branch | Para que serve | Nasce de | Como recebe código |
|---|---|---|---|
| `main` | Código estável, pronto para entrega | Base do projeto | Merge da branch da sprint, feito somente pelo PO |
| `SPRINT-N` | Reúne o trabalho daquela sprint | `main` | PR de feature, após revisão e DoD |
| `US-ID`   | Uma atividade ou feature, isolada | Branch da sprint | Commits do autor e atualizações (merge/rebase) conforme necessário |

---

## 🔀 Branches de feature

- Cada desenvolvedor cria a sua branch de feature a partir da branch da sprint e trabalha a atividade de forma isolada, sem impactar o restante do código.
- Dentro da própria branch, pode fazer commits e atualizar a branch com merge ou rebase conforme necessário, organizando o trabalho como preferir.
- **Antes de abrir o PR**, atualize a feature com a branch da sprint (merge ou rebase) para resolver eventuais conflitos localmente e evitar surpresas na integração.
- O responsável pela branch resolve os conflitos da sua própria implementação. Quando o conflito envolver regras ou código de outro desenvolvedor, deve consultar essa pessoa antes de resolver, para não descartar ou quebrar o trabalho dela.
- Após a feature ser integrada e o PR aprovado, a branch de feature pode ser excluída — mantém o repositório limpo.

---

## ✅ Revisão, DoD e Pull Request

Concluída a atividade na branch de feature, a integração na branch da sprint segue este fluxo:

1. O desenvolvedor testa a própria implementação.
2. O par designado para revisão testa a funcionalidade e verifica se todos os critérios do **Definition of Done (DoD)** foram atendidos. Se o revisor estiver indisponível, outro integrante assume a revisão para não travar a entrega.
3. Aprovada a revisão, o desenvolvedor abre um **Pull Request** descrevendo a funcionalidade ou correção, a justificativa das mudanças e as evidências de que o DoD foi atendido.
4. Ao abrir o PR, avise a equipe pelos meios oficiais de comunicação, para que a revisão e o merge não fiquem parados.
5. Somente após a aprovação do PR a feature é mesclada na branch da sprint.
6. Caso o PR seja reprovado, o responsável realiza as correções solicitadas, testa novamente e solicita nova revisão antes do merge.

> Os merges são feitos com **merge commit** (`git merge --no-ff`), preservando o histórico de commits e o ponto de integração — melhor para auditoria e para a avaliação individual das contribuições.

Os critérios do Definition of Done estão definidos em documento próprio.

---

## 🚀 Integração na `main` (Product Owner)

A integração da branch da sprint na `main` é feita **exclusivamente pelo Product Owner**, garantindo que a `main` contenha apenas código validado e pronto para entrega.

- O PO pode realizar essa integração a qualquer momento; as aulas de Laboratório de Banco de Dados são o momento dedicado para o PO analisar essa integração com mais atenção.
- Antes de mesclar, o PO confirma que as features da sprint foram revisadas e testadas e que os critérios definidos para a sprint foram atendidos (cada feature já passou pelo seu PR).
- Recomenda-se registrar a integração como um PR de `SPRINT-N → main`, para deixar histórico do que entrou.
- Quando a branch da sprint estiver pronta para integração na `main`, o responsável avisa o PO, para que a análise e o merge não fiquem parados.

---

## 🚨 Correção urgente na `main`

Se for encontrado um erro crítico já na `main` (por exemplo, durante uma demonstração):

1. Cria-se uma branch a partir da `main`.
2. Corrige-se o problema.
3. Revisa-se a correção.
4. O Product Owner mescla a correção de volta na `main`.
5. Após o merge na `main`, a correção é integrada à branch da sprint por Pull Request, mantendo ambas alinhadas.

---

<p align="center"><sub>Equipe SquadTech</sub></p>
