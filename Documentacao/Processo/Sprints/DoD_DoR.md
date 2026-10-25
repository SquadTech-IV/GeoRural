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
- `[PENDENTE]` Exclusão de fonte: o cliente confirmou que há cenário de exclusão. Definir se é exclusão lógica (preservando versões já publicadas) ou física, e o efeito sobre indicadores publicados que dependem da fonte.
- `[PENDENTE]` Quem pode cadastrar (operador, gestor ou ambos) — depende do papel do operador, ainda sem resposta do cliente.

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

---

# 📋 DoR — Definition of Ready

- Título, descrição e objetivos claros
- Valor agregado ao cliente
- Critérios de aceitação definidos
- Estimativa, prioridade e rank estabelecidos junto com a equipe
