# R-Manual
![](img/ManualR.jpg)


R es un entorno y lenguaje de programación con un enfoque al análisis estadístico. R nació como una reimplementación de software libre del lenguaje S.

Información recaudada del curso de 'Programación en R' de [OpenWebinars](openwebinars.net)

## Primer “Hola Mundo” en R
En todo lenguaje de programación lo primero que se aprende es escribir nuestro primer “Hola Mundo”. En R este se inscribe utilizando la función ‘print()’ y dentro de los paréntesis escribimos con comillas el texto que queremos visualizar.

```r
print("Hola Mundo")
```


## Estructura del lenguaje
R nos permite asignar valores a diferentes atributos y poder hacer  operaciones con estos. En el ejemplo siguiente asignaremos el valor de 4 a ‘a’ y de 5 a ‘b’. Para luego sumarlos y asignar ese valor a c. El resultado de c lo visualizaremos en la consola (9):

```r
a = 4
b = 5
c = a + b
print(c)
```


El uso de las llaves ‘{}’ no es necesario si queremos lanzar una única instrucción.
```r
if(a == 2)
  print("Hola Mundo")
  print("Sí es un dos")
```


En el caso de querer lanzar más de una instrucción, sí son necesidad las llaves ‘{}’
```r
if(a == 2) {
  print("Hola Mundo")
  print("Sí es un dos")
} else {
  print("Hola Mundo, no es dos")
}
```


El punto y coma, no es obligatorio si escribimos una instrucción por línea. Del mismo modo, sí lo es si queremos escribir varias instrucciones por linea.
```r
# Error
print("Hola") print("Adios")
# Ok
print("Hola"); print("Adios")
```


## Trabajar con Variables

Por defecto, el asignador en R es la función *<-* o *->*. También se puede realizar la asignación con el signo *=*:
```r
 a <- 4
 3 -> b
 a
[1] 4
 b
[1] 3
 c = 5
 c
[1] 5
```

También, podemos realizar la asignación mediante la función *assign* o asignar un valor resultado:
```r
> assign("x", "hola")
> x
[1] "hola"

# Podemos asignar el valor de un resultado
> a
[1] 4
> b
[1] 3
> y = a > b
> y
[1] TRUE
> z = a + b
> z
[1] 7

# La función ifelse(x,y,z) devuelve el valor y si la condición x es TRUE o z si x = FALSE
> mayor = ifelse(a > b , a , b)
> mayor
[1] 4
```


Las variables se irán guardando en memoria conforme se vayan creando. Podemos recuperar un listado de todas variables con la función *objects* o *ls*
```r
> objects()
 [1] "a"            "b"            "c"            "x"       "z"  "mayor" 
> ls()
 [1] "a"            "b"            "c"            "x"       "z"  "mayor" 

# Con la función object.size podemos recuperar el tamaño de una variable
> x
[1] "hola"
> object.size(x)
96 bytes
```


También podemos eliminar variables.
```r
> remove(a)
> a
Error: object 'a' not found
> objects()
 [1] "b"            "c"            "x"       "z"  "mayor"
```

La función *save.image* nos permite guardar todas las variables que tenemos en memoria. Con la función *load* podemos cargar dichas variables.
```r
> save.image(file = "variables.RData")
> remove(list = ls())
> ls()
character(0)
> objects()
character(0)
> load(file = "variables.RData")
> ls()
[1] "a"     "b"     "c"     "mayor" "x"
```
## Funciones predefinidas


![](img/ss1.png)


![](img/ss2.png)


![](img/ss3.png)


Datos Básicos (simples)
En R, vamos a distinguir 5 tipos básicos de datos.

### Numeric
Los números decimales en R son de tipo *numeric*.
```r
> x = 23.4
> x
[1] 23.4
> class(x)
[1] "numeric"
> typeof(a)
[1] "double"
```

Tenemos que tener en cuenta que aunque establezcamos la variable con un número entero, por defecto se asigna a un tipo *numeric*.
```r
> a <- 4
> class(a)
[1] "numeric"
> typeof(a)
[1] "double"
> is.integer(a)
[1] FALSE
```


### Integer

Para poder crear una variable de tipo *integer* debemos utilizar la función *as.integer*.
```r
> i = as.integer(4)
> class(i)
[1] "integer"
> typeof(i)
[1] "integer"
> is.integer(i) 
[1] TRUE
```

La función *as.integer* puede recibir un valor decimal o incluso una cadena. Intentará pasar el valor y en el caso de no poder, devuelve un error.
```r
> d = as.integer(3.43)
> d
[1] 3
> is.integer(d)
[1] TRUE
> d = as.integer("4.4")
> d
[1] 4
> is.integer(s)
[1] TRUE
> d = as.integer("Hola")
Warning message:
NAs introduced by coercion 
> d
[1] NA
```


### Complex

