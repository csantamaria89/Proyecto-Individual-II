<h1 align="center">
Proyecto Analálisis de Inversión con el índice "S&P500"
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
* Alpha Vantage

Estas permitieron acceder a datos financieros que presentaremos en nuestro archivo de power BI **Lab2.pbix**. 

Antes de analizar puntualmente cada empresa, nos parece importante estudiar el comportamiento del índice para conocer su tendencía y saber si vale la pena invertir en cualquiera de las compañías que lo componen por supuesto con su previo análisis.

* Histórico correspondiente al precio de cierre del índice ***S&P500*** (2000 - 2023) 

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

En la imágen anterior, se puede evidenciar la tendencia alsista 📈 del índice *S&P500* a lo largo del tiempo, también se puede observar hitos importantes que describen tiempos de crisis. 

- La recesión económica de 2008, conocida como la Gran Recesión, fue la fuerte caída de la actividad económica que comenzó en diciembre de 2007 y duró hasta junio de 2009.
- Crisis económica por el Corona Virus.
- Repercusión de la Pnademia, Inflación, Guerra.

En general, el comportamiento del índice nos puede suponer una ventaja de inversión si analisamos el entorno y las crisis pues la inversion puede ser en cuanto a tendencias de crecimiento o caidas.


<h1>Grupo Inversión 1</h1>

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/analisis1.png"  height=100>
</p>

* Aplicamos el siguiente código para poder visualizar el valor de cierre de cada acción seleccionada durante un periodo establecido:

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

Con el siguiente código obtenemos el precio de cierre de la acción del día anterior su valor y porcentaje de ganancia.

```shell
import pandas as pd
import requests

# API key de Alpha Vantage
api_key = "YOUR KEY HERE"

# Símbolo de la acción que queremos obtener
symbol = "MCD"

# URL para obtener los datos de la acción
url = f"https://www.alphavantage.co/query?function=GLOBAL_QUOTE&symbol={symbol}&apikey={api_key}"

# Hacemos la petición HTTP GET
response = requests.get(url)

# Obtenemos los datos en formato JSON
data = response.json()

# Creamos un diccionario con los valores que queremos
stock_info = {
    "Last Price": data["Global Quote"]["05. price"],
    "Change": data["Global Quote"]["09. change"],
    "% Change": data["Global Quote"]["10. change percent"]
}

# Creamos el DataFrame
df = pd.DataFrame(stock_info, index=[0])
df.to_csv("Alpha_McDonalds.csv", index=False)
```
**Nota:** El código anterior se basa en la API de Alpha Vantage, para ello directamente en su plataforma se debe crear un Key para que permita el uso del código.

- El análisis de estas acciones corresponde al sector de *Tecnología de la información*, *Consumo ocasional* y *Servicios de comunicación* 
<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/inversion1.png"  height=500>
</p>

De acuerdo con la imágen anterior podemos concluir que para las empresas analisadas, se evidencia que les afecto las crisis mencionadas anteriormente. Sin embargo, todas han tenido un crecimiento o por lo menos se han logrado estabilizar con las diferentes coyunturas que vive del país.

🚨**Netflix**: Puntualmente vemos un caso de tendencia bajista 📉 a finales del 2021 y 2022.

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/Tnetflix.png"  height=300>
</p>

Las acciones de Netflix se desplomaron un 35% después de que la empresa revelara una fuerte caída en los suscriptores, y advirtiera que millones más están listos para abandonar el servicio.
- La compañía perdió más de US$50.000 millones de su valor en el mercado, ya que los expertos indicaron que enfrenta dificultades para volver a la normalidad.
- Netflix afronta una intensa competencia por parte de sus rivales y también se vio afectada después de que subió los precios y se fue de Rusia.
- Impulsar el crecu¿imiento de clientes con nuevo servicio gratuito con publicidad.
- Se estima que más de 100 millones de hogares utilizan su servicio de manera ilegal.</br>
***fuente:***("https://www.bbc.com/mundo/noticias-61182426")

