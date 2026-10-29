## 🗃️ Sprint backlog

| **ID** | **RANK** | **USER STORY** | **PRIORIDADE** | **ESTIMATIVA** | **SPRINT** |
|:-:|:-:|:-:|:-:|:-:|:-:|
| US#11  | 17       | Como gestor, quero acessar o portal, as APIs, o GeoDataLake e o Airflow pela internet, em ambiente de nuvem, para acompanhar e avaliar a solução a qualquer momento, sem depender do computador de alguém da equipe.                                                                                                                                             | ALTA           | 5              |  3   |
| US#10  | 18       | Como operador de dados, quero que o processamento de cada conjunto rode automaticamente em etapas encadeadas no Airflow (recebimento, validação, tratamento, cálculo, qualidade e publicação), registrando a situação, os erros e as reexecuções de cada etapa, para que todo dado siga sempre o mesmo caminho e eu possa reprocessar apenas a etapa que falhou. | ALTA           | 8              |  3   |
| US#13  | 19       | Como administrador, quero que o portal e as APIs só possam ser usados mediante login e que cada pessoa veja e faça apenas o que o seu perfil permite (administrador, operador de dados, analista, gestor ou auditor), para proteger os dados e impedir que alguém altere o que não é de sua responsabilidade.                                                    | ALTA           | 5              |  3   |
| US#17  | 20       | Como analista, quero consultar por API o catálogo, os dados, os indicadores, as versões, a qualidade, a linhagem e a situação das execuções, com documentação clara, para integrar os resultados a outros sistemas sem depender do portal.                                                                                                                       | ALTA           | 3              |  3   |
| US#18  | 21       | Como analista, quero ver os indicadores em uma tabela com filtros (município, imóvel, indicador e versão) e em gráficos, para comparar resultados e identificar rapidamente onde estão os problemas. | ALTA           | 5              |  3   |
| US#19  | 22       | Como auditor, quero comparar duas versões publicadas de um mesmo indicador, para identificar o que mudou entre elas e o motivo da mudança (dado de origem, regra ou parâmetro).                                                                                                                                                                                  | ALTA           | 5              |  3   |
| US#21  | 23       | Como gestor, quero ver os indicadores consolidados por município, para comparar a situação ambiental entre os 399 municípios do Paraná e direcionar ações de planejamento e fiscalização.                                                                                                                                                                        | ALTA           | 5              |  3   |
| US#20  | 24       | Como auditor, quero consultar o histórico das ações realizadas na plataforma (envios de arquivos, mudanças de regras, execuções, publicações, downloads e acessos à API), com o responsável, a data e a hora de cada uma, para saber quem fez o quê e quando.                                                                                                    | ALTA           | 5              |  3   |
| US#22  | 25       | Como analista, quero saber quanto da área de cada imóvel é coberta por vegetação nativa, em hectares e em percentual (indicador ICV), para acompanhar o grau de conservação dos imóveis.                                                                                                                                                                         | MÉDIA          | 3              |  3   |
| US#23  | 26       | Como analista, quero saber quanto da Área de Preservação Permanente de cada imóvel está coberta por vegetação nativa e quantos hectares precisam ser recuperados (indicador IAPP), para dimensionar o passivo ambiental do imóvel.                                                                                                                               | MÉDIA          | 5              |  3   |
| US#24  | 27       | Como analista, quero saber se e quanto cada imóvel se sobrepõe a unidades de conservação, terras indígenas, territórios quilombolas e florestas públicas (indicador ISAP), para avaliar a conformidade do imóvel com as áreas protegidas. | MÉDIA          | 5              |  3   |
| US#25  | 28       | Como analista, quero saber quanto foi desmatado dentro de cada imóvel após os marcos de 22/07/2008, 31/07/2019 e 31/12/2020, em hectares e em percentual (indicador IDesmat), para identificar supressões de vegetação ocorridas depois de cada data de referência.                                                                                              | MÉDIA          | 5              | 3  |
| US#26  | 29       | Como analista, quero saber quantos focos de calor foram detectados dentro de cada imóvel no período, proporcionalmente ao tamanho do imóvel (indicador IFC), para identificar imóveis com maior ocorrência de queimadas.                                                                                                                                         | MÉDIA          | 3              | 3 |
| US#27  | 30       | Como analista, quero baixar os resultados de uma versão publicada em CSV, JSON ou GeoJSON, para usá-los em planilhas e sistemas de informação geográfica sem precisar tratar os dados.                                                                                                                                                                           | MÉDIA          | 3              | 3 |
| US#28  | 31       | Como operador de dados, quero acompanhar no portal um resumo da operação (conjuntos publicados, execuções concluídas, registros em quarentena e duração média) e a lista de execuções do pipeline, para identificar falhas rapidamente sem precisar abrir o Airflow.                                                                                             | MÉDIA          | 5 | 3 |
| US#30  | 32       | Como administrador, quero acompanhar no portal os logs, o estado de saúde e o consumo de recursos dos componentes (portal, API, banco e Airflow), para agir antes que uma falha deixe a plataforma indisponível.                                                                                                                                                 | BAIXA          | 5              | 3 |
| US#31  | 33       | Como administrador, quero cadastrar, editar e desativar usuários e alterar seus perfis pelo portal, para controlar quem tem acesso à plataforma sem mexer diretamente no banco de dados. | BAIXA          | 3              | 3  |
| US#34 | 34 | Como operador de dados, quero cadastrar arquivos em lote para agilizar o processo de upload dos dados. | BAIXA | 5 | 3 |

