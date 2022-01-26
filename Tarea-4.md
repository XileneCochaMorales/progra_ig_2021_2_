Tarea Nº4
================
Xilene Cocha Morales
25/1/2022

# Ejercicios: ggplot2

Cargar la data *millas* del paquete **datos**

### Parte 1: ggplot base

-   Ejecuta ggplot(data = millas). ¿Qué observas?

``` r
ggplot(data = millas) #Al ejecutar el código no se observa ningún gráfico
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

-   ¿Cuántas filas hay en millas? ¿Cuántas columnas?

``` r
dim(millas) ##234 filas y 11 columnas
```

    ## [1] 234  11

-   ¿Qué describe la variable traccion? Lee la ayuda de ?millas para
    encontrar la respuesta.

``` r
?millas
```

    ## starting httpd help server ... done

``` r
#la variable tracción describe el tipo de tracción de cada auto en dat_millas. 
#En la data solo hay tres tipos: delantera(d), trasera(t) y 4ruedas(4).
```

-   Realiza un gráfico de dispersión de autopista versus cilindros.

``` r
grafico_base <- ggplot(data=millas)+
  aes(x=autopista,y=cilindros)+
  geom_point()

grafico_base + labs(ggtitle = "Gráfico de dispersión entre autopista y cilindros", 
                    subtitle="Periodo 1999-2008",
                    xlab("autopista"),
                    ylab("cilindros"), 
                    caption="Data:millas-ggplot2")
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

-   ¿Qué sucede cuando haces un gráfico de dispersión (scatterplot) de
    clase versus traccion? ¿Por qué no es útil este gráfico?

``` r
grafico_base2 <- ggplot(data=millas)+
  aes(x=clase,y=traccion)+
  geom_point()

grafico_base2 + labs(ggtitle = "Gráfico de dispersión entre clase y traccion", 
                    subtitle="Periodo 1999-2008",
                    xlab("clase"),
                    ylab("traccion"), 
                    caption="Data:millas-ggplot2")
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
#Scatterplot es útil para mostrar la relación de dos variables continuas, clase y traccion no son variables continuas
```

### Parte 2: Mapeos estéticos

-   ¿Qué no va bien en este código? ¿Por qué hay puntos que no son
    azules?

``` r
 ggplot(data = millas) +
   geom_point(mapping = aes(x = cilindrada, y = autopista, color = "blue"))
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
#porque se incluyó al color blue dentro de aes(), lo cual trata a este como si fuera una variable, para solucionarlo debemos de pararlo de aes().
```

-   ¿Qué variables en millas son categóricas? ¿Qué variables son
    continuas? (Pista: escribe ?millas para leer la documentación de
    ayuda para este conjunto de datos). ¿Cómo puedes ver esta
    información cuando ejecutas millas?

``` r
?millas
#las varibles categóricas son modelo, transmision, traccion, combustible y clase.
#las variables continuas son cilindrada, años, cilindros, ciudad y autopista.
```

-   Asigna una variable continua a color, size, y shape. ¿Cómo se
    comportan estas estéticas de manera diferente para variables
    categóricas y variables continuas?

-   ¿Qué ocurre si asignas o mapeas la misma variable a múltiples
    estéticas?

``` r
ggplot(millas, aes(x = cilindrada, y = autopista, colour = autopista, size = autopista)) +
  geom_point()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
#se generaría un gráfico redundante.
```

-   ¿Qué hace la estética stroke? ¿Con qué formas trabaja? (Pista:
    consulta ?geom_point)

``` r
ggplot(mtautos, aes(peso, millas)) +
  geom_point(shape = 21, colour = "pink", fill = "yellow", size = 5, stroke = 5)
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

``` r
#Se encarga de cambiar el tamaño de los bordes de las formas 21 a 25, a estas también será posible cambiar su color de relleno y de su borde, y también cambiar el tamaño de su borde.
```

-   ¿Qué ocurre si se asigna o mapea una estética a algo diferente del
    nombre de una variable, como aes(color = cilindrada \< 5)?

``` r
ggplot(millas, aes(x = cilindrada, y = autopista, colour = cilindrada < 5)) +
  geom_point()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
#Se crea una variable temporal que ejecuta la evaluación de la variable, en aes(color = cilindrada < 5) de acuerdo al resultado de esto si es V o F, se incluirá los colores en el gráfico.
```

### Parte 3: Facetas

-   ¿Qué ocurre si intentas separar en facetas una variable continua?

``` r
ggplot(millas, aes(x = cilindros, y = autopista)) +
  geom_point() +
  facet_grid(. ~ ciudad)
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

``` r
#la variable continua se convierte a una variable categórica y el gráfico contiene una faceta para cada valor.(facet_grid) esta función separa las facetas o celdas.
```

