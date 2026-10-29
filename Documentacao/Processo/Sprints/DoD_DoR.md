# 🏁 DoD — Definition of Done

## 📝Sprint 1

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

## 📝Sprint 2

### US#06

**Como operador de dados, quero cadastrar as fontes de dados, como CAR, IBGE, INPE e IBAMA, e os seus conjuntos, informando esquema, sistema de referência, competência e cobertura, para que todo dado que entra no sistema tenha origem conhecida e documentada.**

- Cadastra uma fonte informando nome e órgão de origem (ex.: CAR, IBGE, INPE, IBAMA).
- Cadastra um conjunto vinculado a uma fonte, com os campos obrigatórios: esquema, sistema de referência (ex.: SIRGAS 2000, EPSG:4674), competência e cobertura.
- O sistema não permite salvar conjunto sem fonte vinculada nem com campo obrigatório vazio, e informa qual campo está faltando.
- A listagem exibe todas as fontes e seus conjuntos com os metadados cadastrados.
- O sistema não aceita recebimento de arquivo (US#07, US#29) para conjunto que não esteja cadastrado.
---

### US#07

**Como operador de dados, quero que todo arquivo recebido seja guardado exatamente como chegou, com uma impressão digital (hash) e o registro de quem enviou, quando e para qual conjunto, para poder provar que o dado usado em um cálculo é idêntico ao que foi recebido.**

- O arquivo é armazenado na zona bruta sem nenhuma alteração de conteúdo.
- O sistema calcula o hash do arquivo no recebimento, com algoritmo definido e documentado pelo time (SHA-256), e o armazena junto ao registro.
- Recalcular o hash do arquivo armazenado resulta no mesmo valor registrado.
- O registro contém: usuário que enviou, data/hora do envio, conjunto de destino, nome original e tamanho do arquivo.
- Arquivo na zona bruta nunca é sobrescrito, editado ou apagado por processamentos posteriores.
- Envio sem conjunto vinculado é rejeitado com mensagem de erro.
- Formatos aceitos: shapefile, GeoJSON, GeoPackage, CSV e GeoTIFF.
- Ao receber um arquivo com hash idêntico a um já armazenado para o mesmo conjunto o sistema deve bloquear.

---

### US#08

**Como operador de dados, quero que os registros reprovados na validação, por campos, tipos, domínios, duplicidades, áreas, coordenadas ou geometrias, sejam separados em quarentena com o motivo e que eu possa consultá-los, para corrigir os problemas sabendo exatamente o que foi rejeitado e por quê.**

- Registro reprovado vai para a zona de quarentena e **não** segue para a etapa de tratamento.
- Cada registro em quarentena guarda o motivo da rejeição (qual regra falhou) e a referência ao arquivo bruto de origem.
- Registro aprovado segue para a etapa de tratamento.
- A rejeição de um registro não interrompe o processamento dos demais do mesmo arquivo.
- O operador consulta a quarentena filtrando por conjunto e por execução e vê, para cada registro, o motivo da rejeição.
- Cada execução exibe a contagem de registros recebidos, aprovados e rejeitados, e a soma de aprovados e rejeitados deve ser igual ao total recebido.

---

### US#09

**Como operador de dados, quero que os dados aprovados na validação sejam padronizados e recortados pelo limite do Paraná e guardados na zona tratada, com o registro de cada transformação aplicada, para que todo cálculo use um dado único, limpo e comparável.**

- A validação verifica, por registro: campos obrigatórios, tipos de dados, faixa de valores, duplicidades, áreas, coordenadas e geometrias.
- Os dados são recortados pelo limite estadual do Paraná (IBGE) antes de qualquer cálculo.
- Cada transformação aplicada é registrada com: tipo da transformação, parâmetros usados, data/hora, execução e referência de entrada e saída.
- Cada dado tratado mantém vínculo com o arquivo bruto de origem via hash.
- O processamento da zona tratada não altera nem sobrescreve nada na zona bruta.

---

### US#12

**Como analista, quero saber quanto da área de cada imóvel está declarada como Reserva Legal em relação ao mínimo exigido para o seu bioma (20% na Mata Atlântica), com o déficit ou o excedente em hectares (indicador IRL), para avaliar se o imóvel está regular quanto à Reserva Legal.**

- Calcula: área de Reserva Legal declarada ÷ área do imóvel, usando as geometrias da zona tratada (US#32, US#09).
- O mínimo de comparação vem do parâmetro cadastrado na US#14, não de valor fixo no código.
- Exibe o percentual de Reserva Legal e o déficit ou excedente em hectares, separadamente.
- O resultado é exibido em % e em hectares.
- O resultado registra a regra e a versão dos parâmetros usados (US#14) e é rastreável até a versão dos dados de origem.
- Imóvel sem Reserva Legal declarada tem resultado definido (0% e déficit igual ao mínimo exigido), sem erro nem valor em branco.
- Usar a camada de biomas do IBGE para determinar o bioma por imóvel.

---

### US#14

**Como gestor, quero cadastrar as regras e os parâmetros de cálculo de cada indicador, como o percentual mínimo de Reserva Legal por bioma e as datas de corte do desmatamento, e manter o histórico de cada mudança, para que todo resultado registre exatamente qual regra e quais parâmetros foram usados.**

- Cadastra parâmetros de cálculo por indicador, incluindo ao menos: mínimo de Reserva Legal por bioma (20% para Mata Atlântica, fora da Amazônia Legal) e as datas de corte do desmatamento (22/07/2008, 31/07/2019 e 31/12/2020).
- Alterar um parâmetro **não sobrescreve** o valor anterior: gera uma nova vigência, mantendo o histórico.
- O histórico de cada parâmetro mostra valor anterior, valor novo, responsável, data/hora e vigência.
- Todo resultado de indicador registra o identificador da versão de cada parâmetro usado no cálculo.

---

### US#15

**Como gestor, quero conferir a qualidade de uma execução e, se ela estiver aprovada, publicar os resultados como uma versão que não pode mais ser alterada, para garantir que o número divulgado seja sempre o mesmo e possa ser reproduzido.**

- O gestor consulta as métricas de qualidade de uma execução: registros recebidos, aprovados, rejeitados e percentual de aprovação.
- Somente uma execução aprovada pode ser publicada; execução não aprovada tem a publicação bloqueada.
- A publicação gera uma versão identificada por hash, com fonte(s), competência, execução, parâmetros e regras aplicadas.
- Versão publicada é imutável: qualquer tentativa de alterar ou excluir seus resultados é bloqueada, inclusive diretamente no banco (ex.: restrição ou gatilho), e registrada.
- Correção de um resultado gera uma **nova versão**; as versões anteriores continuam consultáveis.
- A versão vigente é identificada como tal.
- Recalcular o hash de uma versão publicada resulta no valor registrado na publicação.

---

### US#16

**Como auditor, quero partir de um resultado publicado e chegar até os arquivos de origem, a execução do pipeline, as transformações e a regra de cálculo aplicada, para comprovar como aquele número foi produzido.**

- A partir de um resultado de uma versão publicada, o auditor navega até: os arquivos brutos de origem (nome, hash, quem enviou e quando), a execução do pipeline (etapas, situação e registros rejeitados), as transformações aplicadas (US#09) e a regra e os parâmetros de cálculo (US#14).
- Se algum elo não puder ser resolvido (ex.: arquivo de origem sem hash registrado), o sistema sinaliza a lacuna em vez de omitir.
- Teste de reconstituição: dada uma versão publicada, é possível identificar o conjunto exato de arquivos de origem usado no cálculo.
- A consulta é somente leitura, o auditor não consegue alterar nenhum dado a partir dela.

---

### US#29

**Como operador de dados, quero trazer conjuntos de dados também por API (segunda forma de entrada, além do upload), para automatizar o recebimento de fontes atualizadas com frequência, como os focos de calor, que são diários.**

- Existe um endpoint REST que recebe o arquivo e o identificador do conjunto de destino.
- Arquivos recebidos pela API seguem as mesmas regras da US#07: armazenados na zona bruta, com hash e registro de quem enviou, quando e para qual conjunto.
- A API retorna códigos de resposta distintos para: sucesso, conjunto inexistente, arquivo inválido/formato não aceito e erro interno.
- O endpoint está documentado em OpenAPI/Swagger.
- A funcionalidade é demonstrada com uma fonte simulada (o desafio prevê "uma fonte por API simulada").

---

### US#32

**Como operador de dados, quero que o tratamento geoespacial dissolva as geometrias, padronize os atributos e meça as áreas em projeção equivalente, para que os indicadores usem dados corretos e consistentes.**

- As geometrias são reprojetadas para uma projeção equivalente (que preserva área) antes de qualquer cálculo de área; a projeção escolhida é documentada na memória de cálculo.
- Geometrias inválidas (auto-interseção, anéis inválidos, vértices duplicados) são corrigidas automaticamente quando possível; as não corrigíveis são enviadas à quarentena com o motivo.
- Fragmentos da mesma feição (ex.: várias camadas de Reserva Legal de um mesmo imóvel) são dissolvidos em uma geometria única antes do cruzamento.
- A área é calculada em hectares sobre a geometria já reprojetada e dissolvida.
- A área calculada de pelo menos um imóvel de referência é conferida contra um valor conhecido, dentro de uma tolerância definida e documentada pelo time.
- A soma das áreas das partes é igual à área do todo, dentro da mesma tolerância.
- Atributos padronizados (nomes de campo e tipos) conforme o esquema do conjunto cadastrado.
- A mesma entrada produz sempre a mesma saída.

---

### US#33

**Como operador de dados, quero acompanhar a trajetória de cada conjunto enviado pelas zonas do data lake (bruta → quarentena → tratada), com o registro de cada passagem e o que aconteceu em cada uma, para saber exatamente onde o dado está e por quais etapas já passou.**

- Para cada arquivo/conjunto enviado, o operador consulta a zona em que o dado se encontra e o histórico de passagens por zona.
- Cada passagem registra: zona de origem e destino, data/hora, resultado e quantidade de registros.
- Registros que foram para a quarentena aparecem no histórico com a quantidade rejeitada.
- A consulta é somente leitura.

## 📝Sprint 3

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

# 📋 DoR — Definition of Ready

- Título, descrição e objetivos claros
- Valor agregado ao cliente
- Critérios de aceitação definidos
- Estimativa, prioridade e rank estabelecidos junto com a equipe
