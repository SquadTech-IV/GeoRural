# Manual de Usuário — GeoRural

> ⚠️ **Documento em rascunho — aplicação ainda em desenvolvimento, sem deploy.** As telas e fluxos descritos aqui podem mudar antes do lançamento. Este manual será revisado conforme a evolução do projeto.

## 1. O que é o GeoRural

O GeoRural é um sistema que analisa e engloba arquivos geográficos de imóveis rurais e verifica diversos indicadores sobre ele para verificar sua conformidade legal e ambiental. Atualmente apenas um indicador (IAE) está disponível para análise juntamente com o imóvel.

## 2. Acessando o sistema

Atualmente a aplicação está disponível apenas em ambiente de desenvolvimento. O sistema não exige login: ao acessar, você já é direcionado à tela principal.

*(Esta seção será atualizada com o endereço de acesso assim que o sistema estiver publicado.)*

## 3. Enviando um imóvel

Na aba **"Ingestão de Fontes"**, você pode enviar o arquivo geográfico do imóvel rural.

**Formatos aceitos:**
- Shapefile (`.zip`)
- GeoPackage (`.gpkg`)
- GeoJSON

**Como enviar:**
1. Arraste o arquivo para a área indicada, ou clique nela para selecionar o arquivo do seu computador.
2. Envie um arquivo por vez, referente a um único imóvel ou aos embargos (necessário para o IAE).
3. O sistema identifica automaticamente a que o arquivo se refere — não é necessário indicar isso manualmente. *(No momento, apenas dados de embargos ambientais e imóveis rurais são aceitos.)*

Após o envio, o arquivo aparece na lista **"Arquivos recentes"**, abaixo da área de upload, com a situação atual (por exemplo, "Aguardando").

## 4. Acompanhando o processamento

Após o envio, uma janela mostra o andamento do processamento em etapas:

- Validando geometrias
- Reprojetando para área equivalente
- Calculando interseções e áreas
- Calculando o IAE

Durante esse processo, não é necessário (nem possível) fazer nada — apenas aguarde a conclusão.

### Se ocorrer um erro

Caso alguma etapa falhe, o sistema exibe uma mensagem genérica do erro. Não há diagnóstico detalhado disponível para o usuário nesse momento.

**O que fazer:**
1. Reinicie o processo enviando o arquivo novamente.

## 5. Consultando imóveis processados

Ao concluir o processamento, você é direcionado à aba **"Verificar Dados Existentes"**, onde aparece a lista de imóveis já registrados no sistema, com:

- Nome do arquivo
- Data de cadastro
- Botão para **visualizar** o imóvel no mapa
- Botão para **reprocessar** (recalcular) o imóvel
- Status do imóvel

## 6. Visualizando o imóvel no mapa

Ao clicar no ícone de visualização, você é levado a uma tela de mapa com:

- O limite do imóvel analisado (contorno roxo)
- As áreas de embargo próximas ao imóvel (quando houver sobreposição)
- Um painel lateral com:
  - Identificador do imóvel (CAR)
  - Área total (em hectares)
  - Município
  - **IAE — Adequação a Embargos Ambientais**: percentual e quantidade em hectares da área do imóvel que se sobrepõe a embargos ambientais

É possível interagir com o mapa (zoom e navegação), mas não há outras ações disponíveis além da visualização desse ou outro imóvel.

## 7. Recalculando um imóvel

Novos embargos ambientais podem ser cadastrados no sistema com o tempo, o que pode alterar o resultado de um imóvel já processado, para isso é feito o recálculo.

Para recalcular, clique no ícone de "Processar Arquivo" ao lado do imóvel desejado, na aba "Verificar Dados Existentes".

## 8. Limites conhecidos

- Tamanho máximo de arquivo: 300MB.
- No momento, apenas dados relacionados a embargos ambientais e imóveis são processados pelo sistema.
- Não há sistema de notificação para novos embargos cadastrados, mas em caso de recalculo o sistema considera o conjunto de embargos mais recente registrado.
- Não há diagnóstico detalhado em caso de erro de processamento.