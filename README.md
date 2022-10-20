<h1 align="center"> Projeto Covid </h1>

<h4 align="center">Projeto  desenvolvido em PySpark contendo uma análise dos dados da tabela de Covid do Brasil, relacionando dados de desemprego, educação e IDHM</h4>

<h2 align="center"><img src="https://img.shields.io/static/v1?label=STATUS&message=CONCLUIDO&color=green&style=for-the-badge"/></h2>

<img src="https://img.shields.io/static/v1?label=Language&message=PySpark&color=orange"/> [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](http://colab.research.google.com/github/weiji14/deepbedmap/)
 
 <h2>:gear: Acesso ao Projeto</h2>
 
- Para acessar o projeto basta clonar o repositório.

`git clone https://github.com/LawannaKenup/Projeto-covid.git`


<h3> :pencil: Um panorama geral de obitos por covid de acordo com o estado.</h3>

```
estado_total_ob = estados.drop("data")\
                         .groupby("estado")\
                         .agg(sum("obitosNovos").alias("total_obitos_estados"))\
                         .filter(column("total_obitos_estados") >= 0)\
                         .sort(col("total_obitos_estados").desc())\
                         .withColumnRenamed("estado","Estados")

estado_total_ob.show()
```

<img width="199" alt="obitos_estado" src="https://user-images.githubusercontent.com/107578850/196760749-a268c0dd-0055-4567-8727-15b67eedcb41.png">


<h3> :pencil: Média de casos e obitos por covid de acordo com o estado.</h3>

```
media_estado = covid_total5.select("Pais", "estado", \
                                   "media_total_obitos_estado",\
                                   "media_total_casos_estado")\
                           .distinct()\
                           .orderBy(col("media_total_obitos_estado").desc())

media_estado2 = covid_total5.select("Pais", "estado",\
                                    "media_total_obitos_estado", \
                                    "media_total_casos_estado")\
                           .distinct()\
                           .orderBy( col("media_total_casos_estado").desc())

media_estado.show()
media_estado2.show()

```

<img width="424" alt="media_totoal_estados" src="https://user-images.githubusercontent.com/107578850/196763150-06930e69-468f-4a24-8f9d-5fb2728c3379.png">

<h3> :pencil: Dados de desmeprego por trimestre no Brasil de acordo com o estado.</h3>

 - Os dados se tratam de pessoas que se encontravam desempregadas na semana da pesquisa realizada pelo IBGE.
 

<img width="684" alt="desemprego" src="https://user-images.githubusercontent.com/107578850/196764815-5873ba61-06e1-4095-b987-6e06a0a7d0eb.png">


<h3> :bar_chart: Demonstração dos dados em gráfico.</h3>

- Os gráficos a seguir, fazem uma corelação dos dados de obitos por covid em todo o período de 2020 à 2022 e de desemprego no primeiro trimestre de 2020 e segundo trimestre de 2022 de acordo com cada estado.

```
to_plot = [v for v in list(graf.columns)]

fig_graf_desemprego_covid = px.bar(graf, x=graf.Estados, y=to_plot,\
                                   barmode="group",\
                                   text_auto='.2s',\
                                   title="Obitos por Covid e Desemprego")
             
fig_graf_desemprego_covid.show()


graf_desemprego_covid = px.bar(graf, x='Estados', y="total_obitos_estados",\
                               barmode="group",\
                               color="total_obitos_estados",\
                               title="Obitos por Covid")
graf_desemprego_covidx = px.bar(graf, x='Estados', y="1_trimestre_2020",\
                                barmode="group",\
                                color="1_trimestre_2020",\
                                title="Desemprego no primeiro trimestre de 2020")
graf_desemprego_covidxx = px.bar(graf, x='Estados', y="2_trimestre_2022",\
                                 barmode="group",\
                                 color="2_trimestre_2022",\
                                 title="Desemprego no segundo trimestre de 2022")
graf_desemprego_covid.show()
graf_desemprego_covidx.show()
graf_desemprego_covidxx.show()
```

  <img width="854" alt="obitos_covid" src="https://user-images.githubusercontent.com/107578850/196767513-319119fd-6ab5-4a69-82dd-0d5780f63096.png">
  
  <img width="853" alt="desemprego1t2020" src="https://user-images.githubusercontent.com/107578850/196767572-b35383c5-e12e-4e96-a928-986f570973f5.png">
  
  <img width="852" alt="desemprego2t2022" src="https://user-images.githubusercontent.com/107578850/196767607-dc569044-65c2-4124-b3be-1602c29fa80c.png">


<h3> :mag_right: Fonte de dados.</h3>

https://www.ibge.gov.br/

https://covid.saude.gov.br/
