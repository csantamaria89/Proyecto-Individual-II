<h1 align="center">
Proyecto Individual N°2
</h1>

Simularemos una situación en donde una empresa que busca invertir en el mercado bursátil le solicita analizarlo en detalle. Considerando que la empresa no conoce esta área financiera, le solicita una explicación de qué ha sucedido en este mercado en los últimos años (considerando impactos positivos y negativos a partir del año 2000), recomendaciones de inversión (ya sea enfocada en empresas o rubros de éstas) y otra información complementaria que, usted como experto en datos, está en capacidad de brindar.

<h1>Contexto</h1>
El desarrollo de este estudio se basó en el (índice bursátil) que recopila las 500 empresas más grandes de Estados Unidos. Este índice es desarrollado por la empresa Standard & Poor's denominado "S&P500". La elección de las compañías se basan en la capitalización bursatil y excluye las pequeñas y medianas empresas.<br></br>

Las empresas del "S&P500" se dividen en 11 sectores de la economía:<br>

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/TreeMap.png"  height=300>
</p>

Esto permite a los inversionistas hacer un seguimiento no sólo del índice en su conjunto, sino también a las empresas dentro de las mismas indistrias. Esto facilita un mayor nivel de diversificación. Por otra parte, el índice "S&P500" nos brinda "Tranquilidad" al saber que estamos invirtiendo en empresas representativas de Estados Unidos. No obstante, es necesario hacer un análisis detallado que nos permita identificar ciertos comportamientos del mercado que indiquen si debemos invertir o no.</br>

Para este ejercicio, nuestra firma de analistas propone analizar los siguientes sectores:

* Tecnología de la Información
* Servicios de Comunicación
* Productos básicos de consumo
* Consumo Ocasional
* Salud

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/Marcas.png"  height=300>
</p>

<h1>Análisis Exploratorio de los datos (EDA)</h1>

Para poder analizar el mercado bursátil, utilizamos las siguientes herramientas:

* Yahoo Finance
* Alphavantage

Estas permitieron acceder a datos financieros que presentaremos en nuestro archivo de power BI **Lab2.pbix**. 

Antes de analizar puntualmente cada empresa, nos parece importante estudiar el comportamiento del índice para conocer su tendencía y saber si vale la pena invertir en cualquiera de las compañías que lo componen por supuesto con su previo análisis.

1. Histórico correspondiente al precio de cierre del índice ***S&P500*** (2000 - 2023) 

```shell
empresas = ['GSPC']

recolector =[]
for nemo in empresas:
    ticker =yf.Ticker(nemo)
    px = ticker.history(start="2000-01-01", end="2023-03-27")['Close']
    px.name = nemo

    recolector += [px]

precios = pd.concat(recolector, axis=1)
```
**Nota:** Este código guarda en un Data Frame los precios de cierre para el índice bursátil en un periodo del año 2000 al 2023

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/GSPC1.png"  height=500>
</p>


2. Precio de cierre de cada acción durante un periodo establecido:

```shell
empresas = ['AMZN','AAPL','INTC','MSFT','NFLX']

recolector =[]
for nemo in empresas:
    ticker =yf.Ticker(nemo)
    px = ticker.history(start="2000-01-01", end="2023-03-27")['Close']
    px.name = nemo

    recolector += [px]

precios = pd.concat(recolector, axis=1)
```
**Nota:** Este código guarda en un Data Frame los precios de cierre de las diferentes acciones en un periodo del año 2000 al 2023
