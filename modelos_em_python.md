Desenvolvimento de Modelos em Python
================
Ramon Moreno Ferrari em
11/06/2022

------------------------------------------------------------------------

## Baixando o dado

``` python
import pandas as pd
import numpy as np
url='https://raw.githubusercontent.com/ramonferrari/r_and_python/main/intro_python_files/imports-85.data'
df=pd.read_csv(url,header=None)
df
```

    ##      0    1            2       3      4     5   ...    20   21    22  23  24     25
    ## 0     3    ?  alfa-romero     gas    std   two  ...   9.0  111  5000  21  27  13495
    ## 1     3    ?  alfa-romero     gas    std   two  ...   9.0  111  5000  21  27  16500
    ## 2     1    ?  alfa-romero     gas    std   two  ...   9.0  154  5000  19  26  16500
    ## 3     2  164         audi     gas    std  four  ...  10.0  102  5500  24  30  13950
    ## 4     2  164         audi     gas    std  four  ...   8.0  115  5500  18  22  17450
    ## ..   ..  ...          ...     ...    ...   ...  ...   ...  ...   ...  ..  ..    ...
    ## 200  -1   95        volvo     gas    std  four  ...   9.5  114  5400  23  28  16845
    ## 201  -1   95        volvo     gas  turbo  four  ...   8.7  160  5300  19  25  19045
    ## 202  -1   95        volvo     gas    std  four  ...   8.8  134  5500  18  23  21485
    ## 203  -1   95        volvo  diesel  turbo  four  ...  23.0  106  4800  26  27  22470
    ## 204  -1   95        volvo     gas  turbo  four  ...   9.5  114  5400  19  25  22625
    ## 
    ## [205 rows x 26 columns]

``` python
headers = ["symboling","normalized-losses","make","fuel-type","aspiration", "num-of-doors","body-style", "drive-wheels","engine-location","wheel-base", "length","width","height","curb-weight","engine-type", "num-of-cylinders", "engine-size","fuel-system","bore","stroke","compression-ratio","horsepower", "peak-rpm","city-mpg","highway-mpg","price"]
df.columns=headers
df["normalized-losses"]=df["normalized-losses"].replace("?",np.nan) # trocamos ? por NaN
df['normalized-losses'] = df['normalized-losses'].astype(float) # convertermos de string para float
df["price"]=df["price"].replace("?",np.nan) # trocamos ? por NaN
df['price'] = df['price'].astype(float) # convertermos de string para float
df["city-mpg"]=235/df["city-mpg"]
df.rename(columns={"city-mpg":"city-L/100km"},inplace=True)
df.dropna(axis=0,inplace=True) # mesmo acima, ja substituindo o dataset df
df
```

    ##      symboling  normalized-losses   make  ... city-L/100km highway-mpg    price
    ## 3            2              164.0   audi  ...     9.791667          30  13950.0
    ## 4            2              164.0   audi  ...    13.055556          22  17450.0
    ## 6            1              158.0   audi  ...    12.368421          25  17710.0
    ## 8            1              158.0   audi  ...    13.823529          20  23875.0
    ## 10           2              192.0    bmw  ...    10.217391          29  16430.0
    ## ..         ...                ...    ...  ...          ...         ...      ...
    ## 200         -1               95.0  volvo  ...    10.217391          28  16845.0
    ## 201         -1               95.0  volvo  ...    12.368421          25  19045.0
    ## 202         -1               95.0  volvo  ...    13.055556          23  21485.0
    ## 203         -1               95.0  volvo  ...     9.038462          27  22470.0
    ## 204         -1               95.0  volvo  ...    12.368421          25  22625.0
    ## 
    ## [164 rows x 26 columns]

``` python
df.dtypes
```

    ## symboling              int64
    ## normalized-losses    float64
    ## make                  object
    ## fuel-type             object
    ## aspiration            object
    ## num-of-doors          object
    ## body-style            object
    ## drive-wheels          object
    ## engine-location       object
    ## wheel-base           float64
    ## length               float64
    ## width                float64
    ## height               float64
    ## curb-weight            int64
    ## engine-type           object
    ## num-of-cylinders      object
    ## engine-size            int64
    ## fuel-system           object
    ## bore                  object
    ## stroke                object
    ## compression-ratio    float64
    ## horsepower            object
    ## peak-rpm              object
    ## city-L/100km         float64
    ## highway-mpg            int64
    ## price                float64
    ## dtype: object

## Regressão Linear Simples

Preditor ou variável independentes
(![x](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;x "x"))
Target ou variável dependente
(![y](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;y "y")),
que denotaremos de
![\\hat{y}](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Chat%7By%7D "\hat{y}")
fazendo referência a um modelo. Buscamos uma relação linear do tipo

![\\hat{y}=ax + b](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%5Chat%7By%7D%3Dax%20%2B%20b "\hat{y}=ax + b")

Onde
![a](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;a "a")
é o slope, ou coeficiente angular, e
![b](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;b "b")
é o intercept, ou coeficiente linear. A equação cima nos permite
calcular o valor de
![y](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;y "y")
para
![x](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;x "x")
não pertencentes ao conjunto de treinamento.

### Modelando:

``` python
from sklearn.linear_model import LinearRegression
lm=LinearRegression() # cria um objeto de regressão linear
x=df[['highway-mpg']]
y=df[['price']]
lm.fit(x,y)
```

    ## LinearRegression()

``` python
y_hat=lm.predict(x)
b=lm.intercept_
a=lm.coef_
print("O relacionamento é dado por: \nPrice = ",a,"highway-mpg + ",b)
```

    ## O relacionamento é dado por: 
    ## Price =  [[-631.75258436]] highway-mpg +  [31586.29724467]

## Regressão Linear Múltipla

Buscamos uma relação linear do tipo

![ \\hat{y} =a_1x_1 +a_2x_2 + a_3x_3 + \\dots + b ](https://latex.codecogs.com/png.image?%5Cdpi%7B110%7D&space;%5Cbg_white&space;%20%5Chat%7By%7D%20%3Da_1x_1%20%2Ba_2x_2%20%2B%20a_3x_3%20%2B%20%5Cdots%20%2B%20b%20 " \hat{y} =a_1x_1 +a_2x_2 + a_3x_3 + \dots + b ")

``` python
x=df[['horsepower','curb-weight','engine-size','highway-mpg']]
y=df[['price']]
lm.fit(x,y)
```

    ## LinearRegression()

``` python
y_hat=lm.predict(x)
b=lm.intercept_
a=lm.coef_
print("O relacionamento é dado por: \nPrice = ",a[[0],0],"horsepower + ",a[[0],1],"curb-weight + ",a[[0],2],"engine-size + ",a[[0],3],"highway-mpg + ",b)
```

    ## O relacionamento é dado por: 
    ## Price =  [25.34377007] horsepower +  [8.64500785] curb-weight +  [16.79558345] engine-size +  [-2.6715555] highway-mpg +  [-14119.61866258]
