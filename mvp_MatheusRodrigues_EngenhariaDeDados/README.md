# MVP de Engenharia de Dados — Análise do Orçamento e das Bolsas da CAPES

## Visão Geral

Este projeto foi desenvolvido como MVP de Engenharia de Dados com o objetivo de construir um pipeline de dados para analisar a evolução do orçamento da CAPES e a distribuição de bolsas no Brasil entre 2013 e 2020.

O projeto utiliza a arquitetura Medalhão (Bronze, Silver e Gold), organizando os dados desde sua ingestão até a construção de tabelas analíticas voltadas às perguntas de negócio.

## Objetivo

O objetivo principal é analisar a evolução dos recursos orçamentários da CAPES ao longo do período estudado, relacionando-os ao orçamento do Ministério da Educação (MEC) e à evolução das bolsas da CAPES.

As análises possuem caráter descritivo e não buscam estabelecer relações causais entre os eventos observados.

## Tecnologias Utilizadas

- Databricks
- SQL
- Delta Lake
- Unity Catalog
- Databricks Volumes
- Git
- GitHub

## Arquitetura do Pipeline

O pipeline foi estruturado utilizando a arquitetura Medalhão:

**Bronze:** ingestão e armazenamento dos dados brutos.

**Silver:** limpeza, padronização, tratamento de duplicidades e transformação dos dados.

**Gold:** construção do modelo analítico utilizado nas consultas e análises finais.

## Modelo de Dados

A camada Gold é composta por cinco tabelas:

### Dimensões

- `dim_tempo`
- `dim_orgao`
- `dim_regiao`

### Fatos

- `fato_orcamento`
- `fato_bolsas`

Relacionamento lógico principal:

`dim_orgao → fato_orcamento ← dim_tempo → fato_bolsas ← dim_regiao`

## Qualidade dos Dados

Durante o processamento foram realizadas verificações de:

- valores nulos e vazios;
- registros duplicados;
- tipos de dados;
- padronização de valores monetários;
- consistência entre as camadas do pipeline.

Na base orçamentária da CAPES, foram identificados e removidos 8 registros duplicados, passando de 15.739 registros na camada Bronze para 15.731 registros tratados.

Na base de bolsas, os 789.773 registros tratados na camada Silver foram preservados na camada Gold.

## Principais Resultados

Entre os resultados obtidos no período analisado:

- a média da dotação inicial da CAPES passou de aproximadamente R$ 5,22 bilhões entre 2013 e 2016 para R$ 4,01 bilhões entre 2017 e 2020;
- entre 2016 e 2020, a dotação inicial da CAPES apresentou variação de aproximadamente -46,26%, enquanto o orçamento do MEC apresentou variação de aproximadamente +3,33%;
- a participação média da CAPES no orçamento analisado do MEC passou de aproximadamente 5,49% para 3,63% entre os dois períodos comparados;
- o número de bolsas passou de 100.433 em 2016 para 95.116 em 2020, enquanto a distribuição regional permaneceu relativamente estável.

Os resultados são interpretados de forma descritiva, sem atribuição de causalidade.

## Organização dos Notebooks

O desenvolvimento foi dividido nos seguintes notebooks:

- `mvp01-preparacao` — preparação do ambiente e dos dados;
- `mvp03-bronze` — ingestão dos dados na camada Bronze;
- `mvp04-silver` — limpeza e transformação dos dados;
- `mvp05-gold` — construção do modelo Gold e análises finais.

## Documentação

O repositório também contém o relatório completo do projeto:

`MVP - Banco de Dados.pdf`

O documento apresenta detalhadamente as fontes utilizadas, arquitetura, modelagem, tratamentos realizados, consultas e resultados obtidos.

## Autor

**Matheus Rodrigues**