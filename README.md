
---

# Projeto: Análise de Dados do Spotify para Decisões Estratégicas na Indústria Musical

## Visão Geral

No contexto da indústria musical altamente competitiva e em constante evolução, a capacidade de tomar decisões estratégicas baseadas em dados se tornou um diferencial crucial. Este projeto tem como objetivo explorar um extenso conjunto de dados do Spotify de 2023 para validar hipóteses relacionadas aos fatores que influenciam o sucesso de uma música em termos de streams na plataforma.

## Hipóteses

Durante o projeto, identificamos as seguintes hipóteses a serem validadas através da análise de dados:

1. Músicas com BPM (Batidas Por Minuto) mais altos têm mais sucesso em termos de número de streams no Spotify.
2. As músicas mais populares no ranking do Spotify também apresentam um comportamento semelhante em outras plataformas, como a Deezer.
3. A presença de uma música em um maior número de playlists está correlacionada com um maior número de streams.
4. Artistas com um maior número de músicas no Spotify têm mais streams.
5. Características específicas da música influenciam o sucesso em termos de número de streams no Spotify.

## Tecnologias Utilizadas

Para realizar esta análise, utilizamos as seguintes tecnologias:

- **BigQuery**: Para armazenamento e operações iniciais com dados.
- **Python**: Para manipulação de dados utilizando Pandas.
- **Power BI**: Para análise visual e criação de dashboards interativos.

## Detalhamento do Projeto

### Importação e Preparação de Dados

Iniciamos o projeto importando os dados brutos do Spotify e realizando operações de limpeza e preparação utilizando Pandas em conjunto com BigQuery para garantir a integridade dos dados.

#### Importação de Dados com BigQuery e Pandas

Utilizamos BigQuery para importar os dados e Pandas para manipulação adicional:

```python
from google.cloud import bigquery
import pandas as pd

# Configuração do cliente BigQuery
client = bigquery.Client()

# Query SQL para importar dados
query = """
SELECT *
FROM `project.dataset.spotify_raw_data`
"""

# Executar a consulta e salvar os resultados em um DataFrame Pandas
df_spotify = client.query(query).to_dataframe()
```

#### Limpeza de Dados com BigQuery e Pandas

Realizamos a limpeza de dados utilizando Pandas para identificar e gerenciar valores nulos, duplicados e discrepantes:

##### Identificar e Gerenciar Valores Nulos

```sql
# Contagem de valores nulos por coluna
SELECT
  COUNTIF(column_name IS NULL) AS null_count,
  COUNT(*) AS total_rows
FROM
  dataset.spotify_data;
```

##### Identificar e Gerenciar Valores Duplicados

```sql
# Remover registros duplicados
#standardSQL
CREATE OR REPLACE TABLE dataset.spotify_data AS
SELECT
  DISTINCT *
FROM
  dataset.spotify_data;
```

##### Identificar e Gerenciar Dados Fora do Alcance da Análise

```sql
# Exemplo de consulta para gerenciar dados fora do alcance
# Remover registros com stream_count negativo ou muito alto
#standardSQL
CREATE OR REPLACE TABLE dataset.spotify_data AS
SELECT *
FROM dataset.spotify_data
WHERE stream_count >= 0 AND stream_count <= 1000000;
```

##### Verificar e Alterar Tipo de Dado

```sql
# Exemplo de consulta para verificar e alterar tipo de dado
#standardSQL
SELECT
  SAFE_CAST(column_name AS INT64) AS column_name_int
FROM
  dataset.spotify_data;
```

### Análise Visual e Criação de Dashboards (Power BI)

Utilizamos o Power BI para visualizar e explorar os dados de forma interativa. Criamos dashboards personalizados para analisar as hipóteses levantadas e apresentar insights estratégicos para a gravadora.

- **Exploração Visual**: Criamos gráficos e visualizações para entender melhor os padrões de comportamento das músicas no Spotify.

- **Criação de Dashboards**: Consolidamos as análises em dashboards interativos, permitindo uma visualização clara e detalhada dos dados.

## Conclusão

Este projeto não apenas validou hipóteses cruciais para a gravadora, mas também demonstrou a importância de utilizar dados de forma estratégica na indústria musical. As análises realizadas com BigQuery e Pandas garantiram a preparação adequada dos dados, enquanto o Power BI facilitou a exploração visual e a apresentação dos resultados de maneira eficaz.

---
