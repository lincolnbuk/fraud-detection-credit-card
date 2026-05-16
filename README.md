
# Detecção de Fraude em Cartões de Crédito

## Visão Geral do Projeto
Este projeto foca na construção de um modelo de detecção de fraude para transações de cartão de crédito, utilizando um dataset real e técnicas de aprendizado de máquina para identificar transações fraudulentas.

## Objetivos
- Analisar e pré-processar um dataset de transações de cartão de crédito.
- Lidar com o severo desbalanceamento de classes entre transações fraudulentas e não fraudulentas.
- Treinar e avaliar diferentes modelos de classificação para identificar fraudes.
- Implementar Git Large File Storage (Git LFS) para gerenciar arquivos grandes.
- Publicar o projeto no GitHub.

## Dataset
O dataset utilizado é o `creditcard.csv`, proveniente do Kaggle (`mlg-ulb/creditcardfraud`). Ele contém transações de cartão de crédito em um período de dois dias, com features numéricas `V1` a `V28` que são o resultado de uma transformação PCA para preservar a privacidade. As colunas `Time` e `Amount` não foram transformadas, e a coluna `Class` indica se a transação é fraudulenta (1) ou não (0).

## Análise Exploratória de Dados (EDA) e Pré-processamento

### Principais Observações:
- **Ausência de Valores Nulos:** O dataset não apresenta valores nulos em nenhuma coluna.
- **Features PCA:** As colunas `V1` a `V28` já estão escaladas e transformadas via PCA.
- **Desbalanceamento de Classes:** Foi identificada uma proporção extremamente desbalanceada de classes, com a vasta maioria das transações sendo não fraudulentas (Classe 0) e um número muito pequeno de transações fraudulentas (Classe 1).

### Etapas de Pré-processamento:
1.  **Escalamento de Features:** As colunas `Time` e `Amount` foram escaladas utilizando `StandardScaler` para que tivessem uma escala similar às features PCA.
2.  **Divisão de Dados:** O dataset foi dividido em features (`X`) e target (`y`), e em seguida, em conjuntos de treino e teste (`X_train`, `X_test`, `y_train`, `y_test`) utilizando `stratify=y` para manter a proporção original das classes em ambos os conjuntos.
3.  **Tratamento de Desbalanceamento (SMOTE):** A técnica **SMOTE (Synthetic Minority Over-sampling Technique)** foi aplicada **apenas** ao conjunto de treino (`X_train`, `y_train`) para balancear as classes, criando `X_train_res` e `y_train_res`. Isso evita o vazamento de informações para o conjunto de teste.

## Modelagem e Avaliação

Foram explorados dois modelos de classificação:

### 1. Regressão Logística (Baseline)
- **Treinamento:** Treinado com os dados balanceados por SMOTE (`X_train_res`, `y_train_res`).
- **Desempenho:**
    - **ROC AUC Score:** Aproximadamente 0.9659.
    - **Recall (Fraude):** Alto (0.88), indicando boa capacidade de identificar fraudes.
    - **Precision (Fraude):** Baixo (0.06), resultando em muitos falsos positivos. Isso significa que, embora encontre a maioria das fraudes, também marca muitas transações legítimas como fraudulentas.

### 2. Random Forest Classifier
- **Treinamento:** Treinado com os dados balanceados por SMOTE (`X_train_res`, `y_train_res`).
- **Desempenho:**
    - **ROC AUC Score:** Aproximadamente 0.9489.
    - **Recall (Fraude):** Bom (0.78).
    - **Precision (Fraude):** Significativamente melhor (0.86), resultando em menos falsos positivos em comparação com a Regressão Logística. Isso o torna um modelo mais prático para este tipo de problema, onde o custo de falsos positivos pode ser alto.
- **Conclusão:** O Random Forest apresentou um melhor equilíbrio entre Precision e Recall, sendo mais adequado para o problema de detecção de fraude, apesar de um ROC AUC ligeiramente menor que a Regressão Logística.

## Análise de Importância das Features (Random Forest)
Após o treinamento do Random Forest, foi realizada uma análise de importância das features para entender quais variáveis contribuem mais para as previsões do modelo. Isso fornece insights sobre os fatores que mais influenciam a detecção de fraude.

## Gerenciamento de Versões com Git e GitHub
O projeto é versionado usando Git e hospedado no GitHub. Devido ao tamanho do arquivo `creditcard.csv` (143.84 MB), que excede o limite de 100 MB do GitHub para arquivos individuais, foi utilizado o **Git Large File Storage (Git LFS)** para gerenciar este arquivo eficientemente.

