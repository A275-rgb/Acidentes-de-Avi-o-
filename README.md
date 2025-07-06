# Análise Exploratória e Modelagem de Ocorrências Aeronáuticas no Brasil 🛫🌍

Este projeto realiza uma análise completa das ocorrências aeronáuticas registradas no Brasil com base em dados geoespaciais, categóricos e temporais, com foco na visualização, tratamento e modelagem preditiva em produção.

---

## 🔍 Etapas do Projeto

### 1. Carregamento e Visualização Geográfica Inicial

Utilizamos os campos `ocorrencia_latitude` e `ocorrencia_longitude` para mapear a distribuição espacial das ocorrências.

```python
sns.scatterplot(data=dt, x='ocorrencia_longitude', y='ocorrencia_latitude', hue='ocorrencia_uf')
```

![Scatter Latitude vs Longitude](imagens/scatter_lat_lon.png)

---

### 2. Distribuição de Ocorrências por Estado (UF)

```python
sns.barplot(x=ocorrencias_por_uf.index, y=ocorrencias_por_uf.values)
```

![Barplot por UF](imagens/barplot_ocorrencias_uf.png)

---

### 3. Distribuição Espacial por Classificação da Ocorrência

```python
sns.scatterplot(data=dt, x='ocorrencia_longitude', y='ocorrencia_latitude', hue='ocorrencia_classificacao')
```

![Scatter por Classificacao](imagens/scatter_classificacao.png)

---

### 4. Densidade Geográfica por Tipo de Ocorrência

```python
sns.kdeplot(x=subset['ocorrencia_longitude'], y=subset['ocorrencia_latitude'], fill=True)
```

![KDE Plot](imagens/kde_classificacao.png)

---

### 5. Mapa Interativo com Folium

```python
folium.Map(location=[-15.7797, -47.9297], zoom_start=4)
```

O mapa interativo foi salvo como:

```
mapa_ocorrencias.html
```

---

## 🪤 Modelagem Preditiva

Utilizamos um pipeline completo com `RandomForestClassifier` para prever a `ocorrencia_classificacao` com base em variáveis geográficas e categóricas.

### Etapas:

* Separar `X` e `y`
* Pré-processamento com `ColumnTransformer`
* Pipeline com `Pipeline`
* Treinamento e avaliação do modelo

### Métricas do Modelo:

```python
print(classification_report(y_test, y_pred))
```

### Matriz de Confusão:

```python
ConfusionMatrixDisplay.from_estimator(...)
```

![Matriz de Confusão](imagens/matriz_confusao.png)

---

### 🔢 Exportação do Modelo

```python
joblib.dump(clf_pipeline, 'modelo_ocorrencias_pipeline.joblib')
```

---

## 🚀 Como Executar

1. Instale dependências:

```bash
pip install -r requirements.txt
```

2. Execute o notebook `analise_modelagem_ocorrencias.ipynb`

3. Visualize os gráficos na pasta `/imagens` e o mapa interativo em `mapa_ocorrencias.html`

---

## 📄 Arquivos no Repositório

| Arquivo                               | Descrição                              |
| ------------------------------------- | -------------------------------------- |
| `analise_modelagem_ocorrencias.ipynb` | Notebook principal com EDA e modelagem |
| `modelo_ocorrencias_pipeline.joblib`  | Modelo treinado salvo para produção    |
| `mapa_ocorrencias.html`               | Mapa interativo das ocorrências        |
| `/imagens/*.png`                      | Gráficos gerados durante a análise     |

---

## 📊 Possíveis Melhorias

* Explorar outros modelos (XGBoost, SVM, etc.)
* Incluir tempo entre ocorrência e liberação da aeronave
* Hospedar o modelo com FastAPI

---

## 😎 Autor

Desenvolvido por \Gabriel Araujo como parte de um projeto de análise geoespacial e aprendizado de máquina.

---

> Este projeto é parte de um estudo analítico completo envolvendo visualização, tratamento e modelagem preditiva com dados reais de ocorrências aeronáuticas.