R también nos permite el uso de números complejos, los cuales recordemos tienen una parte real y una parte imaginaria.
```r
> a = 2i + 2
> a
[1] 2+2i
> class(a)
[1] "complex"
> b = complex(real = 2, imaginary = 2)
> b
[1] 2+2i

> c = as.complex(3)
> c
[1] 3+0i
> class(c)
[1] "complex"
```

### Logical

Los valores lógicos en R son /TRUE/ y /FALSE/. Estos valores suelen ser creados a partir de comparaciones entre otras variables.
```r
> a = 4
> b = 5
> a < b
[1] TRUE
> a > b
[1] FALSE
> a == b
[1] FALSE
> a == 4
[1] TRUE
> a != 4
[1] FALSE
```

Además, tenemos la función *as.logical(x)* . Está función devuelve FALSE si x == 0 y TRUE si x != 0.
```r
> as.logical(0)
[1] FALSE
> as.logical(1.1)
[1] TRUE
> as.logical(3)
[1] TRUE
> as.logical(-3)
[1] TRUE
> as.logical(-0)
[1] FALSE
> as.logical(0.1)
[1] TRUE
```

### Character

Un objeto carácter es usado para la representación de cadenas.
```r
> cadena = "hola"
> cadena
[1] "hola"
> typeof(cadena)
[1] "character"
> class(cadena)
[1] "character
```

Existen numerosas funciones para trabajar con cadenas. Por ejemplo:
```r
> nombre = "Abraham" ; apellido = "Requena"
> paste(nombre, apellido)
[1] "Abraham Requena"
> edad = 24
> sprintf("%s tiene %d años", nombre, edad)
[1] "Abraham tiene 24 años"
```

n la función ‘sprintf’ , para crear la cadena con los distintos tipos de datos básicos debemos usar:
* `%d, i` → Para mostrar valores numéricos.
* `%s` → Para mostrar cadenas.
* `%f` → Para mostrar valores numéricos decimales
* `e` → Para mostrar valores numéricos en notación exponencial


### Vectores Lógicos

Son vectores formados únicamente por valores TRUE o FALSE.
* `<`  (menor)
* `<=`  (menor o igual)
* `>`  (mayor)
* `>=`  (mayor o igual)
* `==`  (igual)
* `!=`  (distinto).
* `&&`  (conjunción)
* `||`  (disyunción)

Dichos valores lógicos tienen su valor numérico. Siendo FALSE = 0 y TRUE = 1. De esta forma:
```r
> t[1] + t[2]
[1] 1
> t[1] + t[3]
[1] 2
> 30*t[1]
[1] 30
> 30*t[2]
[1] 0
```


### Vectores faltantes

También pueden existir valores faltantes o sin valor en un vector. Estos valores se representan mediante la palabra reservada *NA* o *NaN*.
```r
> z = c(1,3,4, NA)
> z
[1]  1  3  4 NA
> is.na(z)
[1] FALSE FALSE FALSE  TRUE
> 3/0
[1] Inf
> 0/0
[1] NaN
> Inf - Inf
[1] NaN
> c = c(4,3,0,4)
> a = c(2,3,0,4)
> res = c/a
> res
[1]   2   1 NaN   1
```

Existen multitud de funciones para trabajar con vectores. A continuación vamos a enumerar algunas de ellas.
* `NROW(x)`
* `which.max(x)`
* `which.min(x)`
* `sort(x)`
* `rev(x)`
* `which(x)`
* `range(x)`
* `mean(x)`
* `summary(x)`

```r
> v = c(1:10)
> v
 [1]  1  2  3  4  5  6  7  8  9 10
> NROW(v)
[1] 10
> # Para comprobar su valor maximo
> which.max(v)
[1] 10
> # Para comprobar su valor minimo
> which.min(v)
[1] 1
> # Creamos un nuevo vector para ordenarlo
> c = c(3,10,5,43, 40)
> c
[1]  3 10  5 43 40
> sort(c)
[1]  3  5 10 40 43
> # Para hacer el reverse del vector
> rev(c)
[1] 40 43  5 10  3
> # Podemos ordenar descendentemente
> rev(sort(c))
[1] 43 40 10  5  3
> # Con la función which, obtenemos los indices de los valores que cumplen la condicion
> which(c == 5)
[1] 3
> # Range nos devuelve el valor minimo y maximo del vector
> range(c)
[1]  3 43
# Podemos calcular la media de un vector con la funcion mean
> mean(c)
[1] 20.2
# El summary nos devuelve varios calculos sobre el vector
> summary(c)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    3.0     5.0    10.0    20.2    40.0    43.0
```


## Datos Complejos
### Listas