## 🎯 Meta da Sprint

A aplicação deve ser capaz de demonstrar o cálculo correto de todos os indicadores restantes sobre um imóvel ou sobre um município, também possui separação e atribuição de ações para cada tipo de usuário do sistema. User Stories contempladas: US#13, US#21, US#23, US#24, US#25 e US#26.

## 🏁 DoD

### US#10

**Como operador de dados, quero que o processamento de cada conjunto rode automaticamente em etapas encadeadas no Airflow (recebimento, validação, tratamento, cálculo, qualidade e publicação), registrando a situação, os erros e as reexecuções de cada etapa, para que todo dado siga sempre o mesmo caminho e eu possa reprocessar apenas a etapa que falhou.**

- As etapas de recebimento, validação, tratamento, cálculo, verificação de qualidade e publicação do pipeline executam em ordem encadeada automática via Airflow.
- O status de cada etapa, os erros encontrados e o histórico de reexecuções ficam armazenados nos logs.
- A reexecução de um fluxo permite reiniciar exclusivamente a etapa que falhou.

---

### US#11

**Como gestor, quero acessar o portal, as APIs, o GeoDataLake e o Airflow pela internet, em ambiente de nuvem, para acompanhar e avaliar a solução a qualquer momento, sem depender do computador de alguém da equipe.**

- A infraestrutura da plataforma está implantada e acessível via internet em ambiente de nuvem.
- Os acessos ao portal, às APIs REST, às zonas do GeoDataLake e ao Airflow ocorrem por URLs públicas sob conexão segura HTTPS.
- O ambiente operacional e suas dependências funcionam sem necessidade de execução local.

---

### US#13

**Como administrador, quero que o portal e as APIs só possam ser usados mediante login e que cada pessoa veja e faça apenas o que o seu perfil permite (administrador, operador de dados, analista, gestor ou auditor), para proteger os dados e impedir que alguém altere o que não é de sua responsabilidade.**

- O acesso ao portal e às APIs exige autenticação prévia por login e senha.
- O sistema valida as ações com base nos 5 perfis definidos (administrador, operador de dados, analista, gestor e auditor).
- Tentativas de acesso não autorizadas por perfil retornam resposta de acesso negado (HTTP 403)

---

### US#17

**Como analista, quero consultar por API o catálogo, os dados, os indicadores, as versões, a qualidade, a linhagem e a situação das execuções, com documentação clara, para integrar os resultados a outros sistemas sem depender do portal.**

