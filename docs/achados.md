# Principais achados e estratégias de pré-processamento

## Resumo dos achados da EDA

1. **Estrutura dos dados:** 5110 instâncias e 12 colunas (11 features + `id` + target `stroke`), sendo 3 numéricas contínuas (`age`, `avg_glucose_level`, `bmi`), 5 categóricas nominais/binárias em texto, e 2 binárias já numéricas (`hypertension`, `heart_disease`).
2. **Qualidade dos dados:** único campo com ausentes é `bmi` (~4%). Não há duplicatas relevantes nem valores fora de faixa fisiológica em `age`, `avg_glucose_level` ou `bmi`. Há uma única linha com `gender = 'Other'`, categoria muito rara.
3. **Desbalanceamento severo do target:** apenas ~4,9% dos pacientes sofreram AVC (`stroke=1`), o que é o principal desafio para a etapa de classificação (APS2) — métricas como acurácia serão enganosas; deve-se priorizar recall/F1/AUC-ROC para a classe minoritária.
4. **Relações com o target:** `age` é a variável com maior correlação com `stroke`, seguida de `avg_glucose_level` e `heart_disease`/`hypertension`. Categoricamente, pacientes `ever_married='Yes'`, com `work_type` fora de `children`/`Never_worked`, e ex-fumantes (`formerly smoked`) apresentam taxas de AVC mais altas — coerente com o fato de essas categorias estarem associadas a faixas etárias mais avançadas.
5. **Separabilidade:** o PCA em 2D não mostrou separação linear clara entre as classes, indicando que modelos não-lineares tendem a performar melhor na APS2.

## Estratégias de pré-processamento propostas

| Etapa | Estratégia | Justificativa |
| --- | --- | --- |
| Valores ausentes (`bmi`) | Imputação pela mediana | Robusta a outliers, preserva todas as linhas (inclusive casos positivos raros) |
| Outliers (`bmi`, `avg_glucose_level`) | Manter, sem remoção | Valores extremos são clinicamente relevantes como fatores de risco |
| Encoding categórico | One-Hot Encoding | Variáveis nominais sem ordem natural |
| Normalização | StandardScaler | Necessário para PCA e modelos sensíveis à escala; menos afetado por outliers que Min-Max |
| Dimensionalidade | PCA (visualização exploratória) | Investigar separabilidade das classes; não substitui as features originais na modelagem |
| Split treino/teste | 80/20 estratificado por `stroke` | Mantém a proporção da classe minoritária em ambos os conjuntos |

## Próximos passos (APS2)

- Tratar o desbalanceamento de classes (ex.: `class_weight='balanced'`, SMOTE, ajuste de threshold de decisão).
- Testar modelos não-lineares (Random Forest, Gradient Boosting) além de baseline linear (Regressão Logística).
- Reutilizar o `ColumnTransformer` construído na EDA dentro de um `Pipeline` de modelagem completo.
- Avaliar com métricas adequadas ao desbalanceamento: recall, F1-score e AUC-ROC/PR-AUC, não apenas acurácia.

Veja o [notebook completo](notebooks/eda-stroke.ipynb) para o código, gráficos e a análise célula a célula.
