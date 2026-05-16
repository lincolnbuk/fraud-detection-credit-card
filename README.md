
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

