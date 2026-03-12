# Medallion Analytics Spark
#### Descrição do Projeto
Este projeto implementa um pipeline ETL/Analytics utilizando Apache Spark, seguindo a Medallion Architecture (Bronze → Silver → Gold). 
O objetivo é processar dados de vendas, integrar diferentes dimensões (Cliente, Produto, Região, Tempo) e disponibilizar os dados para dashboards de análise.

<img width="1110" height="648" alt="pipeline1" src="https://github.com/user-attachments/assets/f9037c6d-0541-4236-b603-c37b77d6e2e4" />

### Estrutura do Projeto
    analytics-spark/
    │
    ├─ Dockerfile.spark          # Imagem customizada do Spark com Python e Jupyter
    ├─ docker-compose.yml        # Cluster Spark + MinIO + Postgres
    ├─ requirements.txt          # Dependências Python
    ├─ config/                   # Configurações do Spark
    │  └─ spark/jars/            # Jars necessários (não versionar >100MB)
    ├─ data/                     # Datasets de exemplo ou placeholders
    └─ notebooks/                # Notebooks Bronze, Silver, Gold e CDC
  
  
### Tecnologias Usadas

    Apache Spark 3.5.1
    Python 3
    Delta Lake / Delta-Spark
    MinIO (Data Lake para armazenar dimensões e tabelas fato)
    PostgreSQL (banco de dimensões e fatos)
    Docker / Docker Compose com 2 Spark Workers para paralelismo e escalabilidade
    Jupyter Notebook / JupyterLab
    Bibliotecas Python: pandas, pyarrow, delta-spark, sqlalchemy, boto3, requests, deltalake, pytest, psycopg2-binary

### Pipeline Bronze → Silver → Gold

    Bronze: ingestão de dados brutos para o MinIO.
    Silver: limpeza, transformação e integração de dimensões (Cliente, Produto, Região, Tempo) armazenadas em Delta Lake no MinIO.
    Gold: criação da tabela fato fato_vendas, juntando todas as dimensões, com métricas como quantidade, preço unitário e total de vendas, também em Delta Lake no MinIO.
    CDC Notebook: tratamento de mudanças incrementais para atualização contínua.
      
### Modelagem de Dados Dimensional
  <img width="1322" height="812" alt="img_modelagem049" src="https://github.com/user-attachments/assets/e271743f-0b97-4d6b-8a18-542fbc4ef8ca" />


### Dashboard / Métricas
  <img width="1453" height="782" alt="dashbo_vendas1" src="https://github.com/user-attachments/assets/b5a8c367-c234-465d-8033-bc77cd9439da" />
   
  ### Métricas e Gráficos do Dashboard

    - Faturamento total – mostra a receita por período.
    - Ticket médio – acompanha a média de valor por venda.
    - Produto mais vendido – destaca os itens com maior quantidade vendida.
    - Quantidade vendida – exibe volumes de vendas por produto. 
    - Desempenho por marca – compara vendas entre diferentes marcas.
    - Desempenho por região – mostra vendas distribuídas geograficamente.
    - Desempenho ao longo do período – gráficos combinados de linhas e colunas para analisar quantidade e faturamento juntos.


    
### Como Rodar o Projeto

    Build da imagem Spark:
      cmd: docker build -f Dockerfile.spark -t custom-spark:3.5.1 .
    
    Subir o cluster (Spark Master + 2 Workers + MinIO + Postgres):
      cmd: docker-compose up -d



