<div align="center">
  <img width="1822" height="292" alt="image" src="https://github.com/user-attachments/assets/ef77db35-a616-48cf-ba4c-43bc3310b7c0" />
</div>

<p align="center">
  <a href ="#desafio"> Desafio</a>  |
  <a href ="#solucao"> Solução Proposta</a>  |   
  <a href ="#backlog"> Backlog do Produto</a>  |
  <a href ="#cronograma"> Cronograma de Sprints</a> |
  <a href ="#tecnologias">Tecnologias</a> |
  <a href ="#estrutura">Estrutura do Projeto</a> |
  <a href ="#docs">Documentação</a> |
  <a href ="#equipe"> Equipe</a> |
</p>

## 📝 Desafio
<a id="desafio"></a>
A Visiona trabalha com informações territoriais, ambientais e geoespaciais utilizadas em análises, planejamento e tomada de decisão. Esses dados, especialmente os relacionados a imóveis rurais, são provenientes de diferentes fontes e entidades, possuem formatos e níveis de qualidade variados e passam por atualizações, tratamentos e consolidações ao longo do tempo.
O principal desafio é garantir a rastreabilidade, qualidade e governança dos dados, permitindo identificar a origem, versão, tratamentos realizados e regras aplicadas na geração de cada indicador.


## 📃 Solução Proposta
<a id="solucao"></a>
A solução da SquadTech consiste em uma plataforma centralizada de gerenciamento e rastreabilidade de dados, capaz de integrar diferentes fontes, controlar versões e registrar as transformações realizadas nas informações. A plataforma também realizará validação da qualidade dos dados, identificando inconsistências, duplicidades e dados incompletos, além de disponibilizar dashboards e relatórios. Assim, será possível acompanhar a origem dos dados, entender como os indicadores foram gerados e facilitar auditorias e tomadas de decisão.


## 🗃️ Backlog do Produto 
<a id="backlog"></a>