-   ¿Qué significan las celdas vacías que aparecen en el gráfico
    generado usando `facet_grid(traccion ~ cilindros)`? ¿Cómo se
    relacionan con este gráfico?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = traccion, y = cilindros))
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
#Las celdas vacías en el gráfico se refiere a combinaciones de traccion y cilindros que no tienen observaciones.
```

-   ¿Qué grafica el siguiente código? ¿Qué hace . ?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_grid(traccion ~ .)
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_grid(. ~ cilindros)
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-14-2.png)<!-- -->

``` r
#Este código 
#Ignora la dimensión al momento de dibujar las facetas, por ejermplo, el primer gráfico traccion divide los valores de autopista  en el eje y , mientras que cilindros divide los valores de cilindrada  en el eje x .
```

-   Mira de nuevo el primer gráfico en facetas presentado en esta
    sección:

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista)) +
  facet_wrap(~ clase, nrow = 2)
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

¿Cuáles son las ventajas de separar en facetas en lugar de aplicar una
estética de color? ¿Cuáles son las desventajas? ¿Cómo cambiaría este
balance si tuvieras un conjunto de datos más grande? - Lee
`?facet_wrap`. ¿Qué hace nrow? ¿Qué hace ncol? ¿Qué otras opciones
controlan el diseño de los paneles individuales? ¿Por qué `facet_grid()`
no tiene argumentos nrow y ncol? - Cuando usas `facet_grid()`,
generalmente deberías poner la variable con un mayor número de niveles
únicos en las columnas. ¿Por qué?

``` r
ggplot(data = millas) +
  geom_point(mapping = aes(x = cilindrada, y = autopista, color = clase))
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
#.
#La ventaja de usar clase como parte de las facetas en lugar de aplicar color es que nos da la posibilidad de incluir varias categorías, es decir así podemos distinguir las categorías.

#La desventaja de clase para las facetas, en lugar del argumento de color es que dificulta la comparación de valores ebtre las categoria , ya que al haber una gran cantidad de colores se vuelve un poco dificl encontrar cada categoria.
#Si tuvieramos un conjunto de categorias  más grande , podria haber superposición y resultaria problematico manejar esto con argumetnos de color o clase a menos que el numero de argumentos  sea más pequeño.
#Si aumenta cada vez más el número de categorias va volverse más dificl contar con los colores 
#suficientes y sera dificil distinguir las categorias.

#.
#nrow y ncol  determinan el número de filas y columnas al momento de generara las facetas.
#facet_grid() opera sobre una unica variable.y este no necesita a nrow y a ncol porque el 
#número de valores unicos en la función determina el número de filas y columnas.

#.
#Porque al hacer eso originas más espacio para las columnas en caso de que el grafico este en posición horizontal.
```

###Parte 4: Objetos geométricos \* ¿Qué geom usarías para generar un
gráfico de líneas? ¿Y para un diagrama de caja? ¿Y para un histograma?
¿Y para un gráfico de área?

``` r
#para un grafico de lineas geom_line()
#para un diagrama de caja geom_boxplot()
#para un histograma geom_histogram()
#para un gráfico de área geom_area()
```

-   Ejecuta este código en tu mente y predice cómo se verá el output.
    Luego, ejecuta el código en R y verifica tus predicciones.

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista, color = traccion)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
#Sí se verifica
```

-   ¿Qué muestra show.legend = FALSE? ¿Qué pasa si lo quitas? ¿Por qué
    crees que lo utilizamos antes en el capítulo?

``` r
#show.legend =FALSE oculta la leyende del gráfico
ggplot(data = millas) +
  geom_smooth(
    mapping = aes(x = cilindrada, y = autopista, colour = traccion),
    show.legend = FALSE
  )
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
#Si show.legend =TRUE o defrente quitamos show.legend mostrará la relación entre traccion y la paleta de colores.
ggplot(data = millas) +
  geom_smooth(mapping = aes(x = cilindrada, y = autopista, colour = traccion))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-19-2.png)<!-- --> \* ¿Qué
hace el argumento se en geom_smooth()?

``` r
#Se encarga de añadir las bandas de error estandar a las lineas.
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista, colour = traccion)) +
  geom_point() +
  geom_smooth(se = TRUE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-20-1.png)<!-- --> \* ¿Se
verán distintos estos gráficos? ¿Por qué sí o por qué no?

``` r
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_point() +
  geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

``` r
ggplot() +
  geom_point(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_smooth(data = millas, mapping = aes(x = cilindrada, y = autopista))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-21-2.png)<!-- -->

``` r
#No se veran distintos pues geom_point() y geom_smooth() toman los datos y estéticas de ggplot(), así que no es necesario especificar lo mismo dos veces.
```

-   Recrea el código R necesario para generar los siguientes gráficos:

``` r
#a
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
#b
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_smooth(aes(group = traccion), se = FALSE) +
  geom_point()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-2.png)<!-- -->

``` r
#c
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista, color = traccion)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-3.png)<!-- -->

``` r
#d
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_point(aes(color = traccion)) +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-4.png)<!-- -->

``` r
#e
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_point(aes(color = traccion)) +
  geom_smooth(aes(linetype = traccion), se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-5.png)<!-- -->

