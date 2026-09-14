# Projeto de Machine Learning — Predição de AVC (Stroke)

**APS1 — Análise Exploratória de Dados (EDA)**

- **Integrantes:** Adrielle Gabriel Santana, Oscar Rodrigues de Sousa Filho
- **Curso:** Bacharelado em Ciência da Computação — 4º Semestre
- **Data de entrega:** 14/09/2026
- **Dataset:** [Stroke Prediction Dataset (Kaggle)](https://www.kaggle.com/datasets/fedesoriano/stroke-prediction-dataset)
- **Tarefa da APS2:** Classificação (prever a variável `stroke`)

## Sobre o projeto

Este site documenta a etapa de EDA do pipeline de Machine Learning aplicado ao
*Stroke Prediction Dataset*, cujo objetivo final (APS2) é classificar se um
paciente sofrerá ou não um AVC (Acidente Vascular Cerebral) a partir de dados
demográficos e clínicos.

Nesta primeira etapa, realizamos:

1. Carregamento e inspeção inicial dos dados (estrutura, tipos, ausentes, balanceamento de classes).
2. Análise univariada (estatísticas descritivas, histogramas, boxplots, gráficos de barras).
3. Análise bivariada e multivariada (correlações, scatter plots, boxplots conjuntos, taxas de AVC por categoria).
4. Definição e justificativa das estratégias de pré-processamento (ausentes, outliers, encoding, escala) e construção de um `Pipeline`/`ColumnTransformer` do scikit-learn, além de uma visualização via PCA.
5. Consolidação dos principais achados e próximos passos para a etapa de classificação (APS2).

## Navegação

- [Notebook completo da EDA](notebooks/eda-stroke.ipynb) — código, gráficos e análises, célula a célula.
- [Principais achados](achados.md) — resumo executivo dos resultados e decisões de pré-processamento.

## Referências

- FEDESORIANO. *Stroke Prediction Dataset*. Kaggle, 2021.
- PEDREGOSA, F. et al. *Scikit-learn: Machine Learning in Python*. JMLR 12, 2011.
- MCKINNEY, W. *Data Structures for Statistical Computing in Python*. SciPy, 2010 (pandas).
- WASKOM, M. *seaborn: statistical data visualization*. JOSS, 2021.
