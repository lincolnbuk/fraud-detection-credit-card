# 🛡️ Credit Card Fraud Detection | Detecção de Fraude em Cartões de Crédito

![Fraud Detection](https://img.shields.io/badge/Machine%20Learning-Credit%20Card%20Fraud%20Detection-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.8%2B-yellow?style=for-the-badge)

<div align="center">
  <img src="https://images.pexels.com/photos/18187343/pexels-photo-18187343.jpeg?w=800&h=400&fit=crop" alt="AI Robot Writing Code" width="100%" style="border-radius: 10px; margin: 20px 0; max-height: 400px;">
  <p><i>Intelligent Machine Learning Detection System | Sistema Inteligente de Detecção com Machine Learning</i></p>
</div>

---

## 📋 Project Overview | Visão Geral do Projeto

This project implements a **fraud detection model** for credit card transactions using advanced machine learning techniques and a real dataset with over 280 thousand records.

Este projeto implementa um **modelo de detecção de fraude** para transações de cartão de crédito, utilizando técnicas avançadas de aprendizado de máquina e um dataset real com mais de 280 mil registros.

### 🎯 Main Objectives | Objetivos Principais

- ✅ Analyze and pre-process credit card transaction datasets | Analisar e pré-processar dataset de transações de cartão de crédito
- ✅ Handle severe class imbalance (fraud vs legitimate) | Lidar com o severo desbalanceamento de classes (fraude vs legítima)
- ✅ Train and evaluate high-performance classification models | Treinar e avaliar modelos de classificação de alto desempenho
- ✅ Implement Git Large File Storage (Git LFS) for large files | Implementar Git Large File Storage (Git LFS) para arquivos grandes
- ✅ Publish professional project on GitHub | Publicar projeto profissional no GitHub

---

## 📊 Dataset

The dataset used is **`creditcard.csv`**, a real database from Kaggle (`mlg-ulb/creditcardfraud`).

O dataset utilizado é o **`creditcard.csv`**, uma base de dados real proveniente do Kaggle (`mlg-ulb/creditcardfraud`).

### 📁 File Information | Informações do Arquivo

| Property | Details | Propriedade | Detalhes |
|:---|:---|:---|:---|
| **Location** | [creditcard.csv](https://github.com/lincolnbuk/fraud-detection-credit-card/blob/main/creditcard.csv) | **Localização** | [creditcard.csv](https://github.com/lincolnbuk/fraud-detection-credit-card/blob/main/creditcard.csv) |
| **Size** | ~150.8 MB | **Tamanho** | ~150.8 MB |
| **Storage** | 🗄️ Git LFS (Large File Storage) | **Armazenamento** | 🗄️ Git LFS (Large File Storage) |
| **Format** | CSV | **Formato** | CSV |
| **Records** | 284,807 transactions | **Registros** | 284.807 transações |
| **Columns** | 31 (Time, V1-V28, Amount, Class) | **Colunas** | 31 (Time, V1-V28, Amount, Class) |
| **Period** | Two days of real transactions | **Período** | Dois dias de transações reais |

### 🔧 How to Access the File | Como Acessar o Arquivo

```bash
# 1. Clone the repository with Git LFS | Clone o repositório com Git LFS
git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git
cd fraud-detection-credit-card

# 2. Install Git LFS if necessary | Instale o Git LFS (se necessário)
git lfs install

# 3. Download the large file | Baixe o arquivo grande
git lfs pull

# 4. Access the file locally | Acesse o arquivo localmente
# The file will be available at: ./creditcard.csv
```

> ⚠️ **Note:** The file cannot be viewed in the GitHub web interface due to its size, but is fully accessible after cloning with Git LFS.
> 
> ⚠️ **Nota:** O arquivo não pode ser visualizado na interface web do GitHub devido ao seu tamanho, mas está completamente acessível após o clone com Git LFS.

---

## 🔍 Exploratory Data Analysis (EDA) and Pre-processing | Análise Exploratória de Dados (EDA) e Pré-processamento

### 📈 Key Observations | Principais Observações

| Observation | Details | Observação | Detalhes |
|:---|:---|:---|:---|
| **Null Values** | ✅ No null values in any column | **Valores Nulos** | ✅ Sem valores nulos em nenhuma coluna |
| **PCA Features** | Columns V1-V28 already scaled and transformed via PCA | **Features PCA** | Colunas V1-V28 já escaladas e transformadas via PCA |
| **Imbalanced Class** | 🔴 Vast majority non-fraudulent (Class 0) vs. rare frauds (Class 1) | **Classe Desbalanceada** | 🔴 Vasta maioria não fraudulenta (Classe 0) vs. fraudes raras (Classe 1) |
| **Target Distribution** | ~0.17% of fraudulent transactions | **Target Distribution** | ~0.17% de transações fraudulentas |

### ⚙️ Pre-processing Steps | Etapas de Pré-processamento

1. **Feature Scaling | Escalamento de Features**
   - `Time` and `Amount` scaled with `StandardScaler`
   - Alignment with PCA features scale
   - `Time` e `Amount` escaladas com `StandardScaler`
   - Alignamento com escala das features PCA

2. **Data Split | Divisão de Dados**
   - Separation into features (X) and target (y)
   - Train/test split with `stratify=y`
   - Maintains original class proportion
   - Separação em features (X) e target (y)
   - Split treino/teste com `stratify=y`
   - Mantém proporção original de classes

3. **Imbalance Handling | Tratamento de Desbalanceamento**
   - 🔧 **SMOTE (Synthetic Minority Over-sampling Technique)**
   - Applied **exclusively** to training set
   - Avoids data leakage in test set
   - 🔧 **SMOTE (Synthetic Minority Over-sampling Technique)**
   - Aplicado **exclusivamente** ao conjunto de treino
   - Evita data leakage no conjunto de teste

---

## 🤖 Modeling and Evaluation | Modelagem e Avaliação

Two classification models were explored and compared:

Dois modelos de classificação foram explorados e comparados:

### 1️⃣ Logistic Regression (Baseline) | Regressão Logística (Baseline)

```
┌─────────────────────────────────────────┐
│ LOGISTIC REGRESSION                     │
├─────────────────────────────────────────┤
│ ROC AUC Score:  0.9659  ⭐⭐⭐⭐⭐      │
│ Recall (Fraud): 0.88   (Sensitivity)    │
│ Precision:       0.06   (Low)           │
│ Status:          ⚠️ Many false positives │
└─────────────────────────────────────────┘
```

**Analysis | Análise:**
- ✅ Identifies majority of frauds (high recall) | Identifica maioria das fraudes (recall alto)
- ❌ Marks many legitimate transactions as fraud (many false positives) | Marca muitas transações legítimas como fraude (muitos falsos positivos)
- 💭 Less suitable for practical application | Menos adequado para aplicação prática

---

### 2️⃣ Random Forest Classifier ⭐

```
┌─────────────────────────────────────────┐
│ RANDOM FOREST                           │
├─────────────────────────────────────────┤
│ ROC AUC Score:  0.9489  ⭐⭐⭐⭐        │
│ Recall (Fraud): 0.78   (Good)           │
│ Precision:       0.86   (Excellent!) ✨ │
│ Status:          ✅ Recommended Model   │
└─────────────────────────────────────────┘
```

**Analysis | Análise:**
- ✅ Better Precision × Recall balance | Melhor equilíbrio Precision × Recall
- ✅ Fewer false positives | Menos falsos positivos
- ✅ More suitable for production | Mais adequado para produção
- 🏆 **Model selected for deployment | Modelo selecionado para deploy**

---

### 📊 Feature Importance Analysis (Random Forest) | Análise de Importância das Features (Random Forest)

The most relevant features for the model were analyzed to understand which variables contribute most significantly to predictions.

As features mais relevantes para o modelo foram analisadas para entender quais variáveis contribuem mais significativamente nas previsões.

---

## 🔐 Version Management with Git and GitHub | Gerenciamento de Versões com Git e GitHub

The project uses **Git** for version control and is hosted on **GitHub**.

O projeto utiliza **Git** para controle de versão e é hospedado no **GitHub**.

### 🗂️ Why Git LFS? | Por que Git LFS?

The `creditcard.csv` file (150.8 MB) **exceeds GitHub's 100 MB limit** for individual files. We use **Git Large File Storage** to:

O arquivo `creditcard.csv` (150.8 MB) **excede o limite de 100 MB** do GitHub para arquivos individuais. Utilizamos **Git Large File Storage** para:

- ✅ Store large files efficiently | Armazenar arquivos grandes eficientemente
- ✅ Maintain version history | Manter histórico de versões
- ✅ Facilitate collaboration between developers | Facilitar colaboração entre desenvolvedores

---

## 🚀 How to Run the Project | Como Executar o Projeto

### 📝 Prerequisites | Pré-requisitos

- Python 3.8+
- Git with Git LFS
- Jupyter Notebook or Google Colab

### 📥 Installation and Execution | Instalação e Execução

```bash
# 1. Clone the repository | Clone o repositório
git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git
cd fraud-detection-credit-card

# 2. Configure Git LFS | Configure Git LFS
git lfs install
git lfs pull

# 3. Create a virtual environment (optional, but recommended)
# Crie um ambiente virtual (opcional, mas recomendado)
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# 4. Install dependencies | Instale as dependências
pip install -r requirements.txt

# Or install individually | Ou instale individualmente:
pip install pandas scikit-learn matplotlib seaborn imbalanced-learn jupyter

# 5. Run Jupyter Notebook | Execute o Jupyter Notebook
jupyter notebook

# 6. Open the main notebook and run the cells
# Abra o notebook principal e execute as células
```

### ☁️ Alternative: Google Colab | Alternativa: Google Colab

1. Access [Google Colab](https://colab.research.google.com)
2. Open the notebook from the repository
3. Run the cells sequentially

---

## 📦 Dependencies | Dependências

```
pandas==1.5.0
scikit-learn==1.2.0
matplotlib==3.6.0
seaborn==0.12.0
imbalanced-learn==0.10.0
jupyter==1.0.0
```

---

## 📁 Repository Structure | Estrutura do Repositório

```
fraud-detection-credit-card/
├── 📓 notebook.ipynb           # Main notebook with complete analysis
├── 📄 README.md                # This file
├── 📊 creditcard.csv           # Dataset (Git LFS)
├── 📋 requirements.txt         # Project dependencies
└── 🔧 .gitattributes          # Git LFS configuration
```

---

## 🎓 Key Learnings | Aprendizados Principais

- ✅ Handling imbalanced data with SMOTE | Tratamento de dados desbalanceados com SMOTE
- ✅ Comparison between models (Logistic Regression vs Random Forest) | Comparação entre modelos (Regressão Logística vs Random Forest)
- ✅ Evaluation using appropriate metrics (Recall, Precision, ROC AUC) | Avaliação usando métricas apropriadas (Recall, Precision, ROC AUC)
- ✅ Git LFS implementation for large files | Implementação de Git LFS para arquivos grandes
- ✅ Version control best practices and documentation | Boas práticas de versionamento e documentação

---

## 📞 Contact & Contributions | Contato & Contribuições

**Author:** [lincolnbuk](https://github.com/lincolnbuk)

If you find issues or have improvement suggestions, feel free to:

Se você encontrar problemas ou tiver sugestões de melhorias, sinta-se livre para:

- 🐛 Open an [issue](https://github.com/lincolnbuk/fraud-detection-credit-card/issues) | Abrir uma [issue](https://github.com/lincolnbuk/fraud-detection-credit-card/issues)
- 🔄 Submit a [pull request](https://github.com/lincolnbuk/fraud-detection-credit-card/pulls) | Enviar um [pull request](https://github.com/lincolnbuk/fraud-detection-credit-card/pulls)

---

## 📜 License | Licença

This project is licensed under the MIT License - see the LICENSE file for details.

Este projeto está licenciado sob a MIT License - veja o arquivo LICENSE para detalhes.

---

<div align="center">
  <p><strong>⭐ If this project was useful, consider leaving a star! | Se este projeto foi útil, considere deixar uma estrela! ⭐</strong></p>
  <p>Made with ❤️ by <a href="https://github.com/lincolnbuk">lincolnbuk</a></p>
</div>