| **ID** | **RANK** | **USER STORY** | **PRIORIDADE** | **ESTIMATIVA** | **SPRINT** |
|:-:|:-:|:-:|:-:|:-:|:-:|
| US#01 | 1 | Como operador de dados, quero que o sistema calcule corretamente as áreas e as medidas dos imóveis de forma padronizada, para que todos os indicadores sejam gerados com precisão e da mesma maneira. | ALTA | 8 | 1 |
| US#02 | 2 | Como operador de dados, quero enviar os arquivos dos imóveis e das camadas ambientais, como o pacote .zip do CAR e a camada de embargos, em um único arquivo ou em vários, para que o sistema calcule os indicadores e os disponibilize para consulta. | ALTA | 13 | 1 |
| US#03 | 3 | Como operador de dados, quero consultar os arquivos já armazenados na plataforma e enviá-los para processamento, para reaproveitar dados sem precisar enviá-los de novo e gerar os indicadores a partir deles. | ALTA | 3 | 1 |
| US#04 | 4 | Como analista, quero saber quanto da área de cada imóvel está sobreposta a embargos ambientais federais, em hectares e em percentual, e quais embargos atingem o imóvel (indicador IAE), para identificar imóveis com restrições que pesam na fiscalização e na concessão de crédito. | ALTA | 8 | 1 |
| US#05 | 5 | Como analista, quero ver os imóveis e seus resultados em um mapa, para entender a situação de cada um visualmente e apresentá-la com clareza. | ALTA | 3 | 1 |
| US#32 | 6 | Como operador de dados, quero que o tratamento geoespacial dissolva as geometrias, padronize os atributos e meça as áreas em projeção equivalente, para que os indicadores usem dados corretos e consistentes. | ALTA | 8 | 2 |
| US#07 | 7 | Como operador de dados, quero que todo arquivo recebido seja guardado exatamente como chegou, com uma impressão digital (hash) e o registro de quem enviou, quando e para qual conjunto, para poder provar que o dado usado em um cálculo é idêntico ao que foi recebido. | ALTA | 3 | 2 |
| US#08  | 8 | Como operador de dados, quero que os registros reprovados na validação, por campos, tipos, domínios, duplicidades, áreas, coordenadas ou geometrias, sejam separados em quarentena com o motivo e que eu possa consultá-los, para corrigir os problemas sabendo exatamente o que foi rejeitado e por quê. | ALTA | 5 | 2 |
| US#09 | 9 | Como operador de dados, quero que os dados aprovados na validação sejam padronizados e recortados pelo limite do Paraná e guardados na zona tratada, com o registro de cada transformação aplicada, para que todo cálculo use um dado único, limpo e comparável. | ALTA | 5 |  2 |
| US#33 | 10 | Como operador de dados, quero acompanhar a trajetória de cada conjunto enviado pelas zonas do data lake (bruta → quarentena → tratada), com o registro de cada passagem e o que aconteceu em cada uma, para saber exatamente onde o dado está e por quais etapas já passou. | ALTA | 5 | 2 |
| US#06 | 11 | Como operador de dados, quero cadastrar as fontes de dados, como CAR, IBGE, INPE e IBAMA, e os seus conjuntos, informando esquema, sistema de referência, competência e cobertura, para que todo dado que entra no sistema tenha origem conhecida e documentada. | ALTA | 5 | 2 |
| US#14 | 12 | Como gestor, quero cadastrar as regras e os parâmetros de cálculo de cada indicador, como o percentual mínimo de Reserva Legal por bioma e as datas de corte do desmatamento, e manter o histórico de cada mudança, para que todo resultado registre exatamente qual regra e quais parâmetros foram usados.                                                      | ALTA | 3 | 2 |
| US#15 | 13 | Como gestor, quero conferir a qualidade de uma execução e, se ela estiver aprovada, publicar os resultados como uma versão que não pode mais ser alterada, para garantir que o número divulgado seja sempre o mesmo e possa ser reproduzido. | ALTA | 8 | 2 |
| US#16 | 14 | Como auditor, quero partir de um resultado publicado e chegar até os arquivos de origem, a execução do pipeline, as transformações e a regra de cálculo aplicada, para comprovar como aquele número foi produzido. | ALTA | 5 | 2 |
| US#12 | 15 | Como analista, quero saber quanto da área de cada imóvel está declarada como Reserva Legal em relação ao mínimo exigido para o seu bioma (20% na Mata Atlântica), com o déficit ou o excedente em hectares (indicador IRL), para avaliar se o imóvel está regular quanto à Reserva Legal.                                                                        | ALTA           | 5              |  2   |
| US#29  | 16       | Como operador de dados, quero trazer conjuntos de dados também por API (segunda forma de entrada, além do upload), para automatizar o recebimento de fontes atualizadas com frequência, como os focos de calor, que são diários.                                                                                                                                 | MÉDIA          | 5              |  2   |
| US#11  | 17       | Como gestor, quero acessar o portal, as APIs, o GeoDataLake e o Airflow pela internet, em ambiente de nuvem, para acompanhar e avaliar a solução a qualquer momento, sem depender do computador de alguém da equipe.                                                                                                                                             | ALTA           | 5              |  3   |
| US#10  | 18       | Como operador de dados, quero que o processamento de cada conjunto rode automaticamente em etapas encadeadas no Airflow (recebimento, validação, tratamento, cálculo, qualidade e publicação), registrando a situação, os erros e as reexecuções de cada etapa, para que todo dado siga sempre o mesmo caminho e eu possa reprocessar apenas a etapa que falhou. | ALTA           | 8              |  3   |
| US#13  | 19       | Como administrador, quero que o portal e as APIs só possam ser usados mediante login e que cada pessoa veja e faça apenas o que o seu perfil permite (administrador, operador de dados, analista, gestor ou auditor), para proteger os dados e impedir que alguém altere o que não é de sua responsabilidade.                                                    | ALTA           | 5              |  3   |
| US#17  | 20       | Como analista, quero consultar por API o catálogo, os dados, os indicadores, as versões, a qualidade, a linhagem e a situação das execuções, com documentação clara, para integrar os resultados a outros sistemas sem depender do portal.                                                                                                                       | ALTA           | 3              |  3   |
| US#18  | 21       | Como analista, quero ver os indicadores em uma tabela com filtros (município, imóvel, indicador e versão) e em gráficos, para comparar resultados e identificar rapidamente onde estão os problemas.                                                                                                                                                             | ALTA           | 5              |  3   |
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


##  🗓️ Cronograma das Sprints <a id="sprint"></a>
<a id="cronograma"></a>

