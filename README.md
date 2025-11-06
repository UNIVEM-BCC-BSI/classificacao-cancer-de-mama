# 🩺 Classificação do Câncer de Mama (Kaggle Mini Project)

Este projeto foi desenvolvido como parte do **Miniprojeto Kaggle 1 – Classificação de Câncer de Mama**, do curso de Big Data Analytics.  
O objetivo é aplicar técnicas de **Aprendizado de Máquina supervisionado** para prever se um tumor é **maligno (M)** ou **benigno (B)** com base em diversas características extraídas de imagens de nódulos mamários.

📊 **Competição Kaggle:**  
[Breast Cancer Classification – Prototype Fall 2025](https://www.kaggle.com/competitions/breast-cancer-classification-prototype-fall-2025)

---

## 🧠 Objetivo

Treinar, comparar e selecionar o modelo de **classificação binária** mais eficaz para prever o diagnóstico de câncer de mama.  
O modelo final deve gerar um arquivo `submission.csv` no formato exigido pelo Kaggle:

```
id,label
906564,B
85715,M
...
```

A métrica de avaliação utilizada é a **acurácia (Accuracy)**.

---

## 📂 Estrutura do Projeto

```
breast-cancer-classification/
│
├── data/
│   ├── train.csv
│   ├── test.csv
│   ├── sample_submission.csv
│
├── classificacao_de_cancer_de_mama.ipynb           ← código principal
├── submission.csv           ← arquivo gerado após previsão
└── README.md                ← documentação do projeto
```

---

## 🔍 Metodologia (Etapas do Processo KDD)

### 1. Exploração de Dados
- Carregamento dos conjuntos `train.csv` e `test.csv`.
- Verificação de valores ausentes, tipos de dados e estatísticas descritivas.
- Análise da distribuição da variável-alvo (`label`), composta por:
  - **B (Benigno)** – 285 amostras  
  - **M (Maligno)** – 170 amostras

### 2. Pré-processamento e Engenharia de Atributos
- Codificação da variável alvo (`M=1`, `B=0`).
- Remoção da coluna `id` (não informativa para o modelo).
- Padronização dos atributos com `StandardScaler`.

### 3. Treinamento e Avaliação dos Modelos
Foram testados os seguintes classificadores:

| Modelo | Acurácia (validação) |
|--------|----------------------|
| Perceptron | 0.9451 |
| Logistic Regression | **1.0000** |
| SVM | 0.9890 |
| Decision Tree | 0.9341 |
| KNN | 0.9890 |
| Random Forest | 0.9451 |

A regressão logística apresentou desempenho perfeito no conjunto de validação, porém, para evitar **overfitting**, foi selecionado o **SVM** como modelo final, por demonstrar alta acurácia e melhor generalização.

### 4. Ajuste Fino (Grid Search)
Um `GridSearchCV` foi aplicado ao modelo SVM, resultando nos seguintes parâmetros ótimos:

```python
{'C': 0.1, 'gamma': 'scale', 'kernel': 'linear'}
```

A acurácia média obtida durante o *cross-validation* foi de **0.9736**.

### 5. Geração do Arquivo de Submissão
O modelo final foi aplicado ao conjunto de teste e as previsões foram salvas em `submission.csv`, no formato solicitado pela competição Kaggle.

---

## 🧾 Conclusões

- O conjunto de dados é bem linearmente separável, favorecendo modelos lineares como **Regressão Logística** e **SVM**.  
- O modelo **SVM com kernel linear** apresentou excelente desempenho e robustez, sendo utilizado para a submissão final.  
- A metodologia seguiu as boas práticas do processo KDD: análise, pré-processamento, modelagem, avaliação e implantação.

---

## ⚙️ Tecnologias Utilizadas
- Python 3.10+  
- Pandas  
- Scikit-learn  
- NumPy  
- Matplotlib / Seaborn  
- Google Colab / VSCode

---

## 📈 Resultados
- Acurácia média em validação cruzada: **97.36%**
- Modelo final: **SVM (kernel linear, C=0.1)**  
- Arquivo gerado: `submission.csv`

---

## 📚 Referências

- [Kaggle Competition – Breast Cancer Classification Prototype Fall 2025](https://www.kaggle.com/competitions/breast-cancer-classification-prototype-fall-2025)
- [Breast Cancer Wisconsin (Diagnostic) Dataset – UCI Repository](https://www.kaggle.com/datasets/uciml/breast-cancer-wisconsin-data)