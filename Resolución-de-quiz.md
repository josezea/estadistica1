Solución de quiz 1
================

## Solución Quiz 1

1.  Realizar un análisis de frecuencia del tamaño de las empresas /
    Level (frecuencias absolutas, frecuencias relativas, frecuencias
    realtivas acumuladas). Interpretar los resultados en sus propias
    palabras

``` r
# Cargar los datos
library(pander) # Pauete para colocar cuadros con una mejor apariencia
library(TeachingSampling) # Cargar los datos de Lucy
library(ggplot2) # Paquete para hacer gráficos más estéticos
data(Lucy)
```

``` r
# Ordenar las categorías (empresas pequeñas, medianas, grandes)
Lucy$Level <- factor(Lucy$Level, levels = c("Small", "Medium", "Big"))
```

Las frecuencias absolutas pueden calcularse como sigue:

``` r
table(Lucy$Level)
```

    ## 
    ##  Small Medium    Big 
    ##   1576    737     83

Las frecuencias relativas puede calcularse:

``` r
prop.table(table(Lucy$Level))
```

    ## 
    ##      Small     Medium        Big 
    ## 0.65776294 0.30759599 0.03464107

Las frecuencias relativas acumuladas:

``` r
cumsum(prop.table(table(Lucy$Level)))
```

    ##     Small    Medium       Big 
    ## 0.6577629 0.9653589 1.0000000

Pueden organizarse los resultados como sigue:

``` r
tabla_frecuencias <- data.frame(Level = names(table(Lucy$Level)),
  Frec_abs = as.numeric(table(Lucy$Level)), Frec_rel = as.numeric(prop.table(table(Lucy$Level))), 
Frec_relat_acum = as.numeric(cumsum(prop.table(table(Lucy$Level)))))
pander(tabla_frecuencias)
```

| Level  | Frec\_abs | Frec\_rel | Frec\_relat\_acum |
|:------:|:---------:|:---------:|:-----------------:|
| Small  |   1576    |  0.6578   |      0.6578       |
| Medium |    737    |  0.3076   |      0.9654       |
|  Big   |    83     |  0.03464  |         1         |

El 65,6% de las empresas que se analizan son pequeñas y el 30,7% de las
empresas son medianas, cerca del 87% de las empresas soy pequeñas y
medianas, las empresas grandes son únicamente 83 (menos del 3.5% de las
empresas).

1.  Realizar un diagrama del tamaño de las empresas (usar las
    frecuencias relativas) Interpretar.

``` r
ggplot(data = tabla_frecuencias, aes(x = Level, y = Frec_rel)) + 
  geom_bar(stat = "identity")
```

![](Resolución-de-quiz_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->
\* En el gráfico se confirma que dentro del grupo de empresas analizadas
predominan en cuanto número las empresas pequeñas y medianas..