Las listas pueden definirse como vectores en los cuales los elementos no tienen porque ser del mismo tipo. Cada uno de los elementos de una lista, los cuales pueden de diferente *mode* (vector, matrix, …) son conocidos como componentes.
Para crear listas, usaremos la función *list()* y cada componente tendrá asignado un nombre.
```r
> lista = list(empresa="Openwebinars", empleados.numero = 5, empleados.edad = c(25,30,27,28,22))
> # Para consultar algun elemento de la lista utilizamos el operador [[]]
> lista[[1]]
[1] "Openwebinars"
> lista[[3]]
[1] 25 30 27 28 22
> # Tambien podemos utilizar el operador $ usando el nombre
> lista$empleados.numero
[1] 5

# lista$edad es un vector, por lo que podemos consultarlo con el operador []
> lista$empleados.edad[1]
[1] 25
# También podemos usar el operador [] con los nombre de las variables.
> lista[["empresa"]]
[1] "Openwebinars"
```

Además, el operador *$* nos permite realizar la *consulta* de una forma abreviada. Veamos un ejemplo.
```r
# lista$empleados.n solo puede corresponderse con lista$empleados.numero
> lista$empleados.n
[1] 5
> lista$empleados.e
[1] 25 30 27 28 22
```

Podemos *añadir* nuevos campos o *modificar* campos ya existentes en las listas.
```r
> lista[[4]] = list(nombre="cursos", cursos.num = 10)
> lista
$empresa
[1] "Openwebinars"

$empleados.numero
[1] 5

$empleados.edad
[1] 25 30 27 28 22

[[4]]
[[4]]$nombre
[1] "cursos"

[[4]]$cursos.num
[1] 10

Al consultar el 4 elemento del objeto 'lista' obtendremos una nueva lista con dos campos.
> lista[[4]]
$nombre
[1] "cursos"

$cursos.num
[1] 10

> lista[[4]]$nombre
[1] "cursos"
# Si usamos la función is.list(), comprobaremos que ambos campos son de tipo list.
> is.list(lista)
[1] TRUE
> is.list(lista[[4]])
[1] TRUE
```

Por último, también podemos *concatenar* listas usando la función `c()`
```r
> lista2 = list(año = 2014, ciudad = "Sevilla")
> conca = c(lista, lista2)
> conca
$empresa
[1] "Openwebinars"

$empleados.numero
[1] 5

$empleados.edad
[1] 25 30 27 28 22

[[4]]
[[4]]$nombre
[1] "cursos"

[[4]]$cursos.num
[1] 10

$año
[1] 2014

$ciudad
[1] "Sevilla"

> conca$ciudad
[1] "Sevilla"

> is.list(conca)
[1] TRUE
```


### Función lapply() y sapply()

Las funciones *lapply* y *sapply* nos permiten aplicar una función a todos los elementos de una lista o un vector.
La función /lapply/ devuelve una lista.
```r
> l = list(x = c(3,4,1,3), y = c(3,4,4,12), z = c(5,7,3,6))
> l
$x
[1] 3 4 1 3

$y
[1]  3  4  4 12

$z
[1] 5 7 3 6

> lapply(l, mean)
$x
[1] 2.75

$y
[1] 5.75

$z
[1] 5.25
```

Mientras que la función /sapply/ devuelve un vector
```r
> sumatorio = sapply(l, sum)
> sumatorio
 x  y  z 
11 23 21 
> is.vector(sumatorio)
[1] TRUE
```

### Factores

Los factores son otro tipo de vector, en este caso utilizado para mostrar algún tipo de clasificación discreta de los elementos de otro vector de igual tamaño. Veamos un ejemplo:
```r
# ALEMANIA    DE
# AUSTRIA     AT
# BELGICA    BE
# BULGARIA    BG
# HUNGRIA    HU
# ESPAÑA    ES
# FRANCIA    FR
# REPUBLICA CHECA    CZ
# PORTUGAL    PT
# REINO UNIDO    GB
> personas <- c("DE","BG","ES","AT","BE","FR","BG","HU","HU","ES","DE","FR","GB","CZ","PT","ES","GB","FR","BG","CZ","BG","FR","PT","ES","BE","AT","DE","CZ","ES","GB")

> factor = factor(personas)
> factor
 [1] DE BG ES AT BE FR BG HU HU ES DE FR GB CZ PT ES GB FR BG CZ BG FR PT ES BE AT DE CZ ES GB
Levels: AT BE BG CZ DE ES FR GB HU PT
```

Podemos consultar los distintos valores que tiene el factor con la función *levels*. Esta función nos devuelve un tipo vector.
```r
> levels(factor)
 [1] "AT" "BE" "BG" "CZ" "DE" "ES" "FR" "GB" "HU" "PT"

> typeof(levels(factor))
[1] "character"
> is.vector(levels(factor))
[1] TRUE
```

Pero, *¿dónde está la utilidad de los factores?* . Sigamos.
Vamos a tener ahora un vector del mismo tamaño con el número de hijos de cada persona.
```r
> numHijos = c(2,3,1,0,0,2,5,1,3,2,0,3,4,2,1,1,1,0,3,2,1,1,2,2,1,4,2,3,4,0)
> numHijos
 [1] 2 3 1 0 0 2 5 1 3 2 0 3 4 2 1 1 1 0 3 2 1 1 2 2 1 4 2 3 4 0
> NROW(numHijos)
[1] 30
```