|   Sprint    | Início |  Fim  | Documentação | Status | 
| :---------: | :----: | :---: | :----------: | :----: |
| Sprint 1 | 07/09  | 27/09 |  [Sprint 1](./Documentacao/Processo/Sprints/Sprint_1/README.md)           |  Concluida ✔️|
| Sprint 2 | 05/10  | 25/10 |  [Sprint 2](./Documentacao/Processo/Sprints/Sprint_2/README.md)           |  Em Andamento ⚙️|
| Sprint 3 | 02/10  | 22/11 |  [Sprint 3](./Documentacao/Processo/Sprints/Sprint_3/README.md)           |  Em Planejamento 📝|

---
## ⚙️ Tecnologias
<a id="tecnologias"></a>

<h4 align="center">
  <a href="https://www.oracle.com/java/"><img src="https://img.shields.io/badge/Java-000000?style=for-the-badge&logo=openjdk&logoColor=white"/></a>
  <a href="https://spring.io/projects/spring-boot"><img src="https://img.shields.io/badge/SpringBoot-000000?style=for-the-badge&logo=springboot&logoColor=white"/></a>
  <a href="https://vuejs.org/"><img src="https://img.shields.io/badge/Vue.js-000000?style=for-the-badge&logo=vue.js&logoColor=white"/></a>
  <a href="https://www.figma.com/"><img src="https://img.shields.io/badge/Figma-000000?style=for-the-badge&logo=figma&logoColor=white"/></a>
  <a href="https://github.com/"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"/></a>
  <a href="https://github.com/features/issues"><img src="https://img.shields.io/badge/GitHub%20Projects-000000?style=for-the-badge&logo=github&logoColor=white"/></a>
  <a href="https://code.visualstudio.com/"><img src="https://img.shields.io/badge/VS%20Code-000000?style=for-the-badge&logo=visual-studio-code&logoColor=white"/></a>
  <a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-000000?style=for-the-badge&logo=docker&logoColor=white"/></a>
  <a href="https://www.oracle.com/"><img src="https://img.shields.io/badge/Oracle-000000?style=for-the-badge&logo=oracle&logoColor=white"/></a>
  <a href="https://www.oracle.com/cloud/"><img src="https://img.shields.io/badge/Oracle%20Cloud-000000?style=for-the-badge&logo=oracle&logoColor=white"/></a>
</h4>


## 🏛️ Estrutura do Repositório <a id="estrutura"></a>
<a id="estrutura"></a>

- **`backend/`**:API responsável pelo gerenciamento das regras de negócio, processamento, validação e rastreabilidade dos dados.
- **`frontend/`**: Interface web para consulta das informações, acompanhamento dos dados e visualização dos indicadores.
- **`Documentacao/`**: Documentação técnica, requisitos, arquitetura e registros de evolução do projeto.

## 💾 Documentação <a id="docs"></a>
<a id="docs"></a>
- 🏁[DoD — Definition of Done](./Documentacao/Processo/Sprints/DoD_DoR.md)
- 📋[DoR — Definition of Ready](./Documentacao/Processo/Sprints/DoD_DoR.md)
- 🌿[Estratégia de Branch](./Documentacao/Estratégia_de_Branches.md)
- 📝[Padrões de Commits](./Documentacao/Padrões_de_Commits.md)
- 📚​[Configuração de Ambiente](./Documentacao/Configuração_de_Ambiente.md)
- 📖[Manual do Usuário](./Documentacao/Manual_do_Usuario.md)


## 👥 Equipe
<a id="equipe"></a>

| Foto | Nome | Função | GitHub | Linkedln |
|------|------|--------|--------|----------|
| <img src="https://github.com/user-attachments/assets/b30a5634-a2c4-41de-ae57-478f9692318f" width="50px"> | Jhonatan Rossi | Scrum Master | <a href="https://github.com/JhowRossii"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/jhonatan-miranda-a25813377"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/leonardo1022.png?size=50" width="50"> | Leonardo Amon | Product Owner | <a href="https://github.com/Leonardo1022"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/leonardo-amon/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/maria-oliveira.png?size=50" width="50"> | Maria Eduarda Oliveira | Dev. Team | <a href="https://github.com/maria-oliveira"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/maria-eduarda-t-m-oliveira-597666355/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/user-attachments/assets/0fa7866a-2f80-4a1b-a4d7-522381557605" width="50px"> | Guilherme Valim | Dev. Team | <a href="https://github.com/guivalim"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/guilherme-valim-bb3870375/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/user-attachments/assets/d5eec490-de3b-410b-ac6f-014942b78ef3"  width="50px">| Natanael Machado | Dev. Team | <a href="https://github.com/NatanaelSM"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/natanaelsm/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
