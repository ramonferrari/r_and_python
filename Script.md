Códigos em R e Python
================
Ramon Moreno Ferrari em
06/06/2022

------------------------------------------------------------------------

## O mais básico: comentando o código

Use \# para comentar o código:

``` r
# Isso é um comentário.
```

O mesmo (#) em Python:

``` python
# Isso também é um comentário!

# Que também é obtido por 3 aspas duplas! """
# (Muito útil para comentar grandes blocos de código rapidamente)
```

## Atribuição

No R, utilize `=` ou `<-` para atribuir o valor a uma variável.

``` r
df<-cars # o sinal de = também funciona!
summary(df)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

## Impressão de textos e variáveis

Em R:

``` r
print("oi tudo bem?")
```

    ## [1] "oi tudo bem?"

``` r
print(df$speed)
```

    ##  [1]  4  4  7  7  8  9 10 10 10 11 11 12 12 12 12 13 13 13 13 14 14 14 14 15 15
    ## [26] 15 16 16 17 17 17 18 18 18 18 19 19 19 20 20 20 20 20 22 23 24 24 24 24 25

## Help-me!

Em R, utilize a função help()

``` r
help(print)
```

O mesmo em Python:

``` python
help(print)
```

    ## Help on built-in function print in module builtins:
    ## 
    ## print(...)
    ##     print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    ##     
    ##     Prints the values to a stream, or to sys.stdout by default.
    ##     Optional keyword arguments:
    ##     file:  a file-like object (stream); defaults to the current sys.stdout.
    ##     sep:   string inserted between values, default a space.
    ##     end:   string appended after the last value, default a newline.
    ##     flush: whether to forcibly flush the stream.

## Including Plots

Os plots são incluídos no Rmd. No R, utilize plot() ou o package
ggplot2.

``` r
plot(pressure)
```

![](Script_files/figure-gfm/pressure-1.png)<!-- -->

Em Python, utilize a biblioteca matplotlib:

``` python
import matplotlib.pyplot as plt
# %matplotlib inline se estivesse num Jupyter Notebook
plt.plot(5,5,'o')
plt.xlabel("eixo X")
plt.ylabel("eixo Y")
plt.title("exemplo de plot")
plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

## Importar uma planilha para o Pandas

``` python
import numpy as np # útil para computação científica em Python
import pandas as pd # pacote para estruturar data frames
from __future__ import print_function # retrocompatibilidade python2
#!pip install xlrd
#print('xlrd instalado!')
df_can = pd.read_excel('https://github.com/ramonferrari/r_and_python/blob/main/Script_files/Canada_new.xlsx?raw=true',sheet_name="Canada by Citizenship",skiprows=range(20),skipfooter=2, engine='openpyxl')
df_can.head()
#list(df_can.columns)
```

    ##          Type    Coverage          OdName  AREA  ...  2010  2011  2012  2013
    ## 0  Immigrants  Foreigners     Afghanistan   935  ...  1758  2203  2635  2004
    ## 1  Immigrants  Foreigners         Albania   908  ...   561   539   620   603
    ## 2  Immigrants  Foreigners         Algeria   903  ...  4752  4325  3774  4331
    ## 3  Immigrants  Foreigners  American Samoa   909  ...     0     0     0     0
    ## 4  Immigrants  Foreigners         Andorra   908  ...     0     0     1     1
    ## 
    ## [5 rows x 43 columns]

``` python
df_can.columns = df_can.columns.astype(str)
```

``` python
years=list(map(str,range(1980,2014)))
years_num = list(map(int,years))
df_can['Soma']=df_can[years].sum(axis=1)
df_can.head()
```

    ##          Type    Coverage          OdName  AREA  ...  2011  2012  2013   Soma
    ## 0  Immigrants  Foreigners     Afghanistan   935  ...  2203  2635  2004  58639
    ## 1  Immigrants  Foreigners         Albania   908  ...   539   620   603  15699
    ## 2  Immigrants  Foreigners         Algeria   903  ...  4325  3774  4331  69439
    ## 3  Immigrants  Foreigners  American Samoa   909  ...     0     0     0      6
    ## 4  Immigrants  Foreigners         Andorra   908  ...     0     1     1     15
    ## 
    ## [5 rows x 44 columns]

``` python
df_can.loc[75,years].plot(kind='line')
plt.xlabel("Anos")
plt.ylabel("Número de imigrantes")
plt.title("Imigração a partir do Haiti")
plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

# Lendo um CSV

``` python
import pandas as pd
url='https://github.com/ramonferrari/r_and_python/raw/main/Script_files/imports-85.data'
df=pd.read_csv(url,header=None)
# Para exportar, use df.to_csv(path)
headers = ["symboling","normalized-losses","make","fuel-type","aspiration", "num-of-doors","body-style", "drive-wheels","engine-location","wheel-base", "length","width","height","curb-weight","engine-type", "num-of-cylinders", "engine-size","fuel-system","bore","stroke","compression-ratio","horsepower", "peak-rpm","city-mpg","highway-mpg","price"]
df.columns=headers
#df.tail(n)
df.head()
```

    ##    symboling normalized-losses         make  ... city-mpg highway-mpg  price
    ## 0          3                 ?  alfa-romero  ...       21          27  13495
    ## 1          3                 ?  alfa-romero  ...       21          27  16500
    ## 2          1                 ?  alfa-romero  ...       19          26  16500
    ## 3          2               164         audi  ...       24          30  13950
    ## 4          2               164         audi  ...       18          22  17450
    ## 
    ## [5 rows x 26 columns]

# Entendendo o dataset

``` python
df.dtypes
```

    ## symboling              int64
    ## normalized-losses     object
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
    ## city-mpg               int64
    ## highway-mpg            int64
    ## price                 object
    ## dtype: object

``` python
df.describe()
```

    ##         symboling  wheel-base  ...    city-mpg  highway-mpg
    ## count  205.000000  205.000000  ...  205.000000   205.000000
    ## mean     0.834146   98.756585  ...   25.219512    30.751220
    ## std      1.245307    6.021776  ...    6.542142     6.886443
    ## min     -2.000000   86.600000  ...   13.000000    16.000000
    ## 25%      0.000000   94.500000  ...   19.000000    25.000000
    ## 50%      1.000000   97.000000  ...   24.000000    30.000000
    ## 75%      2.000000  102.400000  ...   30.000000    34.000000
    ## max      3.000000  120.900000  ...   49.000000    54.000000
    ## 
    ## [8 rows x 10 columns]

``` python
df.describe(include="all") # mostra ainda que tenham NaNs
```

    ##          symboling normalized-losses    make  ...    city-mpg highway-mpg price
    ## count   205.000000               205     205  ...  205.000000  205.000000   205
    ## unique         NaN                52      22  ...         NaN         NaN   187
    ## top            NaN                 ?  toyota  ...         NaN         NaN     ?
    ## freq           NaN                41      32  ...         NaN         NaN     4
    ## mean      0.834146               NaN     NaN  ...   25.219512   30.751220   NaN
    ## std       1.245307               NaN     NaN  ...    6.542142    6.886443   NaN
    ## min      -2.000000               NaN     NaN  ...   13.000000   16.000000   NaN
    ## 25%       0.000000               NaN     NaN  ...   19.000000   25.000000   NaN
    ## 50%       1.000000               NaN     NaN  ...   24.000000   30.000000   NaN
    ## 75%       2.000000               NaN     NaN  ...   30.000000   34.000000   NaN
    ## max       3.000000               NaN     NaN  ...   49.000000   54.000000   NaN
    ## 
    ## [11 rows x 26 columns]

# Lidando com dados faltantes

Aparecem como NAs, ? ou 0.

``` python
df=df.dropna()
df=df.dropna(axis=0) # remove a linha (da amostra!)
df=df.dropna(axis=1) # remove a coluna inteira!
df=df.dropna(subset=["price"],axis=0) # trata apenas olhando para determinada coluna
df.dropna(subset=["price"],axis=0,inplace=True) # mesmo acima, ja substituindo o dataset df
```

``` python
# Substituia usando df.replace(antigo,novo)
import numpy as np
df["normalized-losses"]=df["normalized-losses"].replace("?",np.nan) # trocamos ? por NaN
df['normalized-losses'] = df['normalized-losses'].astype(float) # convertermos de string para float
media=df["normalized-losses"].mean() # calculamos a media
media
```

    ## 122.0

``` python
df["normalized-losses"].replace(np.nan,media)
```

    ## 0      122.0
    ## 1      122.0
    ## 2      122.0
    ## 3      164.0
    ## 4      164.0
    ##        ...  
    ## 200     95.0
    ## 201     95.0
    ## 202     95.0
    ## 203     95.0
    ## 204     95.0
    ## Name: normalized-losses, Length: 205, dtype: float64

# Acessando, calculando e renomeando colunas

``` python
df["city-mpg"]
```

    ## 0      21
    ## 1      21
    ## 2      19
    ## 3      24
    ## 4      18
    ##        ..
    ## 200    23
    ## 201    19
    ## 202    18
    ## 203    26
    ## 204    19
    ## Name: city-mpg, Length: 205, dtype: int64

``` python
df["city-mpg"]=235/df["city-mpg"]
```

``` python
df.rename(columns={"city-mpg":"city-L/100km"},inplace=True)
df["city-L/100km"]
```

    ## 0      11.190476
    ## 1      11.190476
    ## 2      12.368421
    ## 3       9.791667
    ## 4      13.055556
    ##          ...    
    ## 200    10.217391
    ## 201    12.368421
    ## 202    13.055556
    ## 203     9.038462
    ## 204    12.368421
    ## Name: city-L/100km, Length: 205, dtype: float64

# Normalização de datasets

Seja dividindo pelo máximo, dividindo pelo (máximo - mínimo) após
subtrair o mínimo, ou pelo desvio-padrão após retirar a média,
precisaremos aprender a calcular:

``` python
df["length"]=df["length"]/df["length"].max()
df["length"]=(df["length"]-df["length"].min())/(df["length"].max()-df["length"].min())
df["length"]=(df["length"]-df["length"].mean())/df["length"].std()
```

# Binning (binagem) ou agrupamentos

Parece bastante com os levels do R

``` python
df["price"]=df["price"].replace("?",np.nan) # trocamos ? por NaN
```

# Tratamento de variáveis categóricas

``` python
import pandas as pd
pd.get_dummies(df['fuel-type'])
```

    ##      diesel  gas
    ## 0         0    1
    ## 1         0    1
    ## 2         0    1
    ## 3         0    1
    ## 4         0    1
    ## ..      ...  ...
    ## 200       0    1
    ## 201       0    1
    ## 202       0    1
    ## 203       1    0
    ## 204       0    1
    ## 
    ## [205 rows x 2 columns]

``` python
df['price'] = df['price'].astype(float) # convertermos de string para float
bins = np.linspace(df["price"].min(),df["price"].max(),4) # pega a amplitude e divide em 3 grupos a partir de 4 valores!
group_names = ["Low","Medium","High"]
df["price_binned"]=pd.cut(df["price"],bins,labels=group_names,include_lowest=True)
df["price_binned"]
```

    ## 0         Low
    ## 1         Low
    ## 2         Low
    ## 3         Low
    ## 4         Low
    ##         ...  
    ## 200       Low
    ## 201    Medium
    ## 202    Medium
    ## 203    Medium
    ## 204    Medium
    ## Name: price_binned, Length: 205, dtype: category
    ## Categories (3, object): ['Low' < 'Medium' < 'High']

# Sorting e Transposing um data frame

``` python
df_can.rename(columns={"OdName":"Country"},inplace=True)
df_can=df_can.set_index('Country')
df_can.sort_values(['Soma'],ascending=False,axis=0,inplace=True)
df_can.head()
```

    ##                                                           Type  ...    Soma
    ## Country                                                         ...        
    ## India                                               Immigrants  ...  691904
    ## China                                               Immigrants  ...  659962
    ## United Kingdom of Great Britain and Northern Ir...  Immigrants  ...  551500
    ## Philippines                                         Immigrants  ...  511391
    ## Pakistan                                            Immigrants  ...  241600
    ## 
    ## [5 rows x 43 columns]

``` python
df_top5=df_can.head()
df_top5=df_top5[years].transpose()
```

# Area Plot

``` python
df_top5.plot(kind='area')
plt.xlabel("Anos")
plt.ylabel("Número de imigrantes")
plt.title("Top 5 países em imigração")
plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-21-5.png)<!-- -->