- A API REST oferece endpoints documentados (OpenAPI/Swagger) para consulta do catálogo, dados, indicadores, versões, qualidade, linhagem e execuções.
- A API aceita autenticação via token e retorna respostas em formato padronizado.
- É possível obter a linhagem completa do dado do resultado até a origem exclusivamente via API.

---

### US#18

**Como analista, quero ver os indicadores em uma tabela com filtros (município, imóvel, indicador e versão) e em gráficos, para comparar resultados e identificar rapidamente onde estão os problemas.**

- O portal exibe os indicadores calculados em tabela estruturada com suporte a filtros combinados (município, imóvel, indicador e versão).
- A interface gráfica exibe componentes visuais e gráficos para facilitar a comparação dos indicadores.
- A aplicação dos filtros atualiza a visualização da tabela e dos gráficos em menos de 2 segundos.

---

### US#19

**Como auditor, quero comparar duas versões publicadas de um mesmo indicador, para identificar o que mudou entre elas e o motivo da mudança (dado de origem, regra ou parâmetro).**

- O sistema permite selecionar duas versões publicadas de um mesmo indicador e exibe as divergências lado a lado.
- O comparativo destaca visualmente as alterações numéricas e geográficas entre as versões.
- O relatório de comparação explicita a causa das mudanças (dados de origem, regras de negócio ou parâmetros).

---

### US#20

**Como auditor, quero consultar o histórico das ações realizadas na plataforma (envios de arquivos, mudanças de regras, execuções, publicações, downloads e acessos à API), com o responsável, a data e a hora de cada uma, para saber quem fez o quê e quando.**

- Todas as ações na plataforma (uploads, alterações de regras, execuções, publicações, downloads e chamadas à API) são registradas de forma imutável.
- Cada registro de log armazena a identificação do responsável, tipo de ação, data e hora exatas. 
- O perfil de Auditor dispõe de uma interface de busca para consultar e filtrar o histórico das operações.

---

### US#21

**Como gestor, quero ver os indicadores consolidados por município, para comparar a situação ambiental entre os 399 municípios do Paraná e direcionar ações de planejamento e fiscalização.**

- Os indicadores são calculados e agregados para os 399 municípios do estado do Paraná.
- O portal disponibiliza visões consolidadas e relatórios municipais comparativos.
- Os totais municipais equivalem rigorosamente ao somatório e à média dos valores dos imóveis da respectiva localidade.

---

### US#22

**Como analista, quero saber quanto da área de cada imóvel é coberta por vegetação nativa, em hectares e em percentual (indicador ICV), para acompanhar o grau de conservação dos imóveis.**

- O sistema calcula a área de vegetação nativa contida no imóvel rural em hectares e em percentual sobre a área total do imóvel.
- O cálculo é feito utilizando projeção equivalente e geometrias validadas.
- Os resultados são salvos e atrelados à versão publicada no GeoDataLake.

---

### US#23

**Como analista, quero saber quanto da Área de Preservação Permanente de cada imóvel está coberta por vegetação nativa e quantos hectares precisam ser recuperados (indicador IAPP), para dimensionar o passivo ambiental do imóvel.**

- O sistema cruza a camada de Área de Preservação Permanente (APP) com a vegetação nativa de cada imóvel.
- É calculada a extensão de vegetação preservada na APP e a área de passivo ambiental a ser recuperada (em hectares).
- Imóveis sem presença de APP têm a condição explicitada e tratada sem erro de execução.

---

### US#24

**Como analista, quero saber se e quanto cada imóvel se sobrepõe a unidades de conservação, terras indígenas, territórios quilombolas e florestas públicas (indicador ISAP), para avaliar a conformidade do imóvel com as áreas protegidas.**

- O sistema realiza o cruzamento geoespacial dos imóveis com camadas de Unidades de Conservação, Terras Indígenas, Territórios Quilombolas e Florestas Públicas.
- O resultado detalha se há sobreposição e calcula a área atingida em hectares e percentual para cada categoria.
- Caso não haja sobreposição, o sistema registra formalmente a ausência de conflito (0 ha / 0%).