Ahora, podemos usar la función *tapply* para calcular operaciones muestrales. Por ejemplo, podemos calcular la media de hijos por países.
```r
> mediaHijos <- tapply(numHijos, factor, mean)
> mediaHijos
      AT       BE       BG       CZ       DE       ES       FR       GB       HU       PT 
2.000000 0.500000 3.000000 2.333333 1.333333 2.000000 1.500000 1.666667 2.000000 1.500000

# Podemos realizar consultas por nombre o por indice
> mediaHijos["ES"]
ES 
 2 
> mediaHijos[4]
      CZ 
2.333333
```


## Arrays/Matrices
Podemos transformar un vector en una variable indexada asignándole unas dimensiones. Para ello, usamos la función *dim*.
```r
> v = c(1:20)
> v
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20
> dim(v) = c(5,4)
> v
     [,1] [,2] [,3] [,4]
[1,]    1    6   11   16
[2,]    2    7   12   17
[3,]    3    8   13   18
[4,]    4    9   14   19
[5,]    5   10   15   20
```

Acabamos de convertir un vector de 20 números, en un array de *5 x 4* valores. Si nos fijamos, el orden en rellenar los valores es ### [1,1],[2,1],[3,1],…,[4,3],[4,4],[4,5]
 .
También podemos crear un vector con más de 2 dimensiones.
```r
> dim(v) = c(5,2,2)
> v
, , 1

     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10

, , 2

     [,1] [,2]
[1,]   11   16
[2,]   12   17
[3,]   13   18
[4,]   14   19
[5,]   15   20
```

Del mismo modo que asignamos dimensiones a un vector, podemos consultar las dimensiones de un array.
```r
> dim(v)
[1] 5 2 2
```

A la hora de consultar un array, podemos fijar todas sus dimensiones, o solo algunas de ellas. Veamos ejemplo:
```r
# Consultamos x=1, y=2, z=1
> v[1,2,1]
[1] 6

# Consultamos todos los valores de x donde y=1, z=1. 
> v[,1,1]
[1] 1 2 3 4 5

# Consultamos todos los valores de x e y donde z=1.
> v[,,2]
     [,1] [,2]
[1,]   11   16
[2,]   12   17
[3,]   13   18
[4,]   14   19
[5,]   15   20

# Consultamos el array completo. Identico a ejecutar 'v'.
> v[,,]
, , 1

     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10

, , 2

     [,1] [,2]
[1,]   11   16
[2,]   12   17
[3,]   13   18
[4,]   14   19
[5,]   15   20

# Consultamos las 3 primeras filas.
> v[c(1:3),1,]
     [,1] [,2]
[1,]    1   11
[2,]    2   12
[3,]    3   13
```


### Definición de Arrays/Matrices usando un constructor

Para definir un array o una matriz, R también nos proporciona un constructor por defecto. En concreto son las funciones *array* y *matrix*. A continuación vamos a utilizar esas funciones para crear nuevos arrays y matrices.
```r
> arr <- array(data = c(1:20), dim = c(5,2,2))
> arr
, , 1

     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10

, , 2

     [,1] [,2]
[1,]   11   16
[2,]   12   17
[3,]   13   18
[4,]   14   19
[5,]   15   20

> mat = matrix(data = c(1:20), nrow = 5, ncol = 4)
> mat
     [,1] [,2] [,3] [,4]
[1,]    1    6   11   16
[2,]    2    7   12   17
[3,]    3    8   13   18
[4,]    4    9   14   19
[5,]    5   10   15   20

# También podemos crear variables indexadas con valores 0
> arrayCero = array(0, dim = c(3,5))
> arrayCero
     [,1] [,2] [,3] [,4] [,5]
[1,]    0    0    0    0    0
[2,]    0    0    0    0    0
[3,]    0    0    0    0    0
```


### Reciclado

También debemos tener en cuenta que, si el vector de datos es menor que el tamaño de la dimensión, los elementos se irán repitiendo. Del mismo modo, sí establecemos una dimensión menor que el tamaño del vector, solo se añadirán a la matriz/array los elementos que entren en la dimensión. Esto se conoce como /reciclado/.
```r
# Tamaño vector < Tamaño dimension
> mat = matrix(data = c(1:20), nrow = 5, ncol = 8)
> mat
     [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8]
[1,]    1    6   11   16    1    6   11   16
[2,]    2    7   12   17    2    7   12   17
[3,]    3    8   13   18    3    8   13   18
[4,]    4    9   14   19    4    9   14   19
[5,]    5   10   15   20    5   10   15   20

# Tamaño vector > Tamaño dimensión
> mat = matrix(data = c(1:20), nrow = 5, ncol = 2)
> mat
     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10
```


### Expresiones Aritméticas