# Histogram Plot

``` python
import matplotlib as mpl
import matplotlib.pyplot as plt

df_can['2013'].plot(kind='hist')

plt.title("Histograma de imigração de 195 países em 2013")
plt.ylabel("Número de Paises")
plt.xlabel("Número de imigrantes")

plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-22-7.png)<!-- -->

``` python
import matplotlib as mpl
import matplotlib.pyplot as plt
import numpy as np 

count,bin_edges=np.histogram(df_can['2013'])

df_can['2013'].plot(kind='hist',xticks=bin_edges)

plt.title("Histograma de imigração de 195 países em 2013")
plt.ylabel("Número de Paises")
plt.xlabel("Número de imigrantes")

plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-22-8.png)<!-- -->

# Gráfico de barras

``` python
df_iceland=df_can.loc['Iceland',years]
df_iceland.plot(kind='bar')

plt.title("Imigração Islândia -> Canada de 1980 a 2013")
plt.ylabel("Número de Imigrantes")
plt.xlabel("Ano")

plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-23-11.png)<!-- -->

# Gráfico de pizza

``` python
df_can.rename(columns={"AreaName":"Continent"},inplace=True)
df_continentes=df_can.groupby('Continent',axis=0).sum()
df_continentes=df_continentes.drop(columns=['AREA', 'REG','DEV'])
df_continentes
```

    ##                                   1980   1981   1982  ...    2012    2013     Soma
    ## Continent                                             ...                         
    ## Africa                            3951   4363   3819  ...   38083   38543   618948
    ## Asia                             31025  34314  30214  ...  152218  155075  3317794
    ## Europe                           39760  44802  42720  ...   29177   28691  1410947
    ## Latin America and the Caribbean  13081  15215  16769  ...   27173   24950   765148
    ## Northern America                  9378  10030   9074  ...    7892    8503   241142
    ## Oceania                           1942   1839   1675  ...    1679    1775    55174
    ## 
    ## [6 rows x 35 columns]

``` python
df_continentes['Soma'].plot(kind='pie')
plt.title("Imigração para o Canada por continente, de 1980 a 2013")
plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-25-13.png)<!-- -->

