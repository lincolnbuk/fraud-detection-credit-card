# 🛡️ Detecção de Fraude em Cartões de Crédito

![Fraud Detection](https://img.shields.io/badge/Machine%20Learning-Credit%20Card%20Fraud%20Detection-blue?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.8%2B-yellow?style=for-the-badge)

<div align="center">
  <img src="https://images.unsplash.com/photo-1557821552-17105176677c?w=800&q=80" alt="Fraud Detection" width="100%" style="border-radius: 10px; margin: 20px 0;">
  <p><i>Protegendo transações financeiras com Machine Learning</i></p>
</div>

---

## 📋 Visão Geral do Projeto

Este projeto implementa um **modelo de detecção de fraude** para transações de cartão de crédito, utilizando técnicas avançadas de aprendizado de máquina e um dataset real com mais de 280 mil transações.

### 🎯 Objetivos Principais

- ✅ Analisar e pré-processar dataset de transações de cartão de crédito
- ✅ Lidar com o severo desbalanceamento de classes (fraude vs legítima)
- ✅ Treinar e avaliar modelos de classificação de alto desempenho
- ✅ Implementar Git Large File Storage (Git LFS) para arquivos grandes
- ✅ Publicar projeto profissional no GitHub

---

## 📊 Dataset

O dataset utilizado é o **`creditcard.csv`**, uma base de dados real proveniente do Kaggle (`mlg-ulb/creditcardfraud`).

### 📁 Informações do Arquivo

| Propriedade | Detalhes |
|:---|:---|
| **Localização** | [creditcard.csv](https://github.com/lincolnbuk/fraud-detection-credit-card/blob/main/creditcard.csv) |
| **Tamanho** | ~150.8 MB |
| **Armazenamento** | 🗄️ Git LFS (Large File Storage) |
| **Formato** | CSV |
| **Registros** | 284.807 transações |
| **Colunas** | 31 (Time, V1-V28, Amount, Class) |
| **Período** | Duas dias de transações reais |

### 🔧 Como Acessar o Arquivo

```bash
# 1. Clone o repositório com Git LFS
git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git
cd fraud-detection-credit-card

# 2. Instale o Git LFS (se necessário)
git lfs install

# 3. Baixe o arquivo grande
git lfs pull

# 4. Acesse o arquivo localmente
# O arquivo estará disponível em: ./creditcard.csv
```

> ⚠️ **Nota:** O arquivo não pode ser visualizado na interface web do GitHub devido ao seu tamanho, mas está completamente acessível após o clone com Git LFS.

---

## 🔍 Análise Exploratória de Dados (EDA) e Pré-processamento

### 📈 Principais Observações

| Observação | Detalhes |
|:---|:---|
| **Valores Nulos** | ✅ Sem valores nulos em nenhuma coluna |
| **Features PCA** | Colunas V1-V28 já escaladas e transformadas via PCA |
| **Classe Desbalanceada** | 🔴 Vasta maioria não fraudulenta (Classe 0) vs. fraudes raras (Classe 1) |
| **Target Distribution** | ~0.17% de transações fraudulentas |

### ⚙️ Etapas de Pré-processamento

1. **Escalamento de Features**
   - `Time` e `Amount` escaladas com `StandardScaler`
   - Alignamento com escala das features PCA

2. **Divisão de Dados**
   - Separação em features (X) e target (y)
   - Split treino/teste com `stratify=y`
   - Mantém proporção original de classes

3. **Tratamento de Desbalanceamento**
   - 🔧 **SMOTE (Synthetic Minority Over-sampling Technique)**
   - Aplicado **exclusivamente** ao conjunto de treino
   - Evita data leakage no conjunto de teste

---

## 🤖 Modelagem e Avaliação

Dois modelos de classificação foram explorados e comparados:

### 1️⃣ Regressão Logística (Baseline)

```
┌─────────────────────────────────────────┐
│ REGRESSÃO LOGÍSTICA                     │
├─────────────────────────────────────────┤
│ ROC AUC Score:  0.9659  ⭐⭐⭐⭐⭐      │
│ Recall (Fraude): 0.88   (Sensibilidade) │
│ Precision:       0.06   (Baixa)         │
│ Status:          ⚠️ Muitos falsos +      │
└─────────────────────────────────────────┘
```

**Análise:**
- ✅ Identifica maioria das fraudes (recall alto)
- ❌ Marca muitas transações legítimas como fraude (muitos falsos positivos)
- 💭 Menos adequado para aplicação prática

---

### 2️⃣ Random Forest Classifier ⭐

```
┌─────────────────────────────────────────┐
│ RANDOM FOREST                           │
├─────────────────────────────────────────┤
│ ROC AUC Score:  0.9489  ⭐⭐⭐⭐        │
│ Recall (Fraude): 0.78   (Bom)           │
│ Precision:       0.86   (Excelente!) ✨ │
│ Status:          ✅ Modelo Recomendado  │
└─────────────────────────────────────────┘
```

**Análise:**
- ✅ Melhor equilíbrio Precision × Recall
- ✅ Menos falsos positivos
- ✅ Mais adequado para produção
- 🏆 **Modelo selecionado para deploy**

---

### 📊 Análise de Importância das Features (Random Forest)

As features mais relevantes para o modelo foram analisadas para entender quais variáveis contribuem mais significativamente nas previsões.

---

## 🔐 Gerenciamento de Versões com Git e GitHub

O projeto utiliza **Git** para controle de versão e é hospedado no **GitHub**.

### 🗂️ Por que Git LFS?

O arquivo `creditcard.csv` (150.8 MB) **excede o limite de 100 MB** do GitHub para arquivos individuais. Utilizamos **Git Large File Storage** para:
- ✅ Armazenar arquivos grandes eficientemente
- ✅ Manter histórico de versões
- ✅ Facilitar colaboração entre desenvolvedores

---

## 🚀 Como Executar o Projeto

### 📝 Pré-requisitos

- Python 3.8+
- Git com Git LFS
- Jupyter Notebook ou Google Colab

### 📥 Instalação e Execução

```bash
# 1. Clone o repositório
git clone https://github.com/lincolnbuk/fraud-detection-credit-card.git
cd fraud-detection-credit-card

# 2. Configure Git LFS
git lfs install
git lfs pull

# 3. Crie um ambiente virtual (opcional, mas recomendado)
python -m venv venv
source venv/bin/activate  # No Windows: venv\Scripts\activate

# 4. Instale as dependências
pip install -r requirements.txt

# Ou instale individualmente:
pip install pandas scikit-learn matplotlib seaborn imbalanced-learn jupyter

# 5. Execute o Jupyter Notebook
jupyter notebook

# 6. Abra o notebook principal e execute as células
```

### ☁️ Alternativa: Google Colab

1. Acesse [Google Colab](https://colab.research.google.com)
2. Abra o notebook do repositório
3. Execute as células sequencialmente

---

## 📦 Dependências

```
pandas==1.5.0
scikit-learn==1.2.0
matplotlib==3.6.0
seaborn==0.12.0
imbalanced-learn==0.10.0
jupyter==1.0.0
```

---

## 📁 Estrutura do Repositório

```
fraud-detection-credit-card/
├── 📓 notebook.ipynb           # Notebook principal com análise completa
├── 📄 README.md                # Este arquivo
├── 📊 creditcard.csv           # Dataset (Git LFS)
├── 📋 requirements.txt         # Dependências do projeto
└── 🔧 .gitattributes          # Configuração do Git LFS
```

---

## 🎓 Aprendizados Principais

- ✅ Tratamento de dados desbalanceados com SMOTE
- ✅ Comparação entre modelos (Regressão Logística vs Random Forest)
- ✅ Avaliação usando métricas apropriadas (Recall, Precision, ROC AUC)
- ✅ Implementação de Git LFS para arquivos grandes
- ✅ Boas práticas de versionamento e documentação

---

## 📞 Contato & Contribuições

**Autor:** [lincolnbuk](https://github.com/lincolnbuk)

Se você encontrar problemas ou tiver sugestões de melhorias, sinta-se livre para:
- 🐛 Abrir uma [issue](https://github.com/lincolnbuk/fraud-detection-credit-card/issues)
- 🔄 Enviar um [pull request](https://github.com/lincolnbuk/fraud-detection-credit-card/pulls)

---

## 📜 Licença

Este projeto está licenciado sob a MIT License - veja o arquivo LICENSE para detalhes.

---

<div align="center">
  <p><strong>⭐ Se este projeto foi útil, considere deixar uma estrela! ⭐</strong></p>
  <p>Made with ❤️ by <a href="https://github.com/lincolnbuk">lincolnbuk</a></p>
</div>