Las variables indexadas también pueden ser utilizadas en operaciones aritméticas. Los operandos de una operación aritmética deben tener la misma dimensión, la cual se corresponderá también con la dimensión del resultado.
```r
> x = matrix(data = c(c(3,4), c(6,3)), nrow = 2, ncol = 2)
> x
     [,1] [,2]
[1,]    3    6
[2,]    4    3

> y = matrix(data = c(c(2,1), c(4,2)), nrow = 2, ncol = 2)
> y
     [,1] [,2]
[1,]    2    4
[2,]    1    2

> z = x * y + 1
> z
     [,1] [,2]
[1,]    7   25
[2,]    5    7

> dim(x) == dim(y) && dim(y) == dim(z)
[1] TRUE
```

Un ejemplo de /reciclado/ en operaciones sería.
```r
> x
     [,1] [,2]
[1,]    3    6
[2,]    4    3
> vec = c(2,3)
> x * vec
     [,1] [,2]
[1,]    6   12
[2,]   12    9
```


### Funciones rowsum, colsum, rowMeans, colMeans

Es habitual, tener que realizar operaciones con las columnas o filas de las matrices. Estas 4 funciones nos facilita el sumatorio o la media de cada una de ellas. Su uso es muy simple.

```r
> matriz = matrix(1:10, nrow = 5, ncol = 2)
> matriz
     [,1] [,2]
[1,]    1    6
[2,]    2    7
[3,]    3    8
[4,]    4    9
[5,]    5   10
> rowSums(matriz)
[1]  7  9 11 13 15
> colSums(matriz)
[1] 15 40
> rowMeans(matriz)
[1] 3.5 4.5 5.5 6.5 7.5
> colMeans(matriz)
[1] 3 8
```

### Producto Exterior

El producto exterior de 2 matrices se realiza multiplicando cada elemento de la primera matriz por todos los elementos de la segunda matriz. La dimensión de la variable resultado sería *dim(x)*dim(y)*.

* `outer(x,y, “*”)`  -> Multiplicación
* `outer(x, y, “+”)` -> Suma
* `outer(x, y, “-“)` -> Resta
* `outer(x, y, “/“)` -> División

```r
> x = matrix(data = c(c(3,4), c(6,3)), nrow = 2, ncol = 2)
> x
     [,1] [,2]
[1,]    3    6
[2,]    4    3
> y = matrix(data = c(c(2,1), c(4,2)), nrow = 2, ncol = 2)
> y
     [,1] [,2]
[1,]    2    4
[2,]    1    2
> 
> # Para hacer el producto exterior, podemos:
> outer(x,y, "*")
, , 1, 1

     [,1] [,2]
[1,]    6   12
[2,]    8    6

, , 2, 1

     [,1] [,2]
[1,]    3    6
[2,]    4    3

, , 1, 2

     [,1] [,2]
[1,]   12   24
[2,]   16   12

, , 2, 2

     [,1] [,2]
[1,]    6   12
[2,]    8    6

> # O también podemos utlizar el operador %o%
> x %o% y
, , 1, 1

     [,1] [,2]
[1,]    6   12
[2,]    8    6

, , 2, 1

     [,1] [,2]
[1,]    3    6
[2,]    4    3

, , 1, 2

     [,1] [,2]
[1,]   12   24
[2,]   16   12

, , 2, 2

     [,1] [,2]
[1,]    6   12
[2,]    8    6
```


## DataFrame
Otro tipo de dato complejo son los *DataFrame* o hojas de datos. Los DataFrame son un tipo similar a las matrices, teniendo un número de filas y de columnas. Para crear un dataframe, todos los elementos deben tener el mismo tamaño de filas y usaremos la función *data.frame()*. Puede recibir como entrada:
* Vector
* Factor
* Matriz
* Lista

```r
> vector = c("Francia","Alemania","Italia","Portugal","Suiza")
> factor = factor(vector)
> lista = list(c(2,2,3,4,5))
> matriz = matrix(c(1:25), nrow = 5, ncol = 5)

> dataFrame = data.frame(f = factor, m = matriz, row.names = 1)
> dataFrame
         m.1 m.2 m.3 m.4 m.5
Francia    1   6  11  16  21
Alemania   2   7  12  17  22
Italia     3   8  13  18  23
Portugal   4   9  14  19  24
Suiza      5  10  15  20  25
> dataFrame$m.1
[1] 1 2 3 4 5
> dataFrame["Alemania",]
         m.1 m.2 m.3 m.4 m.5
Alemania   2   7  12  17  22
> dataFrame["Alemania",4]
[1] 17
```

Además, podemos añadir nuevas variables a un dataframe con el operando asignación *$*.

