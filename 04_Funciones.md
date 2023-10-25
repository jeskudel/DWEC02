# DWEC UT02: Estructura de objetos predefinidos y objetos definidos por el usuario.

## Funciones

En programación, cuando nuestro código se va haciendo cada vez más grande, necesitaremos buscar una forma de organizarlo y prepararnos para reutilizarlo y no repetir innecesariamente las mismas tareas. Para ello, un primer recurso muy útil son las funciones.

Las `funciones` son uno de los bloques de construcción fundamentales en JavaScript. Una función en JavaScript es similar a un procedimiento — un conjunto de instrucciones que realiza una tarea o calcula un valor, pero para que un procedimiento califique como función, debe tomar alguna entrada y devolver una salida donde hay alguna relación obvia entre la entrada y la salida. Para usar una función, debes definirla en algún lugar del ámbito desde el que deseas llamarla.

Las funciones nos permiten agrupar líneas de código en tareas con un nombre, para que, posteriormente, podamos hacer referencia a ese nombre para realizar todo lo que se agrupe en dicha tarea. Para usar funciones hay que hacer 2 cosas:

* Declarar la función: Preparar la función, darle un nombre y decirle las tareas que realizará.
* Ejecutar la función: «Llamar» a la función para que realice las tareas de su contenido.

### Declaración de funciones

Una definición de función (también denominada declaración de función o expresión de función) consta de la palabra clave `function`, seguida de:

* El nombre de la función.
* Una lista de parámetros de la función, entre paréntesis y separados por comas.
* Las declaraciones de JavaScript que definen la función, encerradas entre llaves, `{ ... }`.

```js
function square(number) {
  return number * number;
}
```

La función `square` toma un parámetro, llamado `number`. La función consta de una declaración que dice devuelva el parámetro de la función (es decir, `number`) multiplicado por sí mismo. La instrucción `return` especifica el valor devuelto por la función.

La función anterior se le conoce como **función por declaración** y es que le estamos dando un nombre concreto (square) a la hora de definirla.

Las funciónes también pueden ser anónimas o **función por expresión**. Estas funciones no tienen por qué tener un nombre. Por ejemplo, la función `square` se podría haber definido como:

```js
const square = function (number) {
  return number * number;
};
let x = square(4);              // 'x' se asigna el valor 16
```

Las expresiones `function` son más convenientes cuando se pasa una función como argumento a otra función. El siguiente ejemplo muestra una función `map` que debería recibir una función como primer argumento y un array como segundo argumento.

```js
function map(f, a) {
  let result = [];          // Crea un nuevo arreglo
  let i;                    // Declara una variable
  for (i = 0; i != a.length; i++) result[i] = f(a[i]);
  return result;
}
const f = function (x) {
  return x * x * x;
};
let numbers = [0, 1, 2, 5, 10];
let cube = map(f, numbers);
console.log(cube);          // La función devuelve: [0, 1, 8, 125, 1000].
```

