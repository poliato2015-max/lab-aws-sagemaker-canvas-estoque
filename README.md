# 📊 Previsão de Estoque Inteligente com AWS SageMaker Canvas

> Sistema de previsão de estoque baseado em Machine Learning no-code — dataset gerado com IA Generativa (Claude), modelo treinado e avaliado no Amazon SageMaker Canvas, sem necessidade de programação.

[![AWS SageMaker](https://img.shields.io/badge/AWS-SageMaker%20Canvas-FF9900?logo=amazonaws)](https://aws.amazon.com/pt/sagemaker/canvas/)
[![Machine Learning](https://img.shields.io/badge/ML-No--Code-blue)]()
[![IA Generativa](https://img.shields.io/badge/Dataset-Claude%20Sonnet-blueviolet)](https://www.anthropic.com)
[![DIO Desafio IA](https://img.shields.io/badge/DIO-Desafio%20IA-orange)](https://www.dio.me)
[![Status](https://img.shields.io/badge/Status-Conclu%C3%ADdo-brightgreen)]()

---

## 📋 Pré-requisitos

**Requisitos Técnicos:**
- Conta ativa na AWS com permissões para SageMaker
- Acesso ao Amazon SageMaker Canvas
- Conhecimento básico de conceitos de Machine Learning

**Recursos Necessários:**
- Dataset histórico de vendas/estoque
- Navegador web atualizado
- Conexão estável com a internet

> Para criação de conta AWS, consulte o guia completo da equipe DIO: [AWS Cloud Quickstart](https://github.com/digitalinnovationone/aws-cloud-quickstart)

---

## 🎯 Objetivos do Desafio

Desenvolver um modelo de Machine Learning capaz de prever demandas futuras de estoque, permitindo:

- **Otimização de inventário** — redução de custos com excesso ou falta de produtos
- **Previsão de demanda** — antecipação de necessidades de reposição
- **Tomada de decisão baseada em dados** — insights quantitativos para estratégias de supply chain

---

## 📚 Fundamentação Teórica

### 1. Problema de Negócio
A gestão inadequada de estoque representa um dos principais desafios operacionais para empresas, resultando em:

- Custos de armazenamento elevados quando há excesso de produtos
- Perda de vendas e insatisfação do cliente em casos de ruptura de estoque
- Obsolescência de produtos devido a previsões imprecisas

### 2. Abordagem de Machine Learning
Utilizamos algoritmos de séries temporais e regressão para modelar padrões históricos de vendas e prever demandas futuras. O SageMaker Canvas aplica automaticamente técnicas como:

- **AutoML** — seleção automática do melhor algoritmo
- **Feature Engineering** — criação de variáveis preditoras relevantes
- **Validação cruzada** — avaliação robusta do modelo

---

## 📊 Metodologia

### 1. Compreensão e Preparação dos Dados

**Criação do Dataset com IA Generativa**

O dataset foi gerado com auxílio do **Claude Sonnet (Anthropic)**, produzindo dados realistas para o treinamento do modelo:

| Característica | Detalhe |
|---|---|
| Total de registros | 500 |
| Produtos diferentes | 25 |
| Período | 31/12/2024 a 19/01/2025 |
| Mínimo por dia | 20 produtos vendidos com variação natural |
| Flags de promoção | 10% a 30% |
| Formato | CSV pronto para uso no SageMaker Canvas |

**Colunas do dataset:**
- `PRODUTO` — ID numérico (1 a 25)
- `DATA_VENDA` — formato YYYY-MM-DD
- `FLAG_PROMOCAO` — 0 ou 1
- `QUANTIDADE_ESTOQUE` — após a venda, podendo chegar a zero

---

### 2. Construir e Treinar

**Upload do dataset no SageMaker Canvas:**

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_upload_dataset_imagem_1.jpg?raw=true" style="width:100%">

**Validação das colunas e valores importados:**
A coluna de data da venda foi classificada automaticamente como tipo `timestamp`.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_visualizar_dataset_imagem_1.1.jpg?raw=true" style="width:100%">

**Tipo de modelo escolhido:**
O próprio SageMaker Canvas sugeriu automaticamente o modelo de análise preditiva mais adequado.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tipo_modelo_imagem_2.jpg?raw=true" style="width:100%">

**Configuração do modelo de séries temporais:**
- `ID Column` → `ID_PRODUTO` (valores únicos/independentes)
- `Time Stamp Column` → `DATA_VENDA` (ordem temporal dos dados)
- `Days` → 1 dia (período futuro de previsão)
- Feriados do Brasil habilitados como variável explicativa

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.jpg?raw=true" style="width:100%">

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.1.jpg?raw=true" style="width:100%">

**Variável alvo (target):** `QUANTIDADE_ESTOQUE` — extraída do histórico de dados de estoque.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_config_modelo_imagem_3.2.jpg?raw=true" style="width:100%">

**Treinamento do modelo:**
- Método: **Quick Build** — ideal para validação rápida
- Duração estimada: ~20 minutos

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_treinar_modelo_imagem_4.jpg?raw=true" style="width:100%">

---

### 3. Analisar

Após o treinamento, o SageMaker Canvas gerou métricas de desempenho e identificou as colunas com maior impacto nas previsões. A interpretação das métricas foi realizada com auxílio de IA.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_analisar_modelo_imagem_5.jpg?raw=true" style="width:100%">

**Tabela de referência das métricas:**

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_tabela_metricas_modelo_imagem_6.jpg?raw=true" style="width:100%">

**Avaliação do modelo:**
- ✅ Modelo considerado aceitável com base nas métricas de desempenho
- ⚠️ Métrica RMSE: ligeiramente acima do valor sugerido pelo SageMaker Canvas
- ✅ Demais métricas dentro dos valores recomendados
- `FLAG_PROMOCAO` — não apresentou impacto significativo no modelo
- `FLAG_FERIADO_BRASIL` — apresentou baixo impacto nas previsões

---

### 4. Prever

Execução do modelo para prever o volume de estoque para o próximo dia:
- Dataset utilizado: o mesmo importado anteriormente
- Tipo de previsão: **Batch prediction** (previsão em lote)
- Vantagem: processa todos os produtos simultaneamente e exporta os resultados de uma única vez

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_previsao_estoque_imagem_7.jpg?raw=true" style="width:100%">

**Métricas de percentis (P10, P50, P90):**

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_explicacao_metrica_p_imagem_8.jpg?raw=true" style="width:100%">

**Resultado — Produtos com previsão positiva (01, 05, 15, 16 e 21):**
Histórico indica reposição antes do estoque zerar — previsões P10, P50 e P90 permaneceram positivas.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_resultado_grafico_1_imagem_9.jpg?raw=true" style="width:100%">

**Resultado — Demais produtos:**
Histórico indica ausência de reposição nos últimos dias — previsões resultaram em valores zerados ou negativos.

<img src="https://github.com/poliato2015-max/imagens/blob/main/projeto_sagemakercanvas_resultado_grafico_2_imagem_10.jpg?raw=true" style="width:100%">

---

## 🏁 Conclusão

### Alcance dos Objetivos
O projeto atingiu seu objetivo principal de demonstrar a aplicação prática de Machine Learning no-code para previsão de estoque. O SageMaker Canvas provou ser uma ferramenta acessível e eficiente para criar modelos preditivos sem necessidade de programação extensiva.

### Aprendizados Técnicos
- Fluxo completo de um projeto de ML: preparação de dados, treinamento, análise e previsão
- Geração de dataset realista com IA Generativa (Claude Sonnet)
- Experiência prática com AutoML e seleção automática de algoritmos
- Interpretação de métricas de séries temporais (RMSE, WAPE)
- Análise de importância de features e sua influência no modelo
- Entendimento de previsões probabilísticas através de percentis (P10, P50, P90)

### Insights de Negócio
- Os produtos com previsões negativas/zeradas sinalizam necessidade urgente de reabastecimento ou descontinuidade
- Os 5 produtos com previsões positivas demonstram gestão eficiente de inventário — este padrão pode ser replicado para os demais
- A ausência de `FLAG_PROMOCAO` como variável relevante sugere que promoções não impactaram significativamente o volume de estoque no período analisado

---

## 👨‍💻 Autor

Desenvolvido por **Marcelo Poliato de Oliveira** como desafio prático do curso de Inteligência Artificial da [DIO](https://www.dio.me).

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Marcelo%20Poliato-0077B5?logo=linkedin)](https://www.linkedin.com/in/marcelo-poliato)
[![GitHub](https://img.shields.io/badge/GitHub-poliato2015--max-181717?logo=github)](https://github.com/poliato2015-max)