---

### US#25

**Como analista, quero saber quanto foi desmatado dentro de cada imóvel após os marcos de 22/07/2008, 31/07/2019 e 31/12/2020, em hectares e em percentual (indicador IDesmat), para identificar supressões de vegetação ocorridas depois de cada data de referência.**

- O sistema quantifica a supressão de vegetação dentro do imóvel ocorrida após os marcos de 22/07/2008, 31/07/2019 e 31/12/2020.
- O resultado expressa a área desmatada em hectares e em percentual por marco temporal.
- A regra de cálculo grava a data de corte utilizada na linhagem do indicador.

---

### US#26

**Como analista, quero saber quantos focos de calor foram detectados dentro de cada imóvel no período, proporcionalmente ao tamanho do imóvel (indicador IFC), para identificar imóveis com maior ocorrência de queimadas.**

- O sistema contabiliza os focos de calor registrados dentro do perímetro de cada imóvel no período.
- O indicador calcula a taxa de ocorrência proporcional à área do imóvel.
- Dados recebidos por API (como atualizações diárias) são integrados corretamente ao processamento do indicador.

---

### US#27

**Como analista, quero baixar os resultados de uma versão publicada em CSV, JSON ou GeoJSON, para usá-los em planilhas e sistemas de informação geográfica sem precisar tratar os dados.**

- O portal e a API disponibilizam a exportação dos dados de versões publicadas nos formatos CSV, JSON e GeoJSON.
- Os arquivos exportados preservam os atributos das tabelas e a integridade vetorial das geometrias.
- A ação de download gera um evento registrado no histórico de auditoria.

---

### US#28

**Como operador de dados, quero acompanhar no portal um resumo da operação (conjuntos publicados, execuções concluídas, registros em quarentena e duração média) e a lista de execuções do pipeline, para identificar falhas rapidamente sem precisar abrir o Airflow.**

- O portal exibe um dashboard operacional exibindo: total de conjuntos publicados, execuções concluídas, itens em quarentena e tempo médio das execuções.
- A lista de execuções ativas e recentes do pipeline é exibida com status atualizado.
- Falhas nas etapas podem ser identificadas diretamente no painel do portal sem abrir o Airflow.

---

### US#30

**Como administrador, quero acompanhar no portal os logs, o estado de saúde e o consumo de recursos dos componentes (portal, API, banco e Airflow), para agir antes que uma falha deixe a plataforma indisponível.**

- O portal apresenta o status em tempo real (online/offline) dos serviços: portal, API, banco de dados e Airflow.
- O painel indica o uso de recursos de computação (CPU, memória e armazenamento de dados).
- O administrador visualiza alertas em caso de instabilidade nos componentes.

---

### US#31

**Como administrador, quero cadastrar, editar e desativar usuários e alterar seus perfis pelo portal, para controlar quem tem acesso à plataforma sem mexer diretamente no banco de dados.**

- O portal disponibiliza interface gráfica para cadastrar, editar, desativar usuários e alterar seus perfis de acesso.
- Alterações de permissão passam a valer no próximo acesso/autenticação do usuário.
- As modificações cadastrais e de perfis ficam gravadas na trilha de auditoria.

---

## US#34

**Como operador de dados, quero cadastrar arquivos em lote para agilizar o processo de upload dos dados.**

- O sistema aceita a seleção e o envio simultâneo de múltiplos arquivos/conjuntos por upload no portal ou API.
- Cada arquivo do lote passa individualmente pelo processo de recepção e gravação de hash na zona bruta.
- Falhas no processamento de um arquivo não impedem o recebimento e validação dos demais arquivos do lote.

## 📋 DoR

- Título, descrição e objetivos claros
- Valor agregado ao cliente
- Critérios de aceitação definidos
- Estimativa, prioridade e rank estabelecidos junto com a equipe

## Burndown