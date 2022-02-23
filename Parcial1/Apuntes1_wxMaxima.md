# CAL 2122 - Apuntes parcial 1 wxMaxima

## SESIÓN 1 - 22/09 - Primeros pasos

#### Notas:

- Guardar en .wxmx
- Salida por defecto en una línea (lo que quepa). Para sacar los números completos:
  - Menú Maxima>Cambiar pantalla 2D>ascii
- Ctrl+1-6 celdas de texto (1 celda básica, 2-7 títulos)
- Menú Maxima>Reiniciar maxima para cuando se pilla

#### Operaciones y funciones elementales

- wxMaxima asume celdas de cálculo
  - %in para entradas
  - %on para salidas
- Acabar operaciones en ; para salida por pantalla
- Acabar operaciones en $ para sin salida por pantalla
- Shift+enter para calcular
- Historial:
  - % última respuesta
  - %on última n respuesta 

#### Funciones

| Función                | Significado                                                  |
| ---------------------- | ------------------------------------------------------------ |
| sqrt()                 | raíz cuadrada                                                |
| exp(), log()           | exponencial y logaritmo base e                               |
| sin(), cos(), tan()    | seno, coseno, tangente en radianes                           |
| asin(), acos(), atan() | arcoseno, arcocoseno, arcotangente en radianes               |
| sinh(), cosh(), tanh() | funciones hiperbólicas                                       |
| n!                     | factorial de n                                               |
| binomial(n,m)          | ![image-20210922104717274](/home/clara/.config/Typora/typora-user-images/image-20210922104717274.png) |
| entier()               | parte entera                                                 |
| abs()                  | valor absoluto (módulo)                                      |
| random(x)              | número aleatorio entre 0 y x, del mismo tipo que x           |

#### Constantes

- **%e** número e
- **%i** unidad imaginaria
- **%pi** número pi
- **%phi** razón áurea

#### Variables y funciones

- **Definir una variable:** `nombre: valor`
- **Definir una función:** `f(x):=sen(x)` o `define(f(x),sen(x))`

#### Números exactos y aproximados

- numer: true // numer: false para cambiar entre modo numérico o exacto (ej, ver raíz de 2 con el símbolo o ver 1.41.....)
- float() expresión decimal de un número
- bfloat() expresión decimal grande de un número

## SESIÓN 2 - 29/09 - Gráficos de funciones

#### Notas:

- En funciones potenciales, la monotonía depende de si el exponente es positivo (creciente) o negativo (decreciente)
- En funciones exponenciales, la monotonía depende de si la base es mayor que 1 (creciente), o menor (decreciente)
- Hiperbólicas:
  - Sinh(x)  = e^x - e^-x / 2
  - Cosh(x) = e^x + e^-x / 2
  - Tanh(x) = sinh(x) / cosh(x)

#### Funciones y gráficas con wxplot2d

- `:=` para definir funciones
- También comando `define(func, expr)`
  - Define es compatible con funciones internas (ej. derivadas e integrales)

- Para graficarlas, usamos `wxplot2d(expresión, [variable,mínimo,máximo],opciones)`
  - También sirve `plot2d`, pero con wx nos sale en la misma GUI el gráfico
  - Podremos dibujar varias funciones usando una lista dentro del primer parámetro: `wxplot2d([f(x),g(x)],[variable,mínimo,máximo],opciones)`
  - Para rectificar el tamaño del dominio y, añadimos otra lista de igual forma que lo hacemos con la x: `wxplot2d(f(x),[x,mínimo,máximo], [y,mínimo,máximo],opciones)`

#### Gráficas con draw2d

- **Explícitas:** y=f(x), se despeja la y en función de x (ej. no funcionan las funciones de circunferencia)
- **Implícitas:** a través de una ecuación, paramétrica. (ej. x²+y² = 1)
- **De puntos:** podemos hacerlo de dos formas:
  - lista de puntos: points([[x,y],[x,y]])
  - lista de abcisas y ordenadas: points(\[x,x,x],[y,y,y])

Sintaxis:

```
wxdraw2d(explicit/implicit(f(x), variable, minimo, maximo))
```

algunas opciones: 

- color=[color]
- line_width=[número]
- proportional_axes=xy
- xaxis=true/false
- yaxis=true/false
- yrange=[min,max]
- xrange=[min,max]



Asíntotas horizontales en forma explicit(n, x, min, max)

