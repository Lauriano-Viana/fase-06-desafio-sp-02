# 🌾 Previsão de Produtividade Agrícola com NDVI e Imagens de Satélite

## 📌 Objetivo

Este projeto visa prever a **produtividade agrícola** de determinada região utilizando imagens de satélite e análise de NDVI (Normalized Difference Vegetation Index), em conjunto com dados temporais e anomalias de vegetação, para orientar decisões no campo.

---

## 🧩 Pipeline do Projeto

1. **Coleta e Processamento de Dados**
   - Download de imagens de satélite de 2020 a 2024.
   - Fatiamento em patches de 256x256 px.
   - Conversão para PNG e organização em diretórios por ano.

2. **Extração de Métricas**
   - Cálculo de NDVI médio por patch.
   - Integração com dados históricos do SATVeg (.xls).
   - Cálculo de anomalias (desvios da média histórica).

3. **Criação de Dataset**
   - Geração do `patches_enriched.csv` contendo:
     - Nome do patch
     - Ano
     - NDVI médio
     - NDVI médio e desvio padrão do SATVeg
     - Anomalia de NDVI
     - Rótulo (ex: presença ou não de produtividade)

4. **Modelagem**
   - Separação dos dados em treino/teste (80/20).
   - Modelo escolhido: Random Forest Regressor.
   - Avaliação com R², RMSE e MAE.

---

## 📊 Análise Exploratória e Seleção de Variáveis

### 🔍 Variáveis Utilizadas no Modelo

| Variável             | Justificativa                                                                 |
|----------------------|--------------------------------------------------------------------------------|
| `mean_ndvi`          | Relaciona-se diretamente ao vigor vegetativo, essencial para prever produtividade. |
| `year`               | Considera variações interanuais por clima ou manejo agrícola.                    |

### ❌ Variáveis inicialmente descartadas

- `ndvi_anomaly`: Possui relação interessante, mas foi testada em modelos separados para evitar multicolinearidade com o NDVI.
- `mean_ndvi_satveg`: Tem valor agregado, mas está muito correlacionado com `mean_ndvi`.

> **Justificativa da seleção**: Priorizamos simplicidade e variáveis diretamente observadas nos patches. Isso facilita escalabilidade para outras regiões e evita sobreajuste com variáveis fortemente correlacionadas.

---

## 🤖 Escolha do Modelo

### 🔎 Modelo: `RandomForestRegressor`

- **Justificativa**:
  - Funciona bem com poucos dados e variáveis.
  - Robusto contra overfitting.
  - Explicável: permite entender a importância de cada variável.
  - Insensível a outliers e normalizações.

- **Lógica preditiva**:
  O modelo aprende padrões não-lineares entre NDVI médio e produtividade. Por exemplo, um valor elevado de NDVI em um determinado ano é um bom indicativo de uma boa safra, e o modelo consegue capturar essas relações com múltiplas árvores de decisão.

---

## 📉 Avaliação do Modelo
- **R²:**   -0.66
- **RMSE:**  87.33
- **MAE:**   74.93

### 🎯 Gráfico de Predição
> A boa aderência dos pontos à linha diagonal indica forte capacidade preditiva.

---

## 📈 NDVI por Ano e Comparação com SATVeg

As anomalias de NDVI ajudam a identificar períodos críticos como seca, estresse nutricional ou problemas de plantio.

---

## 🔍 Insights Obtidos

1. NDVI é um bom indicador de produtividade em áreas agrícolas.
2. O ano agrícola influencia fortemente o desempenho (efeito climático).
3. Anomalias de NDVI ajudam a identificar áreas com risco produtivo.
4. Modelos simples (como Random Forest) podem fornecer boas previsões com variáveis bem selecionadas.

---
---
🔗 Links

[COLAB](https://colab.research.google.com/drive/1IJUxYicMDRHq3Yq6RKdoV3tIdMkE7E0u?usp=sharing)

[YOUTUBE](https://youtu.be/qjhEYKCYnbU)


---

## 👨‍💻 Desenvolvido por

Lauriano – Estudante FIAP | Engenharia de Machine Learning  