```r
> mtcars$nuevaVariable <- c(1:32)
> mtcars
                     mpg cyl  disp  hp drat    wt  qsec vs am gear carb nuevaVariable
Mazda RX4           21.0   6 160.0 110 3.90 2.620 16.46  0  1    4    4             1
Mazda RX4 Wag       21.0   6 160.0 110 3.90 2.875 17.02  0  1    4    4             2
Datsun 710          22.8   4 108.0  93 3.85 2.320 18.61  1  1    4    1             3
Hornet 4 Drive      21.4   6 258.0 110 3.08 3.215 19.44  1  0    3    1             4
Hornet Sportabout   18.7   8 360.0 175 3.15 3.440 17.02  0  0    3    2             5
Valiant             18.1   6 225.0 105 2.76 3.460 20.22  1  0    3    1             6
Duster 360          14.3   8 360.0 245 3.21 3.570 15.84  0  0    3    4             7
Merc 240D           24.4   4 146.7  62 3.69 3.190 20.00  1  0    4    2             8
Merc 230            22.8   4 140.8  95 3.92 3.150 22.90  1  0    4    2             9
Merc 280            19.2   6 167.6 123 3.92 3.440 18.30  1  0    4    4            10
Merc 280C           17.8   6 167.6 123 3.92 3.440 18.90  1  0    4    4            11
Merc 450SE          16.4   8 275.8 180 3.07 4.070 17.40  0  0    3    3            12
Merc 450SL          17.3   8 275.8 180 3.07 3.730 17.60  0  0    3    3            13
Merc 450SLC         15.2   8 275.8 180 3.07 3.780 18.00  0  0    3    3            14
Cadillac Fleetwood  10.4   8 472.0 205 2.93 5.250 17.98  0  0    3    4            15
Lincoln Continental 10.4   8 460.0 215 3.00 5.424 17.82  0  0    3    4            16
Chrysler Imperial   14.7   8 440.0 230 3.23 5.345 17.42  0  0    3    4            17
Fiat 128            32.4   4  78.7  66 4.08 2.200 19.47  1  1    4    1            18
Honda Civic         30.4   4  75.7  52 4.93 1.615 18.52  1  1    4    2            19
Toyota Corolla      33.9   4  71.1  65 4.22 1.835 19.90  1  1    4    1            20
Toyota Corona       21.5   4 120.1  97 3.70 2.465 20.01  1  0    3    1            21
Dodge Challenger    15.5   8 318.0 150 2.76 3.520 16.87  0  0    3    2            22
AMC Javelin         15.2   8 304.0 150 3.15 3.435 17.30  0  0    3    2            23
Camaro Z28          13.3   8 350.0 245 3.73 3.840 15.41  0  0    3    4            24
Pontiac Firebird    19.2   8 400.0 175 3.08 3.845 17.05  0  0    3    2            25
Fiat X1-9           27.3   4  79.0  66 4.08 1.935 18.90  1  1    4    1            26
Porsche 914-2       26.0   4 120.3  91 4.43 2.140 16.70  0  1    5    2            27
Lotus Europa        30.4   4  95.1 113 3.77 1.513 16.90  1  1    5    2            28
Ford Pantera L      15.8   8 351.0 264 4.22 3.170 14.50  0  1    5    4            29
Ferrari Dino        19.7   6 145.0 175 3.62 2.770 15.50  0  1    5    6            30
Maserati Bora       15.0   8 301.0 335 3.54 3.570 14.60  0  1    5    8            31
Volvo 142E          21.4   4 121.0 109 4.11 2.780 18.60  1  1    4    2            32
> mtcars$nuevaVariable
 [1]  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32
```

Otra manera rápida de crear un data frame es leyendo *datos de un fichero*, aunque eso lo veremos en una lección posterior, donde vemos cómo trabajar con ficheros.
Por defecto, R nos trae algunos data frame con los que poder trabajar. Por ejemplo, está el dataframe /mtcars/. A continuación, vamos a trabajar con dicho dataFrame.

```r
> help(mtcars)
> colnames(mtcars)
 [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear" "carb"
> colnames(mtcars)
 [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear" "carb"
> help(mtcars)
> colnames(mtcars)
 [1] "mpg"  "cyl"  "disp" "hp"   "drat" "wt"   "qsec" "vs"   "am"   "gear" "carb"
> rownames(mtcars)
 [1] "Mazda RX4"           "Mazda RX4 Wag"       "Datsun 710"          "Hornet 4 Drive"     
 [5] "Hornet Sportabout"   "Valiant"             "Duster 360"          "Merc 240D"          
 [9] "Merc 230"            "Merc 280"            "Merc 280C"           "Merc 450SE"         
[13] "Merc 450SL"          "Merc 450SLC"         "Cadillac Fleetwood"  "Lincoln Continental"
[17] "Chrysler Imperial"   "Fiat 128"            "Honda Civic"         "Toyota Corolla"     
[21] "Toyota Corona"       "Dodge Challenger"    "AMC Javelin"         "Camaro Z28"         
[25] "Pontiac Firebird"    "Fiat X1-9"           "Porsche 914-2"       "Lotus Europa"       
[29] "Ford Pantera L"      "Ferrari Dino"        "Maserati Bora"       "Volvo 142E"         
> dim(mtcars)
[1] 32 11

> mtcars$cyl
 [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
> mtcars["Mazda RX4",]
          mpg cyl disp  hp drat   wt  qsec vs am gear carb
Mazda RX4  21   6  160 110  3.9 2.62 16.46  0  1    4    4
```