> Además de definir funciones como se describe aquí, también puedes usar el constructor [`Function`](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Function/Function) para crear funciones a partir de una cadena en tiempo de ejecución, muy al estilo de [`eval()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/eval).

### Funciones flecha (arrow functions)

Las funciones flecha permiten definir de manera compacta una función convencional. Si la función tiene solamente una sentencia que devuelve un valor, el uso de funciones flecha nos permite eliminar las llaves y la palabra `return`. Incluso utilizando parámetros también podemos ver mucho más reducido el código. Se introdujeron en ES2015.

La sintaxis básica de las funciones flecha o arrow functions sin parámetros podría ser culaquiera de las siguientes:

```js
() => expression

param => expression

(param) => expression

(param1, paramN) => expression

() => {
  statements
}

param => {
  statements
}

(param1, paramN) => {
  statements
}
```
Entre las ventajas que nos ofrecen las funciones flecha, están:

* Si el cuerpo de la función sólo tiene una línea, podemos omitir las llaves `{}`.
* Además, en ese caso, automáticamente se hace un `return` de esa única línea, por lo que podemos omitir también el `return`.
* En el caso de que la función no tenga parámetros, se indica como en el ejemplo anterior: `() =>`.

Así puede cambiar una función tradicional en comparación con las arrow functions.

```js
// Función anonima tradicional
(function (a) {
  return a + 100;
});

// 1. Quitamos la palabra "function" colocamos la flecha entre los parametros y el cuerpo
(a) => {
  return a + 100;
};

// 2. Quitamos las llaves que enmarcan el cuerpo y la palabra 'return'
(a) => a + 100;

// 3. Quitamos los parentesis del parametro (ya que solo hay uno)
a => a + 100;
```
### Parametros 

A las funciones se les pueden pasar **parámetros**, que no son más que variables que les pasamos desde fuera hacia dentro de la función. Además, también podemos hacer que la función realice sus tareas y nos devuelva un resultado hacia el exterior de la función.

```js
function tablaMultiplicarUno(hasta) {
  for (let i = 0; i <= hasta; i++) {
    console.log("1 x", i, "=", 1 * i);
  }
}

tablaMultiplicarUno(5);         // Tabla del 1, queremos que llegue hasta el 5
```

Una función de Javascript puede tener muchos más parámetros. Vamos a crear otro ejemplo, mucho más útil donde convertimos nuestra función en algo más práctico y útil:

```js
function tablaMultiplicar(tabla, hasta) {
  for (let i = 0; i <= hasta; i++) {
    console.log(tabla, "x", i, "=", tabla * i);
  }
}
tablaMultiplicar(1, 10); // Tabla del 1
tablaMultiplicar(5, 10); // Tabla del 5
```

A partir de ES2015 se introdujo el concepto de parametros por defecto que no es otra cosa mas que asignar un valor por defecto al parametro en caso de que no se haya definido previamente.

En nuestro ejemplo anterior, nos podría interesar que la tabla de multiplicar llegue siempre hasta el 10, ya que es el comportamiento por defecto. Si queremos que llegue hasta otro número, lo indicamos explicitamente, pero si lo omitimos, queremos que llegue hasta 10. Esto se haría de la siguiente forma:

```js
function tablaMultiplicar(tabla, hasta = 10) {
  for (let i = 0; i <= hasta; i++) {
    console.log(tabla, "x", i, "=", tabla * i);
  }
}

tablaMultiplicar(2);            // Tabla del 2, del 0 al número 10
tablaMultiplicar(2, 15);        // Tabla del 2, del 0 al número 15
```

### Llamada a funciones

Definir una función no la "ejecuta". Definirla simplemente nombra la función y especifica qué hacer cuando se llama a la función.

Llamar a la función en realidad lleva a cabo las acciones especificadas con los parámetros indicados. Por ejemplo, si defines la función `square`, podrías llamarla de la siguiente manera:

```js
square(5);          // llamamos pasando el parametro de tipo number '5'
```

Los argumentos de una función no se limitan a cadenas y números. Puedes pasar objetos completos a una función.

```js
function factorial(n) {
  if (n === 0 || n === 1) return 1;
  else return n * factorial(n - 1);
}

let a, b, c, d, e;
a = factorial(1);       // a se asigna el valor 1
b = factorial(2);       // b se asigna el valor 2
c = factorial(3);       // c se asigna el valor 6
d = factorial(4);       // d se asigna el valor 24
e = factorial(5);       // e se asigna el valor 120
```

Cuando utilizamos la palabra `return` devolvera el valor especificado (pudiendo ser un valor primitivo o algo mas complejo). En caso de no devolver nada, se puede utilizar `return` para parar la ejecución de la función en un momento dado.

```js
function showMovie(age) {
  if ( !checkAge(age) ) {
    return;
  }
  alert( "Showing you the movie" ); 
  // ...
}
```

> #### Buenas prácticas nombrando funciones
> Las funciones son acciones, por lo que es recomendable nombrarlas como verbos. Debe ser conciso y breve, y describir lo que hace la función.
> Es una práctica habitual nombrar las funciones con un prefijo describiendo la acción y después la explicación. Por ejemplo:
> * "get…" – return a value,
> * "calc…" – calculate something,
> * "create…" – create something,
> * "check…" – check something and return a boolean, etc.
> ```js
> showMessage(..)     // muestra algun tipo de mensaje
> getAge(..)          // devuleve la edad (de alguna manera)
> calcSum(..)         // calcula la suma de algo
> createForm(..)      // crea un formulario (y normalmente lo devuelve)
> checkPermission(..) // comprueba alguna condición (normalmente devuelve 'true/false')
> ``` 


### Ambito (Scope) de las variables

No se puede acceder a las variables definidas dentro de una función desde cualquier lugar fuera de la función, porque la variable se define solo en el ámbito de la función. Sin embargo, una función puede acceder a todas las variables y funciones definidas dentro del ámbito en el que está definida.

En otras palabras, una función definida en el ámbito global puede acceder a todas las variables definidas en el ámbito global. Una función definida dentro de otra función también puede acceder a todas las variables definidas en su función principal y a cualquier otra variable a la que tenga acceso la función principal.

```js
// Las siguientes variables se definen en el ámbito global
let num1 = 20,
    num2 = 3,
    name = "Jordan";

// Esta función está definida en el ámbito global
function multiply() {
  return num1 * num2;
}
multiply();                 // Devuelve 60

// Un ejemplo de función anidada
function getScore() {
    let num1 = 2,
        num2 = 3;
    function add() {
        return name + " anotó " + (num1 + num2);
    }
    return add();
}
getScore(); // Devuelve "Chamahk anotó 5"
```

Esto se conoce tambien como 'cierres' (clousures). Los cierres son una de las características más poderosas de JavaScript. JavaScript permite el anidamiento de funciones y otorga a la función interna acceso completo a todas las variables y funciones definidas dentro de la función externa (y todas las demás variables y funciones a las que la función externa tiene acceso).

Sin embargo, la función externa no tiene acceso a las variables y funciones definidas dentro de la función interna. Esto proporciona una especie de encapsulación para las variables de la función interna.

Además, dado que la función interna tiene acceso a el ámbito de la función externa, las variables y funciones definidas en la función externa vivirán más que la duración de la ejecución de la función externa, si la función interna logra sobrevivir más allá de la vida de la función externa. Se crea un cierre cuando la función interna de alguna manera se pone a disposición de cualquier ámbito fuera de la función externa.

```js
let pet = function (name) { 
    // La función externa define una variable llamada "name"
    const getName = function () {
        return name;        // La función interna tiene acceso a la variable "name" de la función externa
    };
    return getName;         // Devuelve la función interna, exponiéndola así a ámbitos externos
};
myPet = pet("Vivie");

myPet(); // Devuelve "Vivie"
```

> #### *Para saber mas ...*
> Las 'arrow functions' no son solo una manera más sencilla y compacta de declarar funciones. También tienen implicaciones al respecto de los ambitos de las variables utilizadas. [Articulo.](https://somospnt.com/blog/207-funciones-flecha-vs-funciones-regulares)

### Funciones `Callback`

Ahora que conocemos las funciones anónimas, podremos comprender más fácilmente como utilizar `callbacks` (también llamadas funciones callback o retrollamadas). A grandes rasgos, un `callback` (llamada hacia atrás) es pasar una función 'B' por parámetro a una función A, de modo que la función 'A' puede ejecutar esa función 'B' de forma genérica desde su código, y nosotros podemos definirlas desde fuera de dicha función:

```js
const fB = function () {
    console.log("Función B ejecutada.");
};
const fA = function (callback) {            // En el ambito de fA se renombra la función a 'callback'
    callback();                             // Se llama a esta función
};
fA(fB);
```

Esto nos podría permitir crear varias funciones para utilizar a modo de callback y reutilizarlas posteriormente con diferentes propósitos. De hecho, los callbacks muchas veces son la primera estrategia que se suele utilizar en Javascript para trabajar la asincronía, uno de los temas que veremos más adelante:

```js
function pregunta(texto, afirmativo, negativo) {
    if (confirm(texto)) {
        afirmativo()
    } 
    else {
        negativo();
    }
    // utilizando operador ternario
    // confirm(texto) ? afirmativo() : negativo()
}

function showOk() {
  alert( "Estas de acuerdo entonces" );
}

function showCancel() {
  alert( "Has cancelado la ejecución" );
}

// modo_uso: las funciones 'showOk', 'showCancel' se pasan como parametros
pregunta("Estas de acuerdo?", showOk, showCancel);
```