<h1>Grupo Inversión 2</h1>

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/analisis2.png"  height=100>
</p>

* Repetimos el proceso del grupo anterior para ver el histórico del precio de cierre para este grupo de compañias.

El análisis de estas acciones corresponde al sector del Consumo Ocasional, Productos básicos de consumo y Salud
<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/inversion2_1.png"  height=500>
</p>

Con en análisis del gráfico, podemos identificar que a la empresa de Walmart (Productos básicos de consumo) y Moderna (Salud) no fueron afectadas por la pandemia y que por el contrario han tenido una tendencia alsista 📈 lo que representa un muy buen escenario para invertir.

<h1>KPIs Conclusiones</h1>

Con el análisis previo y el perfil de inversion conservador, podemos identificar fácilmente los acciones por las cuales podríamos invertir. A continuación se presentaran los siguientes KPIs para poder conluir que alternativas tenemos para invertir a corto o largo plazo.

<p align="center">
<img src="https://github.com/csantamaria89/Proyecto-Individual-II/blob/main/Im%C3%A1genes/kpis.png"  height=400>
</p>

***KPIs***

1. **Market Cap** (Capitalización del Mercado): Valor total de las acciones en circulación de una empresa. </br>

    Se calcula multiplicando el número de acciones en circulación sw una empresa por el precio actual de la acción. </br>
    
    CAP = Número de Acciones x Precio de la Acción </BR>
    
    El Market cap es un dato importante tanto para conocer el tamaño de la empresa como múltiplo para calcular diferentes ratios financieros. Además, se           utiliza esta cifra para determinar el tamaño de una empresa en lugar de usar el total de las ventas o los activos totales.</BR>
    
2. **Earnings per Share** EPS (Beneficio por Scción): Son los beneficios que le corresponden al accionista por cada acción.

    EPS básico = (Beneficio neto-Dividendos de acciones preferentes)/(Media ponderada del número de acciones ordinarias en circulación)
    
    **Es necesario excluir la parte correspondiente a los accionistas preferentes.
    
3. **Range (52 Week)** Este indicador nos muestra el valor mínimo y el máximo del precio de cierre de la acción durante las últimas 52 semanas. Con este valor podemos compararlo con el precio de cierre actual y tener un indicador que nos alerte si el precio de cierre actual está más cerca del valor negativo o incluso ha sobrepasado ese umbral o viceversa.


------------------------------------------------------------------------------------------------------------------------------------------
Invertir dependerá del perfil de la persona o empresa. Hay perfiles conservadores, riesgosos, a corto plazo a largo plazo, etc. Es importante entender el perfil y a partir de allí analizar las diferentes opciones en el mercado búrsatil. 

En este análisis, se propone invertir en (3) acciones de acuerdo con los KPIs evaluados. 

`**Nota: Este análisis es netamente académico, se recomienda buscar una asesoría profesional para invertir.**`

- **Amazon**: En este momento el ***EPS*** (Beneficios por acción) son negativos, lo cual indica que la compañia está generando pérdidas. Para un perfil conservador no recomendamos invertir ya que se presenta volatilidad y es incierto saber que pasará con el precio de la acción.

- **Microsoft**: Esta empresa fue seleccionada ya que según los KPIs analizados y el comportamieto del precio de cierre a lo largo del tiempo muestra una empresa estable a largo plazo.

- **Moderna**: Es importante identificar los momentos de crisis, moderna es una excelente alternativa de inversión en el corto plazo, ya que hay una nueva sepa del Corona Virus que necesitara de nuevas vacunas.

- **Walmart**: Analizando el comportamiento del precio de la acción con respecto a todos los eventos que han afectado la economía americana a lo largo del tiempo, vemos claramente que está empresa tiene una tendencia alsista y que no le ha afectado ningún evento o crisis económica, por lo cual esta puede llegafr  a ser una inversión segura al largo plazo.

