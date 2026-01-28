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

- Criação do Dataset

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
      - Estoque realista que decresce com as vendas e podendo chegar a zero
      - Flags de promoção ( de 10% a 30%)
      - Formato CSV pronto para uso no SageMaker Canvas
      - Colunas existentes no arquivo gerado:
        - PRODUTO ((ID numérico 1-25)
        - DATA_VENDA (formato YYYY-MM-DD)
        - FLAG_PROMOCAO (0 ou 1)
        - QUANTIDADE_ESTOQUE ( após a venda)

### 2. Construir/Treinar

-  Realizar o upload do dataset criado pela Inteligência Artificial Generativa na ferramenta SageMaker Canvas.

   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_upload_dataset_imagem_1.jpg?raw=true" width="800" height="400">

-  Avaliar se os valores e colunas da base carregada no SageMaker Canvas foi importado corretamente.
    -  Ao importar nosso dataset, a coluna data da venda foi classificada automaticamente como tipo timestamp.

     <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_visualizar_dataset_imagem_1.1.jpg?raw=true" width="800" height="400">
 
 - Nome e o tipo do modelo escolhido a ser criado.
   - Neste projeto o próprio Sage Maker Canvas sugeriu o modelo de análise preditiva.

   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tipo_modelo_imagem_2.jpg?raw=true" width="800" height="400">

  - Configurando o modelo de séries temporais:
    - ID column = A coluna do nosso dataset que representa valores uúnicos/independentes é a ID_PRODUTO
    - Time stamp Colunn = A coluna do nosso dataset que conta ordem temporaral de daodos é a DATA_VENDA
    - Days = Definimos 1 dia como o período futuro que o modelo deve prever
    - Habilitamos para que o modelo utilize feriados no Brasil como variável explicativa
    
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.jpg?raw=true" width="800" height="400">
        
    - Para a configuração do tipo modelo, a própria ferramenta escolheu automaticamente a série temporal

    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.1.jpg?raw=true" width="800" height="400">
   
    - Definimos a coluna do dataset que representa a variável alvo (target), permitindo que o modelo identifique corretamente o dado a ser previsto.
      -   Neste projeto, a variável selecionada foi “quantidade de estoque”, extraída do histórico de dados
      -   Observe que os valores das colunas e quantidade de registros do dataset importado estão corretos
    
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.2.jpg?raw=true" width="800" height="400">
  
 - Treinamento do modelo
   - Após configurar os parâmetros necessários, necessário iniciarmos o treinamento para construção do modelo
   - Escolhemos a opção mais demorada porém mais acertiva ( Standad Build ) com prazo estimado em +- 2 horas para a conclisão do treinamento
   
   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_treinar_modelo_imagem_4.jpg?raw=true" width="800" height="400">
   
### 3. Analisar

-  Após SageMaker Canvas encerrar o treinamento do modelo, iremos avaliar as métricas de performance.

-   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_analisar_modelo_imagem_5.jpg?raw=true" width="800" height="400">

-    Utilizamos a inteligência artificial para nos ajudar a entender o significado das métricas retornadas após o treinamento do treinamento:

  


-   Verifique as principais características que influenciam as previsões.
-   Faça ajustes no modelo se necessário e re-treine até obter um desempenho satisfatório.

### 4. Prever

-   Use o modelo treinado para fazer previsões de estoque.
-   Exporte os resultados e analise as previsões geradas.
-   Documente suas conclusões e qualquer insight obtido a partir das previsões.