### Funciones attach() y detach()

A veces, cuando trabajamos con dataFrames nos puede interesar poder consultar las variables directamente, en lugar de usar el operador *$*. Para ello, podemos usar la función *attach()*.

```r
> cyl
Error: object 'cyl' not found
> mtcars$cyl
 [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
> attach(mtcars)
> cyl
 [1] 6 6 4 6 8 6 8 4 4 6 6 8 8 8 8 8 8 4 4 4 4 8 8 8 8 4 4 4 8 6 8 4
```

Tenemos que tener cuidado con el uso de attach, para asegurarnos que no tenemos ninguna variable con el mismo nombre antes de aplicar la función.

```r
> cyl = 2
> cyl
[1] 2
> attach(mtcars)
The following object is masked _by_ .GlobalEnv:

    cyl
```

Del mismo modo, existe la función contraria *detach()*

```r
> detach(mtcars)
> cyl
Error: object 'cyl' not found
```



## Ficheros

Hasta ahora hemos estado conociendo la base del lenguaje, su estructura y los tipos de datos. Pero cuando trabajamos en el mundo real, es habitual que los datos procedan de ficheros. Durante esta lección vamos a ir conociendo cómo trabajar con los ficheros en R.
Lo primero que tenemos que conocer a la hora de trabajar con ficheros en R es la existencia de un workspace, o espacio de trabajo donde encontraremos los diferentes ficheros con los que queramos trabajar. Para configurar el espacio de trabajo usaremos la función *setwd* o la opción que nos proporciona RStudio.

```r
> setwd("D:/R-WS")
```

### Función read.fwf()

La función *read.fwf* se usa para leer ficheros con campos de tamaño fijo, es decir, no se encuentran delimitados por un separador. Para ello, vamos a usar el fichero /“FicheroSinSeparador.txt”/ .
* *skip*: Establece el número de líneas que no se ignoran antes de los datos.
* *widths*: Vector con el tamaño de cada campo.

```r
> f = read.fwf(file = "FicheroSinSeparador.txt", skip = 3, widths = c(10,2,9))
> f
          V1 V2        V3
1 123456789A 25 456487841
2 987654321Z 44 881452145
3 123789456N 22 841414487
4 222333447R 18 547847410
> f = read.fwf(file = "FicheroSinSeparador.txt", skip = 3, widths = c(10,2,9), col.names = c("DNI","Edad","Telefono"), row.names = c("Juan","Maria","Antonio","Ana"))
> f
               DNI Edad  Telefono
Juan    123456789A   25 456487841
Maria   987654321Z   44 881452145
Antonio 123789456N   22 841414487
Ana     222333447R   18 547847410
> is.data.frame(f)
[1] TRUE

> f["Ana", ]
           DNI Edad  Telefono
Ana 222333447R   18 547847410
```


### Función read.table()

La función /read.table/, nos permite leer un fichero cuyos campos están separados por un carácter. Algunos de sus argumentos son:
* *file*: Fichero a leer.
* *header*: TRUE o FALSE, indica si existe linea de cabecera.
* *sep*: Carácter separador.
* *skip*: Número de líneas a ignorar antes de comenzar a leer.
* *blank.lines.skip* : Ignora las líneas en blanco.

```r
> file = read.table(file = "HairEyeColor.txt", header = TRUE, sep = "#", skip = 0)
> file
    X  Hair   Eye    Sex Freq
1   1 Black Brown   Male   32
2   2 Brown Brown   Male   53
3   3   Red Brown   Male   10
4   4 Blond Brown   Male    3
5   5 Black  Blue   Male   11
6   6 Brown  Blue   Male   50
7   7   Red  Blue   Male   10
8   8 Blond  Blue   Male   30
9   9 Black Hazel   Male   10
10 10 Brown Hazel   Male   25
11 11   Red Hazel   Male    7
12 12 Blond Hazel   Male    5
13 13 Black Green   Male    3
14 14 Brown Green   Male   15
15 15   Red Green   Male    7
16 16 Blond Green   Male    8
17 17 Black Brown Female   36
18 18 Brown Brown Female   66
19 19   Red Brown Female   16
20 20 Blond Brown Female    4
21 21 Black  Blue Female    9
22 22 Brown  Blue Female   34
23 23   Red  Blue Female    7
24 24 Blond  Blue Female   64
25 25 Black Hazel Female    5
26 26 Brown Hazel Female   29
27 27   Red Hazel Female    7
28 28 Blond Hazel Female    5
29 29 Black Green Female    2
30 30 Brown Green Female   14
31 31   Red Green Female    7
32 32 Blond Green Female    8
```

### Función scan()

Otra manera de leer, aunque más genérica y menos usada, es a través de la función *scan*. La función scan lee el contenido del fichero y lo almacena es un *vector.* Por defecto, el separador que utiliza es el espacio en blanco, aunque es configurable.