## Como Executar o Projeto
1.  **Clone o repositório:** `git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git`
2.  **Certifique-se de ter o Git LFS instalado:** `git lfs install`
3.  **Baixe o dataset `creditcard.csv`:** O Git LFS fará o download do arquivo grande automaticamente após o clone.
4.  **Abra o notebook:** O projeto pode ser explorado e executado no Google Colab ou em qualquer ambiente Jupyter compatível.
5.  **Instale as dependências:** `pip install -r requirements.txt` (se um arquivo `requirements.txt` for gerado) ou instale individualmente `pandas`, `scikit-learn`, `matplotlib`, `seaborn`, `imbalanced-learn`.



---

# Credit Card Fraud Detection

## Project Overview
This project focuses on building a fraud detection model for credit card transactions, using a real-world dataset and machine learning techniques to identify fraudulent transactions.

## Objectives
- Analyze and preprocess a credit card transaction dataset.
- Address severe class imbalance between fraudulent and non-fraudulent transactions.
- Train and evaluate different classification models to identify fraud.
- Implement Git Large File Storage (Git LFS) to manage large files.
- Publish the project on GitHub.

## Dataset
The dataset used is `creditcard.csv`, sourced from Kaggle (`mlg-ulb/creditcardfraud`). It contains credit card transactions over two days, with numerical features `V1` to `V28` being the result of a PCA transformation for privacy. The `Time` and `Amount` columns were not transformed, and the `Class` column indicates whether the transaction is fraudulent (1) or not (0).

## Exploratory Data Analysis (EDA) and Preprocessing

### Key Observations:
- **No Missing Values:** The dataset has no missing values in any column.
- **PCA Features:** Columns `V1` to `V28` are already scaled and PCA-transformed.
- **Class Imbalance:** A heavily imbalanced class distribution was identified, with a vast majority of non-fraudulent transactions (Class 0) and a very small number of fraudulent transactions (Class 1).

### Preprocessing Steps:
1.  **Feature Scaling:** `Time` and `Amount` columns were scaled using `StandardScaler` to bring them to a similar scale as the PCA-transformed features.
2.  **Data Splitting:** The dataset was split into features (`X`) and target (`y`), and then into training and testing sets (`X_train`, `X_test`, `y_train`, `y_test`) using `stratify=y` to maintain the original class proportions in both sets.
3.  **Imbalance Handling (SMOTE):** **SMOTE (Synthetic Minority Over-sampling Technique)** was applied *only* to the training set (`X_train`, `y_train`) to balance the classes, creating `X_train_res` and `y_train_res`. This prevents data leakage to the test set.

## Modeling and Evaluation

Two classification models were explored:

### 1. Logistic Regression (Baseline)
- **Training:** Trained with SMOTE-balanced data (`X_train_res`, `y_train_res`).
- **Performance:**
    - **ROC AUC Score:** Approximately 0.9659.
    - **Recall (Fraud):** High (0.88), indicating good ability to identify fraud.
    - **Precision (Fraud):** Low (0.06), resulting in many false positives. This means that while it finds most fraud, it also incorrectly flags many legitimate transactions as fraudulent.

### 2. Random Forest Classifier
- **Training:** Trained with SMOTE-balanced data (`X_train_res`, `y_train_res`).
- **Performance:**
    - **ROC AUC Score:** Approximately 0.9489.
    - **Recall (Fraud):** Good (0.78).
    - **Precision (Fraud):** Significantly better (0.86), resulting in fewer false positives compared to Logistic Regression. This makes it a more practical model for this problem, where the cost of false positives can be high.
- **Conclusion:** Random Forest showed a better balance between Precision and Recall, making it more suitable for the fraud detection problem, despite a slightly lower ROC AUC than Logistic Regression.

## Feature Importance Analysis (Random Forest)
After Random Forest training, a feature importance analysis was performed to understand which variables contribute most to the model's predictions. This provides valuable insights into the factors influencing fraud detection.

## Version Control with Git and GitHub
The project is version-controlled using Git and hosted on GitHub. Due to the size of the `creditcard.csv` file (143.84 MB), which exceeds GitHub's 100 MB limit for individual files, **Git Large File Storage (Git LFS)** was used to manage this file efficiently.

## How to Run the Project
1.  **Clone the repository:** `git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git`
2.  **Ensure Git LFS is installed:** `git lfs install`
3.  **Download the `creditcard.csv` dataset:** Git LFS will automatically download the large file after cloning.
4.  **Open the notebook:** The project can be explored and executed in Google Colab or any compatible Jupyter environment.
5.  **Install dependencies:** `pip install -r requirements.txt` (if a `requirements.txt` file is generated) or individually install `pandas`, `scikit-learn`, `matplotlib`, `seaborn`, `imbalanced-learn`.