Asíntotas verticales en forma  implicit(x=0)



## SESIÓN 3 - 13/10 - Programación

#### Notas:

- Ojo en las funciones a trozos: maxima pinta (incorrectamente) la discontinuidad de salto
- Función random:
  - Enteros naturales - random(5)
  - Con decimales - random(5.0)
- Salida por pantalla:
  - Print()
  - Disp()
  - Display()

#### Variables

Asignación con `:`

```
a:8

[a,b]:[1,2]

c:[2,3,4]

c[1] --> 2
c[2] --> 3
c[3] --> 4
```

Eliminar valores: `remvalue(x,y,z/all)`

Acabar con todo: `kill(all)`

#### Listas

Agrupamos entre corchetes y separamos con comas las entradas. Pueden contener cualquier cosa, de múltiples tipos.

Con makelist podemos generar lista según parámetros:

`makelist(función, variable, inicio variable, fin variable, (opcional) salto en cada iteración)`

Por ejemplo, el inverso de los números del 1 al 100 saltando de 5 en 5: `makelist((1/k),k,1,100,5)`

Para poder usar esa lista, obviamente hay que guardarla en una variable: `var:makelist(...)`

#### Bloques

Para ejecutar una secuencia de instrucciones podemos:

- Líneas acabadas en ; -> una salida para cada línea
- Paréntesis con lista de instrucciones separadas por , -> una única salida, la última
- Secuencia de instrucciones en una línea separada por ;

Pero mejor es usar bloques para poder hacer uso de funciones y variables locales: `block(y todo dentro)`

Dentro de un bloque, definimos funciones con `local(f)`. Si no lo hacemos, la función no se limita al bloque

#### Condicionales

`if cond then expr1 else expr2`

Ejemplo: `maximo(x,y):=if x>=y then x else y`

Así definimos las funciones a trozos (cuidado con la discontinuidad de salto)

#### Bucles

- Bucle for: `for contador:valor_inicial thru valor_final [(opcional) step salto_iteración] do expresión`
- Bucle while: `while condition do expr`

# SESIÓN 4 - 27/10 - Ecuaciones

### Notas

- Calcular los puntos de corte => resolver el sistema de ecuaciones

### Ecuaciones 

Se definen con una igualdad entre dos expresiones algebráicas. Se pueden asignar a variables. 

```
x+2=2x-1;
ecuacion: x+2=2x-1
```

Podemos referenciar el lado derecho y lado izquierdo de la asignación con `rhs(eq), lhs(eq)` respectivamente (right hand side, left hand side).

### Resolución

- `solve([eq], [var])`: resuelve ecuaciones polinómicas **de grados 1 a 4** de forma exacta a través de radicales.

  - Si intentamos con grados mayores nos devolverá números imaginarios

  - A veces nos devolverá números complejos y cuentas muy extensas con radicales incluso si es de grado 1 a 4 - en este caso deberíamos usar `float(%)` para que nos dé el resultado anterior de forma legible y descartaremos las soluciones imaginarias.

    - En un polinomio de grado impar, SIEMPRE debe haber al menos una solución real. Las soluciones imaginarias siempre vienen DE DOS EN DOS.

  - Otras veces tendremos que "ayudar" a maxima. Por ejemplo:

    ```
     -->	ec: x=sqrt(x+1);
     -->	solve(ec);
     -->	solve(ec^2);
    ```

    En este ejemplo en particular pueden aparecer soluciones ficticias, debemos comprobarlas siempre.

### Referenciar soluciones

Para referenciar las soluciones: cuando resolvemos una ecuación, Maxima nos da una lista de asignaciones de la variable. Para reutilizar las soluciones haremos así:

```
 -->	s:solve(x^2-3*x+1=0,x);
 -->	sol:map(rhs,s);
```

De esta forma nos quedamos con una lista de las soluciones, no de asignaciones.

### Resolver "aproximadamente"



### Resolver por Bolzano

Find_root se basa en teorema de Bolzano así que tenemos que verificar que los puntos que damos tienen f(x) con signo distinto

> Polinómicas "fáciles" hasta grado 4... solve
>
> Polinómicas mayores de grado 4, trigonométricas (cogidas con pinzas, no recomendable)... to_poly_solve
>
> Logaritmos, raíces, senos, cosenos, etc... find_root, HACER SIEMPRE LA GRÁFICA ANTES

