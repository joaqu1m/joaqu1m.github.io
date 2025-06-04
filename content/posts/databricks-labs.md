---
date: '2025-06-02T20:58:02-03:00'
draft: true
title: 'Explorando o Databricks: Um Projeto Prático com Dados de Criptomoedas'
---

Opa!

Recentemente, durante um final de semana produtivo, tive a oportunidade de explorar a ferramenta **Databricks**. Isso foi possível através de um laboratório de cinco dias oferecido pela própria Databricks, financiado pela minha empresa atual. Além de realizar os exercícios propostos no curso, decidi utilizar o ambiente para desenvolver um projeto pessoal completo, desde a ingestão dos dados até a construção de um painel de visualização.

### Vamos começar explicando o que é o Databricks, na minha visão

De forma direta, o Databricks é uma **plataforma unificada de análise de dados**, construída sobre o Apache Spark. Gosto de pensar nele como uma central abrangente para o ciclo de vida dos dados, uma plataforma que ajuda mais na **governança** do que qualquer outra coisa. É um ambiente colaborativo onde cientistas de dados, engenheiros e analistas de negócios podem trabalhar juntos em todas as etapas: desde a coleta e tratamento dos dados brutos, passando pela construção de modelos de Machine Learning, até a criação de relatórios e visualizações.

Como alguém que, apesar de não ter tanta experiência, já conseguiu experimentar a área de dados, fiquei impressionado com a quantidade de ferramentas e funcionalidades que o Databricks consegue **unificar** em uma única plataforma. Neste post, quero compartilhar um pouco dessa experiência, mostrando como cada etapa do meu projeto foi implementada utilizando a plataforma.

**Uma observação sobre o ambiente do laboratório:** O Databricks é uma plataforma robusta e, naturalmente, possui custos (altíssimos) associados. O ambiente do laboratório que utilizei, por ser focado em aprendizado, tinha algumas limitações de recursos. Por exemplo, não tive acesso às **SQL Warehouses** (mais orientadas para análises com SQL e ferramentas de Business Intelligence), mas pude explorar bastante os **Clusters**. Estes são a unidade de computação do Databricks ideal para processamento de dados em larga escala com Spark, e foram perfeitamente adequados para as necessidades do meu projeto.

## A Proposta do Projeto: Uma ETL de Criptomoedas em Tempo Real

Então, qual era a proposta central do projeto? O objetivo era construir um fluxo de dados (um ETL: **Extract, Transform, Load**) completo. A intenção era capturar dados em tempo real, processá-los, transformá-los em informações úteis e, ao final, criar painéis (dashboards) para acompanhar os resultados.

Na prática, o projeto foi dividido em três etapas principais, todas executadas no Databricks:

1.  **Ingestão dos Dados:** Os dados foram capturados em tempo real a partir de um *socket* público da Binance. Esse *socket* fornecia o valor do índice de diversas criptomoedas em tempo real em um intervalo de 3 segundos.
2.  **Processamento e Transformação (Camadas Bronze, Silver e Gold):** Com os dados brutos em mãos (o que é comumente chamado de camada *Bronze* pela arquitetura Medallion), iniciei o trabalho de limpeza e estruturação. Esses dados foram transformados para uma camada intermediária, mais organizada (camada *Silver*), e, finalmente, agregados e preparados para análise na camada *Gold*, pronta para consumo. Todo esse processamento ocorreu em *near-real-time*.
3.  **Visualização:** Por fim, foram criados dashboards simples para o acompanhamento em tempo real de algumas criptomoedas específicas que selecionei, como Bitcoin, Ethereum e Dogecoin.

Antes de detalhar cada uma dessas etapas, considero importante mencionar como o código foi organizado e o projeto estruturado. Vamos abordar um pouco sobre...

## Organização de Projetos Databricks: Integração com GitHub e CI/CD

Confesso que tirei ideias da blablabla