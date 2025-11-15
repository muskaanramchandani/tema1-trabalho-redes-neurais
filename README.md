# Projeto 1: Classificação Binária de Doenças Cardíacas com Redes Neurais

Este repositório contém o notebook e os resultados do Trabalho 2 da disciplina FIA (Prof. Edjard Mota), focado na construção de um classificador binário para detecção de doenças cardíacas.

## 1. Descrição do Problema

As doenças cardiovasculares são a principal causa de morte em todo o mundo, tornando a detecção precoce um desafio crítico para a saúde pública. O objetivo deste projeto é construir um modelo de classificação binária capaz de prever, com base em atributos clínicos, a **presença (1)** ou **ausência (0)** de doença cardíaca em um paciente.

O projeto utiliza o dataset "Heart Disease UCI", que disponibiliza 14 atributos clínicos (como idade, sexo, pressão arterial em repouso, colesterol, etc.).

Um desafio central deste dataset, e um foco de aprendizado do projeto, é a **diferença de escala** entre as características (ex: `age` variando de ~29 a 77, enquanto `chol` pode ir de ~126 a 564). Isso torna a etapa de **normalização de características** crucial para o desempenho de Redes Neurais Artificiais (ANNs).

## 2. Metodologia e Abordagem

O fluxo de trabalho completo está documentado no notebook (`Tema1_Trabalho2_RedesNeurais.ipynb`) e seguiu estas etapas:

### 2.1. Limpeza e Pré-processamento
O dataset inicial continha 1025 registros, muitos dos quais eram duplicados. Após a remoção de duplicatas, o conjunto de dados foi consolidado em **302 amostras únicas** e limpas, que foram usadas para o treinamento e teste.

Os dados foram então divididos:
* **Treinamento:** 241 amostras (80%)
* **Teste:** 61 amostras (20%)

A etapa mais crítica do pré-processamento foi a **padronização (normalização)**. O `StandardScaler` do Scikit-learn foi aplicado aos dados de treino e teste para garantir que todas as 13 *features* de entrada tivessem média 0 e desvio padrão 1, evitando que atributos com escalas maiores dominassem o aprendizado do modelo.

### 2.2. Arquitetura do Modelo
Foi construída uma Rede Neural Artificial (ANN) *feedforward* usando a API Sequencial do Keras. A arquitetura foi definida da seguinte forma:

1.  **Camada Oculta 1:** `Dense` com 16 neurônios e função de ativação `ReLU`.
2.  **Regularização:** `Dropout` (taxa de 0.25) para prevenir overfitting.
3.  **Camada Oculta 2:** `Dense` com 8 neurônios e função de ativação `ReLU`.
4.  **Regularização:** `Dropout` (taxa de 0.25).
5.  **Camada de Saída:** `Dense` com 1 neurônio e função de ativação `sigmoide`, ideal para produzir uma probabilidade (entre 0 e 1) para a classificação binária.

Para mitigar ainda mais o overfitting, foi aplicado um regularizador `L2` em ambas as camadas densas ocultas. O modelo foi compilado com o otimizador `rmsprop` e a função de perda `binary_crossentropy`.

---

## 3. Resultados Obtidos

O modelo foi treinado por 50 épocas e avaliado rigorosamente no conjunto de teste (as 61 amostras que o modelo nunca viu).

### 3.1. Desempenho Geral
A acurácia final do modelo no conjunto de teste foi de **80,33%**.

Os gráficos de **Acurácia** e **Perda (Loss)** ao longo das épocas (ver notebook) mostram que as curvas de treinamento e validação (teste) se mantiveram próximas, indicando que as técnicas de regularização (Dropout e L2) foram eficazes em evitar um overfitting severo.

### 3.2. Métricas de Classificação (Precisão e Recall)
A performance do modelo foi bem equilibrada para ambas as classes, como detalhado no relatório de classificação:

> **Relatório de Classificação (Conjunto de Teste):**
>
> | Classe | Precision | Recall | F1-Score | Amostras |
> | :--- | :---: | :---: | :---: | :---: |
> | 0 (Sem Doença) | 0.79 | 0.79 | 0.79 | 28 |
> | 1 (Com Doença) | 0.82 | 0.82 | 0.82 | 33 |
> | **Média Ponderada** | **0.80** | **0.80** | **0.80** | **61** |

* **Interpretação:**
    * **Recall (1): 0.82** - O modelo identificou corretamente 82% de todos os pacientes que realmente tinham a doença.
    * **Recall (0): 0.79** - O modelo identificou corretamente 79% de todos os pacientes que não tinham a doença.

### 3.3. Matriz de Confusão
A matriz de confusão visualiza os 12 erros cometidos pelo modelo nas 61 previsões de teste:
* **22 Verdadeiros Negativos** (Corretamente previstos como "Sem Doença")
* **27 Verdadeiros Positivos** (Corretamente previstos como "Com Doença")
* **6 Falsos Positivos** (Erro: Pacientes saudáveis classificados como doentes)
* **6 Falsos Negativos** (Erro: Pacientes doentes classificados como saudáveis)
* <img width="731" height="583" alt="image" src="https://github.com/user-attachments/assets/1aa4ffe4-c0c5-4874-a9b2-7af9ea841819" />

