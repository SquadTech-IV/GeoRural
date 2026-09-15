## 🎯Meta da Sprint

Aplicação capaz de fazer o cálculo e visualização apropriada do indicador IRL com o tratamento de dados vindos de fontes seletas para usá-los em cálculos. As fontes poderão ser cadastradas diretamente e o banco de dados hospedado em cloud. User Stories: US01, US02 e US03


## Sprint backlog

| Rank | Prioridade | User Story | Estimativa | Sprint | ID |
|------|------------|------------|------------|--------|----|
| 1 | Alta | Como gestor, quero uma ferramenta que faça operações geoespaciais (reprojeção, validação/dissolução de geometria, cálculo de área) para padronizar e facilitar a realização dos cálculos de cada indicador | 8 | 1 | US01 |
| 2 | Alta | Como gestor, quero armazenar os dados em categorias de bruta, quarentena, tratada e publicada para garantir que os dados usados foram revisados e tratados de antemão | 13 | 1 | US02 |
| 3 | Alta | Como analista, quero consultar o IRL do imóvel, para avaliar sua conformidade com a Reserva Legal | 3 | 1 | US03 |
| 4 | Alta | Como analista, quero consultar o ISAP do imóvel, para avaliar sua conformidade com unidades de conservação, terras indígenas, quilombolas e florestas públicas | 8 | 1 | US04 |
| 5 | Alta | Como analista, quero consultar o IAE do imóvel, para avaliar sua conformidade com a embargos ambientais | 3 | 1 | US05 |
| 6 | Alta | Como gestor, quero garantir que resultados de indicadores validados possam ser publicados, sem possibilidade de alteração, para manter a integridade e versionamento deles | 11 | 1 | US06 |
| 7 | Alta | Como auditor, quero visualizar as fontes e conjuntos utilizados, cálculos e regras aplicadas num resultado para garantir sua integridade | 5 | 1 | US07 |
| 8 | Alta | Como gestor, quero cadastrar fontes de dados para assegurar a formação de indicadores | 5 | 1 | US08 |

## DoD

### US01
- Reprojeta qualquer geometria de entrada para uma projeção equivalente (equal-area) adequada ao território do Paraná, antes de qualquer cálculo de área;
- Valida geometrias de entrada (auto-interseção, anéis inválidos, vértices duplicados) e corrige automaticamente quando possível;
- Expõe uma função reaproveitável de cruzamento (interseção) entre duas camadas, retornando a geometria resultante e sua área em m² e hectares;
- Erros de geometria não corrigíveis automaticamente são registrados e enviados à fila de rejeitados/quarentena, não interrompem o processamento de outros registros.

### US02
- Bruta: Dados não tratados vindos de fontes, mantendo seu formato e valor comparado a fonte de origem;
- Quarentena: Dados rejeitados (necessário de motivo e responsável pela rejeição);
- Tratada: Dados em formato padrão de um SRC para poder ser usado em cálculos de indicadores;
- Publicada: Dados que foram aceitos de forma manual, são os dados que serão usados pela aplicação e API;
- Deve estar hospedado num ambiente em nuvem.

### US03
- Calcula: área de RL declarada ÷ área do imóvel;
- Compara o percentual obtido ao mínimo de Reserva Legal do bioma (20% para Mata Atlântica, fora da Amazônia Legal — parâmetro do Paraná);
-  Resultado exibido em % e em hectares;
- Exibe déficit ou excedente de RL em hectares, separadamente do percentual;
- Indicador rastreável até a versão da fonte (RL declarada + limite de bioma) usada no cálculo;
- Consulta responde em até 3 segundos.

### US04
- Calcula sobreposição do imóvel com cada uma das 4 categorias de área protegida, individualmente: unidades de conservação (ICMBio/MMA), terras indígenas (FUNAI), territórios quilombolas (INCRA), florestas públicas (SFB);
- Exibe o resultado discriminado por categoria (não apenas um número agregado único), em % e em hectares;
- Indica claramente quando não há sobreposição em uma ou mais categorias (não omite a categoria, mostra "0%");
- Indicador rastreável até a versão de cada uma das 4 fontes usadas no cálculo daquele imóvel;
- Consulta responde em até 3 segundos.

### US05
- Calcula sobreposição do imóvel com embargos ambientais federais (fonte IBAMA/ICMBio);
- Resultado exibido em % e em hectares;
- Indicador rastreável até a versão da fonte de embargos usada no cálculo;
- Consulta responde em até 3 segundos.

### US06
- Ao publicar, o sistema gera uma versão imutável do conjunto de indicadores calculados, identificada por hash, data/hora, fonte(s), competência e regra de cálculo aplicada;
- Uma vez publicada, a versão não pode ser editada, qualquer correção gera uma nova versão;
- Versão publicada substitui a "versão vigente" nas consultas por padrão, mantendo as versões anteriores acessíveis para consulta e comparação;
- Publicação deve ser feita de forma manual pelo usuário responsável.

### US07
- Para um resultado publicado, exibe: fonte(s) e versão(ões) exata(s) usada(s), regra/fórmula de cálculo aplicada, execução (pipeline) que gerou o resultado e data e responsável pela publicação;
- Exibe registros rejeitados (quarentena) associados a execução, com o motivo da rejeição;
- Informação é somente leitura para o auditor (não pode alterar nenhum dado a partir dessa tela).
- Diferencia-se da consulta de catálogo do analista: esta story mostra a linhagem de um **resultado específico já publicado**, não a lista geral de fontes cadastradas no sistema.

### US08
- Cadastra um conjunto vinculado a uma fonte, com formato de origem aceito (Shapefile, GeoPackage, GeoJSON, GeoTIFF, CSV, conforme a fonte);
- Sistema preserva o arquivo original na zona bruta com hash e metadados de origem;
- Sistema registra o autor do cadastro e data;
- Gestor visualiza e organiza as quatro zonas do GeoDataLake (bruta, tratada, publicada, quarentena) associadas a cada conjunto.

## DoR

- Título, descrição e objetivos claros
- Valor agregado ao cliente
- Critérios de aceitação definidos
- Estimativa, prioridade e rank estabelecidos junto com a equipe