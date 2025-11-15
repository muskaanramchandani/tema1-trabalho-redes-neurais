# Projeto 1: Classificação de Doenças Cardíacas (Redes Neurais)

[cite_start]Este repositório documenta o Trabalho 2 da disciplina FIA (Prof. Edjard Mota). [cite: 1]

## 1. Descrição do Projeto e O Problema

[cite_start]O objetivo deste projeto é construir um classificador binário para prever a **presença (1)** ou **ausência (0)** de doença cardíaca [cite: 5][cite_start], um desafio crítico de saúde pública, visto que as doenças cardiovasculares são a principal causa de morte em todo o mundo. [cite: 4]

[cite_start]Para isso, foi utilizada uma Rede Neural Artificial (ANN) do tipo feedforward [cite: 32][cite_start], implementada em Keras, e treinada com o dataset "Heart Disease UCI" [cite: 9][cite_start], que contém 14 atributos clínicos de pacientes. [cite: 15]

O fluxo de trabalho principal, detalhado no notebook `Tema1_Trabalho2_RedesNeurais.ipynb`, incluiu:

* **Limpeza de Dados:** Carregamento do dataset, tratamento de valores ausentes e remoção de duplicatas. O dataset original de 1025 registros foi reduzido para **302 amostras únicas**.
* **Pré-processamento:** Padronização das 13 características (features) de entrada usando `StandardScaler` para normalizar as diferentes escalas (ex: 'age' vs 'chol'). [cite_start]Este é um passo essencial para o bom desempenho da rede neural. [cite: 13]
* **Modelagem:** Criação de um modelo sequencial com duas camadas ocultas (16 e 8 neurônios, ativação ReLU) e uma camada de saída (1 neurônio, ativação sigmoide) para classificação binária. Foram aplicadas camadas de Dropout para regularização e prevenção de overfitting.

---

## 2. Resultados Obtidos

O modelo foi treinado por 50 épocas e avaliado no conjunto de teste (61 amostras), que não foi utilizado durante o treinamento. Os resultados demonstram um desempenho sólido para o classificador.

* **Acurácia Geral (Conjunto de Teste):** **80.3%**

### Relatório de Classificação (Dados de Teste)

O modelo obteve um desempenho equilibrado na distinção entre as duas classes:

| Classe | Precision | Recall | F1-Score |
| :--- | :---: | :---: | :---: |
| 0 (Sem Doença) | 0.79 | 0.79 | 0.79 |
| 1 (Com Doença) | 0.82 | 0.82 | 0.82 |
| **Média Ponderada** | **0.80** | **0.80** | **0.80** |

Os gráficos de Acurácia e Perda (Loss) ao longo do treinamento (disponíveis no notebook) mostram que as curvas de treino e validação (teste) se acompanharam de perto, indicando que as técnicas de regularização (Dropout) foram eficazes em prevenir um overfitting significativo.

A matriz de confusão e o relatório de classificação detalhado podem ser encontrados no final do notebook.
