1 - fib.c

> El Fibonacci iterativo tarda menos que el recursivo debido a la gran cantidad de registros de activación que crea: para calcular cada número de la secuencia, calcula el anterior inmediato recursivamente y el anterior al anterior en otro llamado recursivo, y los suma. En cambio, el enfoque iterativo, crea solo un registro de activación, evitando desperdiciar tiempo alocando y desalocando registros de activación.
> Ejemplo:  
Calculando Fibonacci iterativo para n = 20...
 Resultado = 6765
 Tiempo en segundos 0.0000001192 
Calculando Fibonacci recursivo para n = 20...
 Resultado = 6765
 Tiempo en segundos 0.0000451088 


2 - funcion.c

> La primera forma es mas rapida, ya que calcula una sola vez la la parte de la funcion que es estatica, es decir que en la sumatoria siempre da lo mismo ( 2 * (( (x*x*x) + (3*x*x) + (3*x) + 2 ) / ( (x*x) + 1))), y lo guarda en una variable llamada fx, y lo que si varia que es la variable i, se le resta dentro de un for.
> En cambio la segunda forma el for siempre resuelve toda la ecuacion de la sumatoria.

3 - instrucciones.c

> Tras correr el programa varias veces, se puede concluir que la operación más
rápidas son la suma la resta y la multiplicación (todas tardan lo mismo),
y la división tarda el doble que las anteriores.
Esto se debe a que las tres primeras operaciones pueden realizarse directamente
en hardware en un ciclo de instrucción (gracias al uso de binario en formato
ca2), mientras que la división requiere del uso repetido de dichas
instrucciones en varios pasos.
Con potencias de 2, el tiempo decrementa en todos los casos.

4 - instrucciones2.c

>  Como se explico en el punto anterior, en instrucciones2.c se busca el mismo resultado ya que 1000 / 5 y 1000 * 0.2 es 200, pero se llega de una forma mas rapida usando la multiplicacion. Mientras no sean potencias de 2, la división será mas lenta de la multiplicación.

5 - matrices.c

> https://www.rapidtables.com/code/linux/gcc/gcc-o.html

6 - quadratic1.c

> a - Como el nombre lo indica, el tipo de dato double tiene una precisión doble que el tipo de dato float (2x). En general, un double tiene 15 dígitos decimales de precisión, mientras que el tipo de dato float tiene solamente 7.
Debido a la menor precisión de un tipo de dato float, puede existir pérdida de información más rápidamente.
Es por esto que la solucion double se acerca mas al resultado indicado en la practica en decimal.
Soluciones Float: 2.00000       2.00000
Soluciones Double: 2.00032      1.99968

> b - Times 100 
> Tiempo requerido solucion Double: 29.235821 Tiempo requerido solucion Float: 33.772318
> Si modificamos la constante TIMES el resultado siempre es el mismo, double tarda menos que float.
> el tipo de dato double, utiliza una base 2 

> c - El cambio esta en que al definir las variables ahora para los numeros flotantes se pone 1.0f en vez de 1.0, esto hace que el float tarde muchisimo menos que en el ejercicio B. Ya que el numero 1.0 es una representacion de double que utiliza 64 bits y al agregarle la f, utilizamos la representacion de 32bits
> StackOverflow: The number 3.0 is the literal representation of a double value (it's equivalent to 3.0d), whereas 3.0f is a float value. The different precisions explain why you're getting different results - a double is stored using 64-bits, a float uses 32-bits.

7 - iterstruc1 / interstruc2
> El cambio de codigo es de un for y un while.
> El for es mas rapido porque tiene ya el indice de antes y sabe cuantas iteracciones tiene que dar, en cambio el while tiene que analizar la condicion. Aunque el tiempo no tiene un cambio muy significativo (?)
./iterstruc1.out 1000
Incializando matrices...
Calculando For...
 Tiempo For en segundos 3.344360 

>./iterstruc2.out 1000
Incializando matrices...
Calculando While...
Tiempo While en segundos 3.354049 


8 - matrices.c
>Hay dos cuestiones simples a optimizar en cuanto al código. La primera es respecto del acceso a los valores en las matrices. En el codigo se accede a los datos de la matriz por fila. Cuando se cambia esta configuracion establecida mediante macros, accediendo por columnas, el tiempo de ejecucion es menor. Luego, se puede optimizar el uso del stack. Por cada llamado a una función se carga las referencias necesarias en el stack, así como los parametros enviados. Esto podría optimizarse minimamente mediante el uso de funciones inline, pero en este caso quedaría a elección del compilador evaluar si la función pasa a ser efectivamente inline o no. Al mismo tiempo esto se podría forzar mediante extensiones del compilador, pero no va al caso. La solucion mas simple es evitar el llamado a estas funciones cambiando el codigo donde estas rutinas son llamadas por el codigo correspondiente sin el llamado.

> Modificado en matricesM.c


10 - triangular.c
>"triangular.c" tarda 52 segundos para una matriz cuadrada de orden 2048.
"triangularM.c" tarda 32 segundos para una matriz de igual orden.
El código optimizado realiza la multiplicación de "atrás hacia adelante".
Recorre primero BT, mientras no encuentre un 0 realizar la multiplicación con A y sumar a un total. Esto es válido porque BT es una matriz triangular inferior; si fuera triangular superior: recorrer normal y parar cuando se encuentre un 0.
Además, la disposición del acceso a las matrices permite un mejor uso de la localidad de las referencias en caché, ahorrando accesos innecesarios.