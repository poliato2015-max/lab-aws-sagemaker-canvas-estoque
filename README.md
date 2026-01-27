# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Este projeto implementa um sistema de previsão de estoque baseado em Machine Learning utilizando Amazon SageMaker Canvas, permitindo a criação de modelos preditivos sem necessidade de codificação. O objetivo é auxiliar na tomada de decisão sobre gestão de inventário através de técnicas de análise preditiva.

## 📋 Pré-requisitos

Requisitos Técnicos:

- Conta ativa na AWS com permissões para SageMaker
- Acesso ao Amazon SageMaker Canvas
- Conhecimento básico de conceitos de Machine Learning

Recursos Necessários:

- Dataset histórico de vendas/estoque (disponível na pasta datasets/)
- Navegador web atualizado
- Conexão estável com a internet

Nota : Para criação de conta AWS, consulte o guia completo realizado pela equipe DIO [AWS Cloud Quickstart](https://github.com/digitalinnovationone/aws-cloud-quickstart).

## 🎯 Objetivos Deste Desafio de Projeto

Desenvolver um modelo de Machine Learning capaz de prever demandas futuras de estoque, permitindo:

- Otimização de inventário: Redução de custos com excesso ou falta de produtos
- Previsão de demanda: Antecipação de necessidades de reposição
- Tomada de decisão baseada em dados: Insights quantitativos para estratégias de supply chain
  
## 📚 Fundamentação Teórica

### 1. Problema de Negócio
A gestão inadequada de estoque representa um dos principais desafios operacionais para empresas, resultando em:

- Custos de armazenamento elevados quando há excesso de produtos
- Perda de vendas e insatisfação do cliente em casos de ruptura de estoque
- Obsolescência de produtos devido a previsões imprecisas

### 2. Abordagem de Machime Learning
Utilizamos algoritmos de séries temporais e regressão para modelar padrões históricos de vendas e prever demandas futuras. O SageMaker Canvas aplica automaticamente técnicas como:

- AutoML: Seleção automática do melhor algoritmo
- Feature Engineering: Criação de variáveis preditoras relevantes
- Validação cruzada: Avaliação robusta do modelo

## 📊 Metodologia

### 1. Compreensão e Preparação dos Dados

- 1.1 Criação do Dataset

  Variáveis:
  - Temporais: Data, mês, ano
  - Demanda: Unidades em estoque
  - Contextuais: Sazonalidade, promoções, feriados
  
  Critérios básicos:
  - Qualidade dos dados (baixa ou nenhuma taxa de valores ausentes)
  - Granularidade temporal adequada (diária, semanal ou mensal)
  - Período histórico: 19 dias
  
  Geração dos dados:
    - Para a geração dos dados foi Utilizado uma ferramenta de Inteligência Artificial Generativa: Claude Sonnet 4.5
    - Características do dataset gerado:
      - 500 registros de vendas
      - 25 produtos diferentes
      - Período: 31/12/2024 a 19/01/2025
      - Mínimo de 20 produtos vendidos por dia com variação natural
      - Estoque realista que decresce com as vendas
      - Flags de promoção ( de 10% a 30%)
      - Formato CSV pronto para uso no SageMaker Canvas
      - Colunas existentes no arquivo gerado:
        - PRODUTO ((ID numérico 1-25)
        - DATA_VENDA (formato YYYY-MM-DD)
        - FLAG_PROMOCAO (0 ou 1)
        - QUANTIDADE_ESTOQUE ( após a venda)

### 2. Construir/Treinar

-  2.1 Faça o upload do dataset criado pela Inteligência Artificial Generativa na ferramenta SageMaker Canvas.

  [![Imagem](https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_upload_dataset_imagem_1.jpg?raw=true)
 
-  2.2 Configure as variáveis de entrada e saída de acordo com os dados.
-  Escolha o nome e o tipo do modelo a ser criado. Neste projeto o próprio Sage Maker Canvas sugerio o modelo de análise preditiva.
[![Imagem](https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tipo_modelo_imagem_2.jpg?raw=true)

-  
-   Inicie o treinamento do modelo. Isso pode levar algum tempo, dependendo do tamanho do dataset.

### 3. Analisar

-   Após o treinamento, examine as métricas de performance do modelo.
-   Verifique as principais características que influenciam as previsões.
-   Faça ajustes no modelo se necessário e re-treine até obter um desempenho satisfatório.

### 4. Prever

-   Use o modelo treinado para fazer previsões de estoque.
-   Exporte os resultados e analise as previsões geradas.
-   Documente suas conclusões e qualquer insight obtido a partir das previsões.