# Boxplot

``` python
df_japan=df_can.loc[['Japan'],years].transpose()
import matplotlib as mpl
import matplotlib.pyplot as plt
df_japan.plot(kind='box')

plt.title("Boxplot de imigrantes japoneses para o Canadá entre 1980 e 2013")
plt.ylabel("Número de Imigrantes")

plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-26-15.png)<!-- -->

# Gráficos de Dispersão

``` python
df_total=df_continentes.drop(columns=['Soma']).transpose()
df_total = df_total.reset_index(level=0)
df_total.rename(columns={"index":"Year"},inplace=True)
df_total.index.names = ['Index']

df_total['Total']=df_total.sum(axis=1)
```

    ## <string>:1: FutureWarning: Dropping of nuisance columns in DataFrame reductions (with 'numeric_only=None') is deprecated; in a future version this will raise TypeError.  Select only valid columns before calling the reduction.

``` python
df_total=df_total.drop(columns=['Africa','Europe','Latin America and the Caribbean','Northern America','Oceania','Asia'])

marcacoes=columns=['1980','1990','2000','2010']
df_total.plot(kind='scatter',x='Year',y='Total',xticks=marcacoes)

plt.title("Imigração total para o Canada entre 1980 e 2013")
plt.ylabel("Número de Imigrantes")
plt.xlabel("Ano")

plt.show()
```

![](Script_files/figure-gfm/unnamed-chunk-27-17.png)<!-- -->

# Folium

    ## <folium.folium.Map object at 0x00000000660B4C70>

    ## <folium.folium.Map object at 0x0000000065E0DAF0>

    ## <folium.folium.Map object at 0x0000000065E0DF40>

Folium deve ser aberto no Jupyter!

# Escrever

## Sobre Rmd

Utilizar `echo = FALSE` no RMarkdown faz com que o código não apareça no
output, apenas o resultado (um gráfico, por exemplo!).
