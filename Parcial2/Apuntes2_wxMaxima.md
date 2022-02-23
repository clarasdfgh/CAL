# CAL 2122 - Apuntes parcial 2 wxMaxima

## SESIÓN 5 - 03/11 - Error absoluto y relativo, método de bisección

#### Notas:

- TRABAJAR SIEMPRE EN NUMÉRICO (`numer:true`) EN LAS SIGUIENTES SESIONES

#### Error absoluto y relativo:

- Error absoluto: diferencia entre valor exacto y valor aproximado
  - |valor exacto - valor aproximado|
- Error relativo: representación en tanto por ciento del valor absoluto
  - |error absoluto| / |valor exacto| * 100

##### Fuentes de error

- Redondeo:
- Truncamiento:

#### Métodos cerrados y abiertos

Buscamos una raíz de una función f en un intervalo [a,b].

- Métodos cerrados: la función cambia de signo en los extremos y vamos reduciendo el  intervalo, manteniendo el cambio de signo, hasta encontrar la solución.
- Métodos abiertos: empezando con uno o varios valores iniciales, construimos una sucesión de aproximaciones a la raíz.

En los métodos cerrados tenemos garantizado que encontramos la solución.

## SESIÓN 6 - 17/11 - Método de Newton-Raphson y de la secante

### Método de Newton-Raphson

- Función continua en forma de bolzano
- Consiste en tomar un punto de inicio (x0,f(x0)) y trazar su recta tangente
  - Que el punto no sea crítico!!
- Buscar el corte de la recta con el eje x: x1
- Buscamos la recta tangente en x1
  - Cada vez el punto de corte con el eje x de la recta tangente se acerca más al punto de corte de la función con el eje x
- Repetir el proceso hasta que se estabilicen los decimales: tomar punto xn, obtener recta tangente rn, obtener punto de corte con eje x, el punto de corte es la nueva xn

##### Precauciones:

- Evitar puntos criticos (tanto como x0 como "en medio")
- Que cumpla el tma de Newton Raphson:
  - Que sea derivable dos veces y continua
  - Que cambie de signo el intervalo (Bolzano)
  - f'(x) y f''(x) tienen signo constante en [a,b]. Es decir:
    - f(x) es estrictamente creciente o decreciente (f'(x)>0 o f'(x)<0)
    - f(x) es estrictamente cóncava o convexa (f''<0 o f''(x)>0)
    - Comprobar con la gráfica **siempre** (tanto para este método como para los otros)

### Método de la secante

- Función continua en forma de Bolzano
- Tomamos dos puntos: x0, x1. Trazamos la recta que los atraviesa los dos.
  - Secante: atraviesa la gráfica de la función en dos puntos
- Tomamos el punto de intersección de la secante con el eje x (f(x2)=0)
- Repetimos el proceso con los puntos x2, x1. El punto de intersección de la recta secante con el eje x se irá acercando (oscilando) al punto de corte de la función original con el eje  x

##### Precauciones

- Que los puntos iniciales x1, x2 no sean muy cercanos (en pocas iteraciones acabaríamos dividiendo por 0)

## Interpolación

ejercicio 3.1 obtener los puntos equitativamente distribuidos:

como todos los puntos serán (x,f(x))

Si queremos n puntos equitativamente distribuidos entre A,B: [distancia entre AB/n-1]

Entonces -1+k*1/10 para 21 puntos equitativamente distribuidos entre -1, 1

```
f(x):=1/(1+x^2);
makelist([-1+k*1/10, f(-1+k*1/10)],k,0,20);
```

