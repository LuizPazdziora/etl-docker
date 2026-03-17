ETL Pipeline com Docker

Projeto de pipeline ETL (Extract, Transform, Load) desenvolvido em Python para extração de dados da API Open Brewery DB.

A aplicação foi estruturada de forma modular, separando cada etapa do processo ETL em módulos independentes. O projeto também foi preparado para execução em ambiente containerizado utilizando Docker.

O objetivo deste projeto é demonstrar a construção de uma pipeline de ingestão de dados organizada, escalável e fácil de manter.

Arquitetura da Pipeline

O fluxo de dados segue o modelo clássico de pipelines de engenharia de dados:

API → Extract → Transform → Load → Database

Cada etapa da pipeline possui um módulo específico dentro da pasta src.

Estrutura do Projeto
etl-docker/
│
├── src/
│   ├── __init__.py
│   ├── config.py
│   ├── extract.py
│   ├── transform.py
│   └── load.py
│
├── main.py
├── Dockerfile
├── docker-compose.yml
├── .gitignore
├── .env
└── README.md



Descrição dos Arquivos


src/

A pasta src contém os módulos responsáveis pela implementação das etapas da pipeline ETL.

__init__.py

Arquivo responsável por definir a pasta src como um pacote Python, permitindo que seus módulos sejam importados em outros arquivos do projeto.

config.py

Responsável por centralizar todas as configurações da aplicação.

Esse módulo carrega as variáveis de ambiente e disponibiliza os parâmetros utilizados pela pipeline, como:

URL da API

número de registros por página

limite de páginas a serem consultadas

configurações de banco de dados

Centralizar as configurações facilita a manutenção e evita duplicação de código.

extract.py

Implementa a etapa de extração de dados (Extract) da pipeline.

Esse módulo é responsável por:

realizar requisições à API

lidar com paginação de resultados

tratar erros de requisição

consolidar os dados extraídos

O processo também inclui tentativas automáticas de requisição (retry) em caso de falha na comunicação com a API.

transform.py

Responsável pela etapa de transformação dos dados (Transform).

Nesta fase os dados extraídos podem passar por diversos processos, como:

limpeza de dados

padronização de campos

remoção de valores inconsistentes

reorganização da estrutura dos registros

Essa etapa prepara os dados para serem armazenados ou analisados.

load.py

Implementa a etapa de carga dos dados (Load).

Esse módulo será responsável por armazenar os dados transformados em um sistema de persistência, como um banco de dados.

Essa etapa representa o destino final da pipeline ETL.

Arquivos da raiz do projeto
main.py

Arquivo principal responsável por orquestrar a execução da pipeline ETL.

Ele controla a sequência de execução das etapas do processo:

Extração de dados

Transformação dos dados

Carregamento dos dados

Dockerfile

Arquivo responsável por definir a imagem Docker da aplicação.

Ele descreve o ambiente necessário para execução do projeto, incluindo dependências e arquivos necessários.

docker-compose.yml

Arquivo utilizado para orquestrar os containers da aplicação.

Com o Docker Compose é possível iniciar toda a infraestrutura necessária com um único comando.

.gitignore

Arquivo responsável por definir quais arquivos não devem ser versionados no repositório, como:

arquivos de variáveis de ambiente

ambientes virtuais

caches do Python

arquivos temporários

.env

Arquivo que contém variáveis de ambiente utilizadas pelo projeto, permitindo configurar a aplicação sem alterar o código.

Essas variáveis podem incluir:

endereço da API utilizada

parâmetros de paginação

configurações de conexão com banco de dados

README.md

Arquivo de documentação do projeto.

Ele apresenta o objetivo do projeto, arquitetura da pipeline, estrutura dos arquivos e instruções para execução.

Tecnologias Utilizadas

Python

Requests

Docker

Docker Compose

API REST