``` r
#f
ggplot(data = millas, mapping = aes(x = cilindrada, y = autopista)) +
  geom_point(size = 4, colour = "white") +
  geom_point(aes(colour = traccion))
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-22-6.png)<!-- -->

### Parte 5: Gráficos estadísticos

-   ¿Cuál es el geom predeterminado asociado con stat_summary()? ¿Cómo
    podrías reescribir el gráfico anterior para usar esa función geom en
    lugar de la función stat?

-   ¿Qué hace geom_col()? ¿En qué se diferencia de geom_bar()?

-   La mayoría de los geoms y las transformaciones estadísticas vienen
    en pares que casi siempre se usan en conjunto. Lee la documentación
    y haz una lista de todos los pares. ¿Qué tienen en común?

``` r
#geometría      #estadístico
#geom_bar()     stat_count()
#geom_bin2d()     stat_bin_2d()
#geom_boxplot() stat_boxplot()
#geom_contour() stat_contour()
#geom_count()    stat_sum()
#geom_density() stat_density()
#geom_qq_line() stat_qq_line()
#geom_qq()        stat_qq()
#geom_quantile()    stat_quantile()
#geom_smooth()    stat_smooth()
#geom_violin()    stat_violin()
#geom_density_2d()  stat_density_2d()
#geom_hex() stat_hex()
#geom_freqpoly()    stat_bin()
#geom_histogram()   stat_bin()
#geom_sf()          stat_sf()

#los nombres suelen ser similares como geom_qq() y stat_qq().
```

-   ¿Qué variables calcula stat_smooth()? ¿Qué parámetros controlan su
    comportamiento?

``` r
#stat_smooth() calcula las variables..... y: valor predicho, ymin: menor valor del intervalo de confianza,ymax: mayor valor del intervalo de confianza y se: error estándar.
#Los parámetros que controlan a stat_smooth() son: method, formula y na.rm.
```

-   En nuestro gráfico de barras de proporción necesitamos establecer
    group = 1. ¿Por qué? En otras palabras, ¿cuál es el problema con
    estos dos gráficos?

### Parte 6: Ajuste de posición

-   ¿Cuál es el problema con este gráfico? ¿Cómo podrías mejorarlo?

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

``` r
#Como se ve en el grafico existe superposición por las multiples observaciones 
#Para las conbincaciones de ciudad y autopista .
#Se puede arreglar usando el argumento de distorción .

ggplot(data = millas, mapping = aes(x = ciudad , y = autopista)) + 
  geom_point(position = "jitter")
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-28-2.png)<!-- -->

-   ¿Qué parámetros de geom_jitter() controlan la cantidad de ruido?

``` r
#los paramétros que controlan la cantidad de ruido son : 
#width (desplazamiento vertical) y height (desplazamiento horizontal)
```

-   Compara y contrasta geom_jitter() con geom_count()

``` r
# diferencias entre 
#geom_jitter: distorsiona la ubicación de los puntos en el grafico, 
#esto causa la disminución en la superposición ya que cuando se mueven
#los puntos es pococ probable que se ubiquen en el mismo lugar.

#geom_count:en cambio este parametro cambia el tamaño de los puntos 
#este aumento de tamaño de los puntos si bien no distorciona los valores causa 
#superposición.
```

-   ¿Cuál es el ajuste de posición predeterminado de geom_boxplot()?
    Crea una visualización del conjunto de datos de millas que lo
    demuestre.

``` r
#El ajuste predeterminado de geom_boxplot() es position_dodge2
#este ajuste nmueve las geometrias horizontalmente para evitar la superposción
```

### Parte 7: Sistema de coordenadas

-   Convierte un gráfico de barras apiladas en un gráfico circular
    usando coord_polar().

``` r
grafico_base3 <- ggplot(data=millas,aes(x=ciudad))+ 
  geom_bar(fill="Red3")
grafico_base3+theme_classic()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

``` r
grafico_base3+coord_polar()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-32-2.png)<!-- -->

-   ¿Qué hace labs()? Lee la documentación.

``` r
help(labs)
#Permite modificar las etiquetas de ejes, leyendas y gráficos. La personalización de etiquetas ayuda al mejor entendimiento de lo que se muestra en un plot
```

-   ¿Cuál es la diferencia entre coord_quickmap() y coord_map()?

``` r
#coord_map() proyecta una parte de la tierra en un plano 2D usando una proyección definida por el paquete mapproj, las proyecciones que usa no conservan las líneas rectas; coord_quickmap() conserva las líneas rectas y es más útil para áreas pequeñas cercanas al Ecuador.
```

-   ¿Qué te dice la gráfica siguiente sobre la relación entre ciudad y
    autopista? ¿Por qué es coord_fixed() importante? ¿Qué hace
    geom_abline()?

``` r
ggplot(data = millas, mapping = aes(x = ciudad, y = autopista)) +
  geom_point() +
  geom_abline() +
  coord_fixed()
```

![](Tarea-4_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

``` r
#La gráfica muestra que la cantidad de millas por galón de combustible en autopista ha ido en ascenso, paralelo a la línea de referencia.
#coord_fixed() es importante porque fuerza a que las unidades del eje x y eje y mantengan una relación fija.
#geom_abline() agrega líneas de referencia (reglas) a una parcela, estas pueden ser horizontal, vertical o diagonal. Útil para anotar parcelas.
```
