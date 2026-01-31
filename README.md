# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Este projeto implementa um sistema de previsão de estoque baseado em Machine Learning utilizando Amazon SageMaker Canvas, permitindo a criação de modelos preditivos sem necessidade de codificação. O objetivo é auxiliar na tomada de decisão sobre gestão de inventário através de técnicas de análise preditiva.

## 📋 Pré-requisitos

Requisitos Técnicos:

- Conta ativa na AWS com permissões para SageMaker
- Acesso ao Amazon SageMaker Canvas
- Conhecimento básico de conceitos de Machine Learning

Recursos Necessários:

- Um Dataset histórico de vendas/estoque
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
        - QUANTIDADE_ESTOQUE ( após a venda, podendo chegar a zero )

### 2. Construir/Treinar

-  Realizar o upload do dataset criado pela Inteligência Artificial Generativa na ferramenta SageMaker Canvas.

   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_upload_dataset_imagem_1.jpg?raw=true" width="800" height="400">

-  Avaliar se os valores e colunas da base carregada no SageMaker Canvas foi importado corretamente.
    -  Ao importar nosso dataset, a coluna data da venda foi classificada automaticamente como tipo timestamp.

     <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_visualizar_dataset_imagem_1.1.jpg?raw=true" width="800" height="400">
 
 - Nome e o tipo do modelo escolhido a ser criado.
   - Neste projeto, o próprio SageMaker Canvas sugeriu automaticamente o modelo de análise preditiva mais adequado.

   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tipo_modelo_imagem_2.jpg?raw=true" width="800" height="400">

  - Configurando o modelo de séries temporais:
    - ID column = A coluna do nosso dataset que representa valores uúnicos/independentes é a ID_PRODUTO
    - Time stamp Colunn = A coluna do nosso dataset que conta ordem temporaral de daodos é a DATA_VENDA
    - Days = Período futuro de previsão: 1 dia
    - Habilitamos o uso de feriados do Brasil como variável explicativa
    
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.jpg?raw=true" width="800" height="400">
        
    - Para a configuração do tipo modelo, a própria ferramenta escolheu automaticamente a série temporal.

    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.1.jpg?raw=true" width="800" height="400">
   
    - Definimos a coluna do dataset que representa a variável alvo (target), permitindo que o modelo identifique corretamente o dado a ser previsto:
      -   Variável selecionada: "QUANTIDADE_ESTOQUE", extraída do histórico de dados de estoque
      -   Validação realizada: os valores das colunas e a quantidade de registros do dataset importado estão corretos
    
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.2.jpg?raw=true" width="800" height="400">
  
 - Treinamento do modelo:
   - Com os parâmetros configurados, procedemos ao treinamento
   - Método escolhido: Quick build - ideal para validação rápida do modelo
   - Duração estimada: ~20 minutos
   
   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_treinar_modelo_imagem_4.jpg?raw=true" width="800" height="400">
   
### 3. Analisar

-  Após a conclusão do treinamento, o SageMaker Canvas gerou métricas de desempenho do modelo e identificou as colunas do dataset que tiveram maior impacto nas previsões.

   <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_analisar_modelo_imagem_5.jpg?raw=true" width="800" height="400">

-  Para facilitar a análise, utilizamos inteligência artificial na interpretação das descrições das métricas obtidas, avaliando se seus valores indicam qualidade adequada conforme os critérios de aceitação do modelo.
    -  Abaixo tabela para referência com as mêtricas de status:
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tabela_metricas_modelo_imagem_6.jpg?raw=true" width="800" height="400">

-   O modelo treinado foi considerado aceitável com base nas métricas de desempenho e análise de importância das variáveis:
    -   Métrica RMSE: ligeiramente acima do valor sugerido pelo SageMaker Canvas
    -   Demais métricas: dentro dos valores recomendados
    -   FLAG_PROMOÇÃO: não apresentou impacto significativo no modelo
    -   FLAG_FERIADO_BRASIL: apresentou baixo impacto nas previsões    

### 4. Prever

-   Chegamos à etapa final do projeto: executar o modelo para prever o volume de estoque para o próximo dia:
    -   Utilizamos o mesmo dataset importado anteriormente
    -   Tipo de previsão: Batch prediction (previsão em lote)
    -   Vantagem: permite processar todos os produtos simultaneamente e exportar os resultados de uma única vez
      
    <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_previsao_estoque_imagem_7.jpg?raw=true" width="800" height="400">

    -   Ao concluir o processamento, exportamos os resultados de todos os produtos para análise das métricas de percentis (P10, P50, P90) que representam as previsões de demanda para o próximo dia.
      
    -   Para facilitar o entendimento, utilizamos inteligência artificial na explicação das métricas de percentis:
     <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_explicacao_metrica_p_imagem_8.jpg?raw=true" width="800" height="400">

-   Resultado e parecer do modelo de previsão.
    -   Para os produtos 01, 05, 15, 16 e 21, o histórico de estoque do nosso dataset demonstra que sempre houve reposição antes do estoque zerar. Consequentemente, as previsões de P10, P50 e P90 permaneceram positivas.

     <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_resultado_grafico_1_imagem_9.jpg?raw=true" width="800" height="400">
     
    -  Para os demais produtos, o histórico de estoque do nosso dataset indica ausência de reposição nos últimos dias. Consequentemente, as previsões de P10, P50 e P90 resultaram em valores zerados ou negativos.
     <img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_resultado_grafico_2_imagem_10.jpg?raw=true" width="800" height="1200">

     
-   Conclusão.
    -   Alcance dos Objetivos:
        -   O projeto atingiu seu objetivo principal de demonstrar a aplicação prática de Machine Learning no-code para previsão de estoque. O SageMaker Canvas provou ser uma ferramenta acessível e eficiente para criar modelos preditivos sem necessidade de programação extensiva.
    -   Aprendizados Técnicos:
        -   Compreensão do fluxo completo de um projeto de ML: preparação de dados, treinamento, análise e previsão
        -   Experiência prática com AutoML e seleção automática de algoritmos
        -   Interpretação de métricas de séries temporais (RMSE, WAPE)
        -   Análise de importância de features e sua influência no modelo
        -   Entendimento de previsões probabilísticas através de percentis
     -   Insights de Negócio:
        -   Os produtos com previsões negativas/zeradas sinalizam necessidade urgente de reabastecimento ou de descontinuidade. A ausência de reposição nos últimos dias criou um padrão crítico que o modelo identificou.
        -   Os 5 produtos com previsões positivas demonstram gestão eficiente de inventário com reposições tempestivas. Este padrão pode ser replicado para os demais produtos.
 -   Considerações Finais:
        -   Este projeto representa uma excelente introdução ao mundo de Machine Learning aplicado à gestão de operações.
        -   O uso de SageMaker Canvas democratiza o acesso a técnicas avançadas de previsão, permitindo que profissionais de diferentes áreas apliquem ML em seus contextos sem barreiras técnicas significativas.

