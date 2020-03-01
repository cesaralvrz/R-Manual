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
