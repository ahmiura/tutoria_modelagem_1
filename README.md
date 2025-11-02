# tutoria_modelagem_1
# Projeto de Regressão: Previsão de Custos de Seguro de Saúde

Este repositório contém um projeto de Machine Learning focado em um problema de regressão: a previsão de custos individuais de seguro de saúde. O objetivo é treinar, comparar e avaliar múltiplos algoritmos de regressão para identificar o modelo com o melhor desempenho preditivo.

O projeto utiliza **MLflow** e **DagsHub** para um gerenciamento robusto de experimentos, permitindo o rastreamento de métricas, parâmetros e artefatos de cada modelo treinado.

## 📋 Índice

- [Visão Geral](#-visão-geral)
- [Dataset](#-dataset)
- [Tecnologias Utilizadas](#-tecnologias-utilizadas)
- [Metodologia](#-metodologia)
- [Como Executar o Projeto](#-como-executar-o-projeto)
- [Resultados](#-resultados)

## 🎯 Visão Geral

O principal objetivo deste projeto é construir um modelo de regressão capaz de prever os custos de seguro (`charges`) com base em características demográficas e de saúde de um indivíduo. Para alcançar isso, o projeto segue as seguintes etapas:

1.  Análise exploratória e pré-processamento dos dados.
2.  Treinamento de uma vasta gama de modelos de regressão, desde modelos base até versões com ajuste de hiperparâmetros.
3.  Avaliação sistemática dos modelos utilizando métricas de regressão como R-squared (R²), Mean Absolute Error (MAE) e Root Mean Squared Error (RMSE).
4.  Uso do MLflow para registrar cada experimento, facilitando a comparação e a reprodutibilidade.
5.  Integração com DagsHub para versionamento de código e hospedagem do servidor MLflow.

## 📊 Dataset

O dataset utilizado é o **"Medical Cost Personal Datasets"**, disponível publicamente no Kaggle. Ele contém 1.338 registros com as seguintes colunas:

- **age**: Idade do beneficiário.
- **sex**: Gênero do beneficiário.
- **bmi**: Índice de Massa Corporal (IMC).
- **children**: Número de dependentes.
- **smoker**: Se o beneficiário é fumante ou não.
- **region**: Região de residência nos EUA.
- **charges**: Custos médicos individuais cobrados pelo seguro (variável alvo).

**Link para o dataset:** https://www.kaggle.com/datasets/mirichoi0218/insurance

## 🛠️ Tecnologias Utilizadas

- **Linguagem**: Python 3
- **Bibliotecas de Dados**: Pandas, NumPy
- **Visualização**: Seaborn, Matplotlib
- **Machine Learning**:
  - Scikit-learn (`LinearRegression`, `RandomForestRegressor`, `GradientBoostingRegressor`)
  - XGBoost (`XGBRegressor`)
  - LightGBM (`LGBMRegressor`)
  - CatBoost (`CatBoostRegressor`)
- **Experiment Tracking**: MLflow
- **Plataforma MLOps**: DagsHub

## 📈 Metodologia

O fluxo de trabalho foi estruturado da seguinte forma:

1.  **Preparação**: Os dados foram carregados e as variáveis categóricas (`sex`, `smoker`, `region`) foram transformadas em formato numérico usando One-Hot Encoding.
2.  **Divisão dos Dados**: O dataset foi dividido em conjuntos de treino (80%) e teste (20%).
3.  **Treinamento e Comparação**: Uma ampla gama de modelos foi treinada e avaliada, incluindo:
    - Modelos de *baseline* com hiperparâmetros padrão.
    - Modelos com duas rodadas de ajuste manual de hiperparâmetros (Tunado V0 e Tunado V1).
4.  **Logging com MLflow**: Para cada modelo treinado, um "run" foi iniciado no MLflow para registrar:
    - **Parâmetros**: O nome do modelo e seus hiperparâmetros.
    - **Métricas**: R², MAE, MSE, RMSE e tempo de treinamento.
    - **Artefatos**: O objeto do modelo treinado, salvo com `mlflow.sklearn.log_model()`.
5.  **Seleção do Melhor Modelo**: Após a execução de todos os experimentos, os resultados foram consolidados em um DataFrame e ordenados com base nos seguintes critérios, nesta ordem:
    1.  Maior **R-squared (R²)**.
    2.  Menor **Mean Absolute Error (MAE)**.
    3.  Menor **Tempo de Treinamento**.

## 🚀 Como Executar o Projeto

1.  **Clone o repositório:**
    ```bash
    git clone <URL_DO_SEU_REPOSITORIO_DAGSHUB>
    cd tutoria_modelagem_1
    ```

2.  **Crie e ative um ambiente virtual:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # No Windows: venv\Scripts\activate
    ```

3.  **Instale as dependências:**
    ```bash
    pip install -r requirements.txt
    ```
    *(Nota: Certifique-se de criar um arquivo `requirements.txt` com as bibliotecas do projeto).*

4.  **Execute o notebook ou script principal** que contém o código de treinamento. As credenciais do DagsHub serão configuradas automaticamente para enviar os resultados do MLflow para o servidor remoto.

## 🏆 Resultados

Após a execução de todos os experimentos, os resultados foram comparados para determinar o modelo com o melhor desempenho geral. O modelo campeão foi selecionado com base na sua capacidade de explicar a variância dos dados (maior R²) e na sua precisão de previsão (menor MAE).

A tabela de comparação completa e os detalhes de cada execução podem ser visualizados na aba **"Experiments"** do DagsHub neste repositório. O melhor modelo foi promovido ao **MLflow Model Registry** para facilitar seu versionamento e futuro deployment.

Resultados no MLflow:(dagshug)
https://dagshub.com/ahmiura/modelagem-exe1-regressao.mlflow/#/experiments/0?searchFilter=&orderByKey=attributes.start_time&orderByAsc=false&startTime=ALL&lifecycleFilter=Active&modelVersionFilter=All+Runs&datasetsFilter=W10%3D