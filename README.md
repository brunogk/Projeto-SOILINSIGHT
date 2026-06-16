# 🌱 SoilInsight
### Classificação e Agrupamento de Solos com Machine Learning para Recomendação de Culturas

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-1.3+-orange?logo=scikit-learn&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00?logo=tensorflow&logoColor=white)
![Colab](https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?logo=googlecolab&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completo-brightgreen)

---

## Sobre o projeto

SoilInsight é um projeto de portfólio em Ciência de Dados que aplica técnicas de Machine Learning para recomendar culturas agrícolas com base em variáveis edafoclimáticas — nitrogênio (N), fósforo (P), potássio (K), pH do solo, temperatura, umidade e precipitação.

O projeto foi desenvolvido com o diferencial de unir conhecimento técnico em ciência do solo e agronomia à análise de dados, tornando cada etapa interpretável do ponto de vista agronômico — não apenas computacional.

---

## Contexto agronômico

Cada variável do dataset tem relevância biológica direta:

| Variável | Significado agronômico |
|---|---|
| N — Nitrogênio | Componente de aminoácidos, clorofila e ATP. Essencial para crescimento vegetativo |
| P — Fósforo | Fundamental para desenvolvimento radicular, floração e síntese de DNA |
| K — Potássio | Regula abertura estomática e transporte de fotoassimilados |
| pH | Controla a disponibilidade de nutrientes e a atividade da microbiota do solo |
| Temperatura | Afeta metabolismo, germinação e incidência de patógenos |
| Umidade | Interfere na transpiração e no desenvolvimento de doenças fúngicas |
| Precipitação | Define disponibilidade hídrica e risco de lixiviação de nutrientes |

---

## Dataset

**Crop Recommendation Dataset** — disponível no [Kaggle](https://www.kaggle.com/datasets/atharvaingle/crop-recommendation-dataset)

- 2.200 registros | 7 features | 22 culturas
- Dataset balanceado: 100 registros por cultura
- Variável-alvo: cultura recomendada (classificação multiclasse)

---

## Estrutura do projeto

```
soilinsight/
├── notebook/
│   └── SoilInsight.ipynb        ← notebook principal (Google Colab)
├── data/
│   └── crop_recommendation.csv  ← dataset
├── figures/
│   └── *.png                    ← gráficos exportados
└── README.md
```

---

## Metodologia

O projeto foi estruturado em três frentes complementares:

### 1. Análise Exploratória de Dados (EDA)
- Distribuição de cada variável edafoclimática
- Correlação entre nutrientes do solo
- Perfil nutricional médio (N, P, K, pH) por cultura
- Boxplot de pH por cultura com faixas de referência agronômica

### 2. Aprendizado Supervisionado — Classificação
Dois modelos foram treinados, avaliados e comparados:

**Random Forest**
- 100 estimadores na versão base
- Tuning via `RandomizedSearchCV` (30 iterações, cross-validation 5 folds)
- Hiperparâmetros otimizados: `n_estimators`, `max_depth`, `min_samples_split`, `min_samples_leaf`, `max_features`

**Rede Neural Densa (Keras/TensorFlow)**
- Arquitetura fully connected: 128 → 64 → 32 → 22 neurônios
- Dropout para regularização (0.3 e 0.2)
- Ativação ReLU nas camadas ocultas, Softmax na saída
- Tuning via `RandomizedSearchCV` com `scikeras` (10 iterações, CV 3 folds)
- Hiperparâmetros otimizados: neurônios por camada, dropout, otimizador, batch size, épocas

### 3. Aprendizado Não Supervisionado — Agrupamento
- K-Means sobre variáveis exclusivamente edafológicas (N, P, K, pH)
- Escolha de K pelo Método Elbow + Silhouette Score
- Visualização dos clusters em 2D com PCA
- Nomeação agronômica dos clusters com base no perfil nutricional médio

---

## Resultados

| Modelo | Acurácia (%) | Tuning |
|---|---|---|
| Random Forest — padrão | ~99.0 | Não |
| Random Forest — tunado | ~99.3 | RandomizedSearchCV |
| Rede Neural — padrão | ~97.5 | Não |
| Rede Neural — tunada | ~98.5 | RandomizedSearchCV |

> Valores de referência. Os resultados exatos dependem do ambiente de execução.

**Silhouette Score K-Means (K=4):** ~0.45

---

## Principais conclusões

- Random Forest apresentou desempenho superior e maior estabilidade para dados tabulares com 2.200 registros, sendo menos sensível à escolha de hiperparâmetros do que a rede neural.
- A rede neural beneficiou-se mais do processo de tuning, com ganho mais expressivo após otimização.
- O agrupamento K-Means revelou perfis de solo distintos que correspondem biologicamente a grupos de culturas com demandas nutricionais similares — resultado que só pode ser interpretado adequadamente com conhecimento agronômico.
- A variável pH apresentou a maior variação entre clusters, confirmando seu papel central na disponibilidade de nutrientes para diferentes culturas.

---

## Simulação de campo

O notebook inclui uma célula de simulação que recebe variáveis de um solo hipotético (como um talhão no Paraná) e retorna:
- Cultura recomendada pelo Random Forest tunado e pela Rede Neural tunada
- Top 3 culturas mais prováveis com probabilidades
- Cluster de solo ao qual o perfil nutricional pertence

---

## Tecnologias utilizadas

- **Python 3.10+**
- **Pandas / NumPy** — manipulação e análise de dados
- **Matplotlib / Seaborn** — visualização
- **Scikit-learn** — Random Forest, K-Means, PCA, métricas, tuning
- **TensorFlow / Keras** — rede neural densa
- **scikeras** — integração Keras + scikit-learn para tuning
- **Google Colab** — ambiente de desenvolvimento

---

## Como executar

1. Acesse o notebook no Google Colab
2. Execute as células em sequência
3. O dataset é carregado automaticamente via URL pública — nenhuma instalação adicional necessária além das células de `!pip install`

---

## Autor

**Bruno** — Doutorando em Ciências do Solo (UFPR) em transição para Ciência de Dados.
Combinando expertise em biologia e agronomia com análise de dados e machine learning.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Conectar-0A66C2?logo=linkedin&logoColor=white)](https://linkedin.com/in/seu-perfil)
[![GitHub](https://img.shields.io/badge/GitHub-Portfólio-181717?logo=github&logoColor=white)](https://github.com/seu-usuario)

---
