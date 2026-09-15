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

| Rank | Prioridade | User Story | Estimativa | Sprint |
|------|------------|------------|------------|--------|
| 1 | Alta | Como gestor, quero uma ferramenta que faça operações geoespaciais (reprojeção, validação/dissolução de geometria, cálculo de área) para padronizar e facilitar a realização dos cálculos de cada indicador | 8 | 1 |
| 2 | Alta | Como gestor, quero armazenar os dados em categorias de bruta, quarentena, tratada e publicada para garantir que os dados usados foram revisados e tratados de antemão | 13 | 1 |
| 3 | Alta | Como analista, quero consultar o IRL do imóvel, para avaliar sua conformidade com a Reserva Legal | 3 | 1 |
| 4 | Alta | Como analista, quero consultar o ISAP do imóvel, para avaliar sua conformidade com unidades de conservação, terras indígenas, quilombolas e florestas públicas | 8 | 1 |
| 5 | Alta | Como analista, quero consultar o IAE do imóvel, para avaliar sua conformidade com a embargos ambientais | 3 | 1 |
| 6 | Alta | Como gestor, quero garantir que resultados de indicadores validados possam ser publicados, sem possibilidade de alteração, para manter a integridade e versionamento deles | 11 | 1 |
| 7 | Alta | Como auditor, quero visualizar as fontes e conjuntos utilizados, cálculos e regras aplicadas num resultado para garantir sua integridade | 5 | 1 |
| 8 | Alta | Como gestor, quero cadastrar fontes de dados para assegurar a formação de indicadores | 5 | 1 |
| 9 | Média | Como administrador, quero separar o sistema por níveis de acesso e ações entre tipos de usuários (administrador, operador de dados, gestor, analista e auditor) para assegurar a integridade do sistema | 5 | 2 |
| 10 | Média | Como auditor, quero comparar duas versões publicadas de um mesmo indicador para identificar o que mudou entre elas | 5 | 2 |
| 11 | Média | Como analista, quero ter acesso aos dados vigentes do sistema por API para conseguir fazer consultas aos dados de forma independente ao portal web | 5 | 2 |
| 12 | Média | Como utilizador dos dados, quero que os dados da API venham em formato CSV, JSON e GeoJSON para utilizá-lo em outras aplicações sem a necessidade de tratar os dados | 3 | 2 |
| 13 | Média | Como gestor, quero pipelines de dados para configurá-los no Airflow | 8 | 3 |
| 14 | Média | Como analista, quero consultar o IFC do imóvel, para identificar regiões com focos de incêndios | 5 | 3 |
| 15 | Baixa | Como gestor, quero garantir a segurança do acesso a API com chave de acesso, histórico de injeções e requisições para monitorar por quem e como a API é acessada | 11 | 3 |
| 16 | Baixa | Como analista, quero consultar o ICV do imóvel, para monitorar seu estado ambiental ao longo do tempo | 3 | 3 |
| 17 | Baixa | Como analista, quero consultar o IAPP do imóvel, para monitorar seu estado ambiental ao longo do tempo | 5 | 3 |
| 18 | Baixa | Como analista, quero consultar o IDesmat do imóvel, para monitorar seu estado ambiental ao longo do tempo | 5 | 3 |
| 19 | Baixa | Como gestor, quero criar indicadores customizados para reaproveitar e ampliar a atuação da aplicação | 11 | 3 |


##  🗓️ Cronograma das Sprints <a id="sprint"></a>
<a id="cronograma"></a>

|   Sprint    | Início |  Fim  | Documentação | Status | 
| :---------: | :----: | :---: | :----------: | :----: |
| Sprint 1 | 07/09  | 27/09 |  [Sprint 1](./Documentacao/Processo/Sprints/Sprint_1/README.md)           |  Em Andamento ⚙️|
| Sprint 2 | 05/10  | 25/10 |  [Sprint 2](./Documentacao/Processo/Sprints/Sprint_2/README.md)           |  Em Planejamento 📝|
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
- 🏁 DoD — Definition of Done
- 📋 DoR — Definition of Ready
- 🌿 Estratégia de Branch
- 📝 Estratégia de Commits
- 📖 Manual do Usuário


## 👥 Equipe
<a id="equipe"></a>

| Foto | Nome | Função | GitHub | Linkedln |
|------|------|--------|--------|----------|
| <img src="https://github.com/user-attachments/assets/b30a5634-a2c4-41de-ae57-478f9692318f" width="50px"> | Jhonatan Rossi | Scrum Master | <a href="https://github.com/JhowRossii"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/jhonatan-miranda-a25813377"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/leonardo1022.png?size=50" width="50"> | Leonardo Amon | Product Owner | <a href="https://github.com/Leonardo1022"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/leonardo-amon/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/maria-oliveira.png?size=50" width="50"> | Maria Eduarda Oliveira | Dev. Team | <a href="https://github.com/maria-oliveira"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/maria-eduarda-t-m-oliveira-597666355/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/user-attachments/assets/0fa7866a-2f80-4a1b-a4d7-522381557605" width="50px"> | Guilherme Valim | Dev. Team | <a href="https://github.com/guivalim"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/guilherme-valim-bb3870375/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
| <img src="https://github.com/user-attachments/assets/d5eec490-de3b-410b-ac6f-014942b78ef3"  width="50px">| Natanael Machado | Dev. Team | <a href="https://github.com/NatanaelSM"><img src="https://img.shields.io/badge/GitHub-000000?style=for-the-badge&logo=github&logoColor=white"></a> | <a href="https://www.linkedin.com/in/natanaelsm/"><img src="https://img.shields.io/badge/LinkedIn-000000?style=for-the-badge&logo=linkedin&logoColor=white"></a> |
