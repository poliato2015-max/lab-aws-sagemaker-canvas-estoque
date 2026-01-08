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

## 🚀 Passo a Passo

### 1. Selecionar Dataset

-   Navegue até a pasta `datasets` deste repositório. Esta pasta contém os datasets que você poderá escolher para treinar e testar seu modelo de ML. Sinta-se à vontade para gerar/enriquecer seus próprios datasets, quanto mais você se engajar, mais relevante esse projeto será em seu portfólio.
-   Escolha o dataset que você usará para treinar seu modelo de previsão de estoque.
-   Faça o upload do dataset no SageMaker Canvas.

### 2. Construir/Treinar

-   No SageMaker Canvas, importe o dataset que você selecionou.
-   Configure as variáveis de entrada e saída de acordo com os dados.
-   Inicie o treinamento do modelo. Isso pode levar algum tempo, dependendo do tamanho do dataset.

### 3. Analisar

-   Após o treinamento, examine as métricas de performance do modelo.
-   Verifique as principais características que influenciam as previsões.
-   Faça ajustes no modelo se necessário e re-treine até obter um desempenho satisfatório.

### 4. Prever

-   Use o modelo treinado para fazer previsões de estoque.
-   Exporte os resultados e analise as previsões geradas.
-   Documente suas conclusões e qualquer insight obtido a partir das previsões.

## 🤔 Dúvidas?

Esperamos que esta experiência tenha sido enriquecedora e que você tenha aprendido mais sobre Machine Learning aplicado a problemas reais. Se tiver alguma dúvida, não hesite em abrir uma issue neste repositório ou entrar em contato com a equipe da DIO.