```r
> a = scan(file = "HairEyeColor.txt", what = "character", quiet = TRUE, sep = "#")
> a
  [1] ""       "Hair"   "Eye"    "Sex"    "Freq"   "1"      "Black"  "Brown"  "Male"   "32"     "2"     
 [12] "Brown"  "Brown"  "Male"   "53"     "3"      "Red"    "Brown"  "Male"   "10"     "4"      "Blond" 
 [23] "Brown"  "Male"   "3"      "5"      "Black"  "Blue"   "Male"   "11"     "6"      "Brown"  "Blue"  
 [34] "Male"   "50"     "7"      "Red"    "Blue"   "Male"   "10"     "8"      "Blond"  "Blue"   "Male"  
 [45] "30"     "9"      "Black"  "Hazel"  "Male"   "10"     "10"     "Brown"  "Hazel"  "Male"   "25"    
 [56] "11"     "Red"    "Hazel"  "Male"   "7"      "12"     "Blond"  "Hazel"  "Male"   "5"      "13"    
 [67] "Black"  "Green"  "Male"   "3"      "14"     "Brown"  "Green"  "Male"   "15"     "15"     "Red"   
 [78] "Green"  "Male"   "7"      "16"     "Blond"  "Green"  "Male"   "8"      "17"     "Black"  "Brown" 
 [89] "Female" "36"     "18"     "Brown"  "Brown"  "Female" "66"     "19"     "Red"    "Brown"  "Female"
[100] "16"     "20"     "Blond"  "Brown"  "Female" "4"      "21"     "Black"  "Blue"   "Female" "9"     
[111] "22"     "Brown"  "Blue"   "Female" "34"     "23"     "Red"    "Blue"   "Female" "7"      "24"    
[122] "Blond"  "Blue"   "Female" "64"     "25"     "Black"  "Hazel"  "Female" "5"      "26"     "Brown" 
[133] "Hazel"  "Female" "29"     "27"     "Red"    "Hazel"  "Female" "7"      "28"     "Blond"  "Hazel" 
[144] "Female" "5"      "29"     "Black"  "Green"  "Female" "2"      "30"     "Brown"  "Green"  "Female"
[155] "14"     "31"     "Red"    "Green"  "Female" "7"      "32"     "Blond"  "Green"  "Female" "8"     
> # Si queremos, podemos quitar la primera linea de cabecera
> a = scan(file = "HairEyeColor-CSV.csv", what = "character", quiet = TRUE, sep = ",", skip = 1)
> a
  [1] "1"      "Black"  "Brown"  "Male"   "32"     "2"      "Brown"  "Brown"  "Male"   "53"     "3"     
 [12] "Red"    "Brown"  "Male"   "10"     "4"      "Blond"  "Brown"  "Male"   "3"      "5"      "Black" 
 [23] "Blue"   "Male"   "11"     "6"      "Brown"  "Blue"   "Male"   "50"     "7"      "Red"    "Blue"  
 [34] "Male"   "10"     "8"      "Blond"  "Blue"   "Male"   "30"     "9"      "Black"  "Hazel"  "Male"  
 [45] "10"     "10"     "Brown"  "Hazel"  "Male"   "25"     "11"     "Red"    "Hazel"  "Male"   "7"     
 [56] "12"     "Blond"  "Hazel"  "Male"   "5"      "13"     "Black"  "Green"  "Male"   "3"      "14"    
 [67] "Brown"  "Green"  "Male"   "15"     "15"     "Red"    "Green"  "Male"   "7"      "16"     "Blond" 
 [78] "Green"  "Male"   "8"      "17"     "Black"  "Brown"  "Female" "36"     "18"     "Brown"  "Brown" 
 [89] "Female" "66"     "19"     "Red"    "Brown"  "Female" "16"     "20"     "Blond"  "Brown"  "Female"
[100] "4"      "21"     "Black"  "Blue"   "Female" "9"      "22"     "Brown"  "Blue"   "Female" "34"    
[111] "23"     "Red"    "Blue"   "Female" "7"      "24"     "Blond"  "Blue"   "Female" "64"     "25"    
[122] "Black"  "Hazel"  "Female" "5"      "26"     "Brown"  "Hazel"  "Female" "29"     "27"     "Red"   
[133] "Hazel"  "Female" "7"      "28"     "Blond"  "Hazel"  "Female" "5"      "29"     "Black"  "Green" 
[144] "Female" "2"      "30"     "Brown"  "Green"  "Female" "14"     "31"     "Red"    "Green"  "Female"
[155] "7"      "32"     "Blond"  "Green"  "Female" "8"     
> # O podemos leer una sola linea
> a = scan(file = "HairEyeColor-CSV.csv", what = "character", quiet = TRUE, sep = ",", skip = 1, nlines = 1)
> a
[1] "1"     "Black" "Brown" "Male"  "32"   
> is.data.frame(a)
[1] FALSE
> is.list(a)
[1] FALSE
> is.vector(a)
[1] TRUE
```

