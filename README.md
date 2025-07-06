Análise Exploratória e Modelagem de Ocorrências Aeronáuticas no Brasil 🛫🌍
Este projeto realiza uma análise completa das ocorrências aeronáuticas registradas no Brasil com base em dados geoespaciais, categóricos e temporais, com foco na visualização, tratamento e modelagem preditiva em produção.
________________________________________
🔍 Etapas do Projeto
1. Carregamento e Visualização Geográfica Inicial
Utilizamos os campos ocorrencia_latitude e ocorrencia_longitude para mapear a distribuição espacial das ocorrências.
 
sns.scatterplot(data=dt, x='ocorrencia_longitude', y='ocorrencia_latitude', hue='ocorrencia_uf')
Scatter Latitude vs Longitude
Scatter Latitude vs Longitude
________________________________________
2. Distribuição de Ocorrências por Estado (UF)

 
sns.barplot(x=ocorrencias_por_uf.index, y=ocorrencias_por_uf.values)
Barplot por UF
Barplot por UF
________________________________________
3. Distribuição Espacial por Classificação da Ocorrência
 
sns.scatterplot(data=dt, x='ocorrencia_longitude', y='ocorrencia_latitude', hue='ocorrencia_classificacao')
Scatter por Classificacao
Scatter por Classificacao
________________________________________
4. Densidade Geográfica por Tipo de Ocorrência
 
sns.kdeplot(x=subset['ocorrencia_longitude'], y=subset['ocorrencia_latitude'], fill=True)
KDE Plot
KDE Plot
________________________________________
5. Mapa Interativo com Folium
 
folium.Map(location=[-15.7797, -47.9297], zoom_start=4)
O mapa interativo foi salvo como:
mapa_ocorrencias.html
________________________________________
🪤 Modelagem Preditiva
Utilizamos um pipeline completo com RandomForestClassifier para prever a ocorrencia_classificacao com base em variáveis geográficas e categóricas.
Etapas:
•	Separar X e y
•	Pré-processamento com ColumnTransformer
•	Pipeline com Pipeline
•	Treinamento e avaliação do modelo
Métricas do Modelo:
print(classification_report(y_test, y_pred))
Matriz de Confusão:
ConfusionMatrixDisplay.from_estimator(...)
Matriz de Confusão
Matriz de Confusão
________________________________________
🔢 Exportação do Modelo
joblib.dump(clf_pipeline, 'modelo_ocorrencias_pipeline.joblib')
________________________________________
🚀 Como Executar
1.	Instale dependências:
pip install -r requirements.txt
2.	Execute o notebook analise_modelagem_ocorrencias.ipynb
3.	Visualize os gráficos na pasta /imagens e o mapa interativo em mapa_ocorrencias.html
________________________________________
📄 Arquivos no Repositório
Arquivo	Descrição
analise_modelagem_ocorrencias.ipynb	Notebook principal com EDA e modelagem
modelo_ocorrencias_pipeline.joblib	Modelo treinado salvo para produção
mapa_ocorrencias.html	Mapa interativo das ocorrências
/imagens/*.png	Gráficos gerados durante a análise
________________________________________
📊 Possíveis Melhorias
•	Explorar outros modelos (XGBoost, SVM, etc.)
•	Incluir tempo entre ocorrência e liberação da aeronave
•	Hospedar o modelo com FastAPI
________________________________________


## 😎 Autor

Desenvolvido por \Gabriel Araujo como parte de um projeto de análise geoespacial e aprendizado de máquina.

---

> Este projeto é parte de um estudo analítico completo envolvendo visualização, tratamento e modelagem preditiva com dados reais de ocorrências aeronáuticas.
