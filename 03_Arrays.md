# DWEC UT02: Estructura de objetos predefinidos y objetos definidos por el usuario.

## Arrays

Los objetos le permiten almacenar colecciones de valores con una `clave`. Pero muy a menudo encontramos que necesitamos una colección ordenada, donde tenemos un primer, un segundo, un tercer elemento, etc. Por ejemplo, lo necesitamos para almacenar una lista de algo: usuarios, productos, elementos HTML, etc.

Un `array` (también conocido con `vector` o `arreglo`) es una colección ordenada de elementos (valores). Cada elemento tiene una posición denominada índice. El primer elemento tienen índice `0`. Los elementos del array pueden ser de cualquier tipo (datos primitivos, objetos, arrays...), y dentro del array puede haber elementos de diferentes tipos. Se accede a los elementos por su índice mediante corchetes `[]`.

| Método  | Descripción |
|----------|----------|
| `new Array(size)` | Crea un array vacío de tamaño `size`. Sus valores no están definidos, pero son `undefined` |
| `new Array(e1, e2...)` | Crea un array con los elementos indicados |
| `[e1, e2...]` | Simplemente, los elementos dentro de corchetes: `[]`. **Notación preferida** |

```js
let a= new Array(),                             // Array vacío
    b= [],                                      // Array vacio
    c= new Array(20),                           // Array vacío de 20 elementos
    d= [20],                                    // Array de un elemento
    e= new Array(10, "hola", 30, "Mundo!"),     // Array de 4 elementos
    f= [10, 20, 30, 40];                        // Array de 4 elementos
```

### Accediendo a elementos del `Array`

Al igual que los `string`, saber el número elementos que tiene un array es muy sencillo. Sólo hay que acceder a la propiedad `.length`, que nos devolverá el número de elementos existentes en un array:

| Método  | Descripción |
|----------|----------|
| `.length` | Propiedad que devuelve el número de elementos del array |
| `[pos]` | Operador que devuelve (o modifica) el elemento número `pos` del array |
| `.at(pos)` | Método que devuelve el elemento en la posición `pos`. Números negativos en orden inverso |

```js
let frutas = ["Manzana", "Naranja", "Piña"];

console.log(frutas.length);     // 3
console.log(frutas[0]);         // Manzana
console.log(frutas[1]);         // Naranja

frutas[2] = "Nectarina";
console.log(frutas);            // ["Manzana", "Naranja", "Nectarina"]

frutas[3] = "Mango"             // Se añade un elemeto mas en la posición especificada
console.log(frutas.length);     // 4
```

El operador `[]` también nos permite modificar el elemento de la posición especificada, además de poder añadir elementos al `array`.

Con el método `at()`, al igual que con los `string`, podemos utilizar indices negativos para indicar elementos desde el final del `array`. De otra manera tendríamos que calcular nosotros a mano cuantos indices existen en el array y restarle 1 (recordad que se empieza por el indice `0`).

```js
let frutas = ["Manzana", "Naranja", "Piña"];

console.log(frutas[frutas.length-1]);     // Piña
console.log(fruits.at(-1));               // Piña
```

### Añadir y eleminar elementso de un `Array`

Existen varias formas de añadir elementos a un `array` ya existente. Ten en cuenta que en todos estos casos estamos mutando (variando los elementos del array ya existente). Veamos los métodos que podemos usar para ello:

| Método  | Descripción |
|----------|----------|
| `.push(e1, e2, e3...)` | Añade uno o varios elementos al final del array. Devuelve el tamaño del array |
| `.pop()` | Elimina el último elemento del array. Devuelve dicho elemento |
| ` .unshift(e1, e2, e3...)` | Añade uno o varios elementos al inicio del array. Devuelve el tamaño del array |
| `.shift()` | Elimina el primer elemento del array. Devuelve dicho elemento |

```js
let frutas = ["Manzana", "Naranja", "Piña"];

frutas.pop();                       // elimina "Piña" del array y devuelve su valor
frutas.push("Pera");                // añade "Pera" en la última posición del array
console.log(frutas);                // [ "Manzana", "Naranja", "Pera" ]

let primeraFruta = frutas.shift();  // asigna "Manzana" a la variable primeraFruta y lo elimina del array
console.log(frutas);                // [ "Naranja", "Pera" ]
console.log(primeraFruta);          // "Manzana"
frutas.unshift("Arandanos");        
console.log(frutas);                // [ "Arandanos", "Naranja", "Pera" ]
```
### Iterar sobre elementos de un `Array`

Una de las formas de iterar mas tradicional por los elementos de un `array` es utilizar una estructura iterativa (`for`, `while`, ...)

```js
let frutas = ["Manzana", "Naranja", "Piña"];
for (let i = 0; i < frutas.length; i++) {
    console.log(frutas[i]);
}
...
let contador = 0;
while (contador < frutas.length){
    console.log(frutas[contador]);
    contador ++;
}
```

Pero han aparecido metodos mas sencillos de escribir y utilizar que, además, facilita la legibilidad de código por usuarios y desarrolladores. Estos métodos son `for...in` y `for...of`.

Utilizar `for...in` es muy parecido a utilizar un bucle normal de los anteriores ya que no se accede directamente al elemento, sino que se accede al indice del elemento en cuestión.

```js
let frutas = ["Manzana", "Naranja", "Piña"];
for (let i in frutas) {
    console.log(frutas[i]);
}
```

Por el contrario, utilizando `for...of` accedemos directamente al elemento y no al indice del elemento.

```js
let frutas = ["Manzana", "Naranja", "Piña"];
for (let fruta of frutas) {
    console.log(fruta);
}
```
En realidad el bucle `for..in` itera sobre todas las propiedades, no sólo las numéricas.

En el navegador y en otros entornos existen los llamados objetos “array-like”, que parecen a los arrays. Es decir, tienen propiedades de `length` e `indices`, pero también pueden tener otras propiedades y métodos no numéricos, que normalmente no necesitamos. Sin embargo, el bucle `for..in` los enumerará. Entonces, si necesitamos trabajar con objetos tipo matriz, entonces estas propiedades "adicionales" pueden convertirse en un problema.

```js
let frutas = ["Manzana", "Naranja", "Piña"];
frutas["nuevaPropiedad"] = "Maracuya";
for (let i in frutas) {
    console.log(frutas[i]);     // muestra también el valor de la propiedad "nuevaPropiedad"
}
```

El bucle `for..in` está optimizado para objetos genéricos, no tanto para matrices. Pero aun así debemos ser conscientes de la diferencia al hacer uso de el. Generalmente, no se recomienda usar `for..in` para arrays.

Por último tenemos el método del obejto `array` llamado `.forEach()` que es un poco diferente a los anteriores ya que necesitas que se le pase una función, la cual, se ejecutara por cada elemento que exista en el `array`. Veamos unos ejemplos sencillos:

```js
let frutas = ["Manzana", "Naranja", "Piña"];
frutas.forEach(alert);          // muestra mensaje de alerta por cada fruta

frutas.forEach(function(){      // mismo resultado que lo anterior
    alert()
})
```

Sin embargo, este ejemplo no tiene demasiada utilidad. Al `callback` se le pueden pasar varios parámetros opcionales:

* Si se le pasa un primer parámetro, este será el elemento del array.
* Si se le pasa un segundo parámetro, este será la posición en el array.
* Si se le pasa un tercer parámetro, este será el array en cuestión.

```js
let frutas = ["Manzana", "Naranja", "Piña"];
frutas.forEach(function(elemento, posicion, array){
    console.log(`${elemento} esta en la posición ${posicion + 1} en ${array}`)
})
```
Para entender mejor el funcionamiento puedes empezar a mirar la parte de ["Funciones"](./04_Funciones.md) de los apuntes, para luego volver y entender mejor el funcionamiento. Mas adelante entraremos con los "array functions" en los que se profundizara mas en los `callback` (pasar funciones a métodos).


### Arrays multidimensionales

Los `array` pueden tener elementos de diferente tipo (`string`, `number`, ...) y tambien pueden almacenar otro `array` creando así un `array` dentro de otro `array`. Podemos usarlo para `arrays` multidimensionales, por ejemplo para almacenar matrices:

```js
let matriz = [
  [1, 2, 3],
  [4, 5, 6],
  [7, 8, 9]
];
console.log(matriz[1][1]);      // 5
```

Con los primeros `[]` accedemos a la posición del `array` "principal" y con los seguientes `[]` al elemento con indice `1`de ese `array`.

### Buscando elementos en un `Array`

En muchas ocasiones nos interesará buscar elementos de un `array` para saber si se encuentran dentro de él o saber la posición del elemento en el `array`. Para ello, existen una serie de métodos mediante los cuales podemos realizar estas acciones. Son los siguientes:

| Método  | Descripción |
|----------|----------|
| `.includes(elemento, [pos])` | Comprueba si `elemento` está incluido en el array |
| `.indexOf(elemento, [pos])` | Devuelve la posición de la primera aparición de `elemento`. Devuelve -1 si no existe |
| `.lastIndexOf(elemento, [pos])` | Devuelve la posición de la última aparición de `elemento`. Devuelve -1 si no existe |

```js
let frutas = ["Manzana", "Naranja", "Piña", "Pera", "Manzana"];
frutas.includes("Naranja")                      // devuelve "true"
frutas.includes("Naranja", 2)                   // devuelve "false"
frutas.includes("Mango")                        // devuelve "false"
frutas.indexOf("Pera")                          // devuelve 3
frutas.lastIndexOf("Manzana")                   // devuelve 4
```

### Modificando un `Array`

Hay situaciones en las que tenemos un `array` y queremos crear nuevos subarrays, es decir, un pequeño fragmento del original, o simplemente modificar el `array` original para hacer ciertos cambios, pero de una forma más general y no tener que hacerlo elemento a elemento.

Para ello, existen varios métodos relacionados, entre los que se encuentran los siguientes:

| Método  | Descripción | Mutación array original |
|----------|----------|----------
| `.slice(start, end)` | Devuelve los elementos desde la posición `start` hasta `end` (*excluído*) | **No cambia** |
| `.splice(start, size)` | Devuelve los `size` siguientes elementos desde la posición `start` | **Cambia** | 
| `.toSpliced(start, size)` | Idem a `splice(start, size)`, pero sin mutar el array original. | **No cambia** | 
| `.with(index, item)` | Devuelve una copia del original, con el elemento `index` modificado. | **No cambia** | 
| `.copyWithin(pos, start, end)` | Muta el array, cambiando en `pos` y copiando desde `start` a `end` | **Cambia** | 
| `.fill(element, start, end)` | Cambia los elementos del por element desde start hasta end | **Cambia** | 

```js
let frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.slice(3)             //["Pera", "Mango"]
frutas.slice(0,2)           //["Manzana", "Naranja"]
console.log(frutas)         //["Manzana", "Naranja", "Piña", "Pera", "Mango"]

let nuevasFrutas = frutas.splice(0,2)          // Crea, devuelve y asigna a una variable ["Manzana", "Naranja"]
console.log(frutas)         // ["Piña", "Pera", "Mango"]

frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.toSpliced(0,2)        // Crea y devuelve  ["Manzana", "Naranja"]
console.log(frutas)          // ["Manzana", "Naranja", "Piña", "Pera", "Mango"]
```

El método`copyWithin(pos, start, end)` nos permite alterar el array, de modo que, empezando en la posición `pos`, copiará los elementos que están desde la posición `start` hasta la posición `end`. El parámetro `end` es opcional, de modo que si no se indica, se asume que end es el tamaño del array.

```js
let frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.copyWithin(2, 0, 3)          // ["Manzana", "Naranja", "Manzana", "Naranja", "Piña"]

frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.copyWithin(2, 1)             // ["Manzana", "Naranja", "Naranja", "Piña", "Pera"]    

frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.copyWithin(3, 1, 2)          // ["Manzana", "Naranja", "Piña", "Naranja", "Mango"]
```

El un método `fill()` nos permite rellenar el con los elementos indicados.

```js
let frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];
frutas.fill("Uva", 0, 3)            // ["Uva", "Uva", "Uva", "Pera", "Mango"]

let arr = new Array(5).fill("X")    // ["X", "X", "X", "X", "X"]    
```

El nuevo método `.with()` nos proporciona una forma donde podemos hacer una pequeña modificación en un array, sin que alteremos el original.

```js
let frutas = ["Manzana", "Naranja", "Piña", "Pera", "Mango"];

frutas.with(0, "Golden")
console.log(frutas)             // ["Golden", "Naranja", "Piña", "Pera", "Mango"]

//podemos encadenar varias llamadas a .with()
frutas.with(1, "Valenciana")
      .with(3, "Conferencia")
      .with(4, "Francis")
console.log(frutas)             // ["Golden", "Valenciana", "Piña", "Conferencia", "Francis"]
```

> Puedes encontrar más información acerca de estos métodos y sus parametros opcionales en este enlace de MDN Mozilla ([enlace](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array#m%C3%A9todos_de_instancia)).


### Ordenando un `Array`

| Método  | Descripción | Mutación array original |
|----------|----------|----------
| `.sort()` | Ordena los elementos del array bajo un criterio de ordenación alfabética. | **Cambia** |
| `.toSorted()` | Devuelve una copia del array, con los elementos ordenados. | **No cambia** |
| `.reverse()` | Invierte el orden de elementos del array. | **Cambia** |
| `.toReversed()` | Devuelve una copia del array, con el orden de los elementos invertido. | **No cambia** |

```js
let numeros = [5, 10, 6, 1, 12];
numeros.sort()                      // [1, 10, 12, 5, 6], el array original ha cambiado
numeros.reverse()                   // [6, 5, 12, 10, 1], el array original ha cambiado

numeros = [5, 10, 6, 1, 12];
let nuevoOrdenado = numeros.toSorted()
let nuevoReverse = numeros.toReversed()

console.log(nuevoOrdenado)          // [1, 10, 12, 5, 6]
console.log(nuevoReverse)           // [12, 1, 6, 10, 5]
```

Os habreis fijado en que cuando ordena los elementos del `array` no lo hace bien con los numeros que tenemos como elementos del `array`. Esto es por la función de ordenación por defecto que tiene (que funciona correctamente con letras pero no con números).

> Si quereis saber mas acerca de las funciones de ordenación que se pueden utilizar con los métodos de ordenazión aquí teneéis el enlace de MDN Mozilla ([enlace](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)).

### Metodos complejos (con funciones)

Hasta ahora hemos visto que a los métodos (algunos) les podemos pasar unos parametros (indices, strings, ...) y que realizan una acción concreta (con los parametros facilitados).

Pero hay algunos métodos que funcionan de manera mas compleja, realizando con los elementos del `array` una función concreta definida por el desarrollador. Algunas de ellas ya las hemos visto por encima, como `forEach()` o `sort()`. Veamos un ejemplo de como funciona y se puede representar de diferentes maneras.

```js
let numeros = [1, 2, 3, 4, 5, 6];

// Utilizando funciones por expresión
const f = function(){
    console.log("Elemento del array")
} 
numeros.forEach(f)

// Con funciones anonimas
numeros.forEach(function(){
    console.log("Elemento del array")
})

// Utilizando arrow functions
numeros.forEach(() => console.log("Elemento del array"))
```

#### Comprobaciones en un array

En este ejemplo no estamos pasando ningun parametro a la función y lo único que hace es loguear la misma frase por cada elemento que existe en el `array`.

| Método  | Descripción |
|----------|----------|
| `.every(f)` | Comprueba si todos los elementos del array cumplen la condición de `ƒ` |
| `.some(f)` | Comprueba si al menos un elemento del array cumple la condición de `ƒ` |

El método `.every()` permite comprobar si todos y cada uno de los elementos de un array cumplen la condición que se especifique en la callback:

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"]

nombres.every(function(nombre){
    return nombre.length > 3 ? true : false
})
```

De esta manera comprobamos si todos los nombres del array tienen mas de 3 letras. Si hay un solo elemento que no las tenga, devolvera `false`.

De la misma forma que el método anterior sirve para comprobar si todos los elementos del array cumplen una determinada condición, con `.some()` podemos comprobar si al menos uno de los elementos del array, cumplen dicha condición definida por el callback.

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"]

nombres.some(function(nombre){
    return nombre.length < 4 ? true : false
})
```

Como os habreis dado cuenta, estos dos métodos devuelven un valor bolleano, `true` o `false`.

#### Transformando un array

| Método  | Descripción |
|----------|----------|
| `.map(f)` | Construye un array con lo que devuelve `ƒ` por cada elemento del array |
| `.filter(f)` | Filtra un array y se queda sólo con los elementos que cumplen la condición de `ƒ` |

El método `map()` es un método muy potente y útil para trabajar con arrays, puesto que su objetivo es devolver un nuevo array donde cada uno de sus elementos será lo que devuelva la función `callback` por cada uno de los elementos del array original:

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"]
let letras = nombres.map(name => name.length)      // [4, 4, 6, 3, 5, 4]
```

El método `filter()` nos permite filtrar los elementos de un array y devolver un nuevo array con sólo los elementos que queramos. Para ello, utilizaremos la función `callback` para establecer una condición que devuelve `true` sólo en los elementos que nos interesen:

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"]
let filtrado = nombres.filter(function(nombre){
    if (nombre.startsWith("J")){
        return true
    } else {
        return false
    }
})
```

Hay que tener en cuenta que si `.filter()` no divuevel ningún elemento que cumpla la condición, se devolvera un `array` vacio.

#### Busquedas en un array

| Método  | Descripción |
|----------|----------|
| `.find(f)` | Devuelve el elemento que cumple la condición de `ƒ` |
| `.findIndex(f)` | Devuelve la posición del elemento que cumple la condición de `ƒ` |

Disponemos de 2 métodos interesantes para realizar busquedas , son `find()` y `findIndex()`. Ambos se utilizan para buscar elementos de un array mediante una condición, la diferencia es que el primero devuelve el elemento mientras que el segundo devuelve su posición en el array original:

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"]
nombres.find( nombre => nombre.length == 5)

nombres.findIndex(function(nombre){
    return nombre.length == 5
})
```

#### Metodos acumuladores 

| Método  | Descripción |
|----------|----------|
| `.reduce(f)` | Ejecuta `ƒ` con cada elemento (de izq a der), acumulando el resultado |
| `.reduceRight(f)` | Idem al anterior, pero en orden de derecha a izquierda |

El método `.reduce()` se encarga de recorrer todos los elementos del array, e ir acumulando sus valores (o alguna operación diferente) y sumarlo todo, para devolver su resultado final.

Cuando necesitamos iterar sobre una array, podemos usar `forEach`, `for` o `for...of`. Cuando necesitamos iterar y devolver los datos de cada elemento, podemos usar `map`.

En este  método, encontraremos una primera diferencia en su función `callback`, puesto que en lugar de tener los clásicos parámetros opcionales `(element, index, array)` que hemos utilizado hasta ahora, tiene `(accumulator, item, index, array)`, que funciona de forma muy similar, pero adaptado a este tipo de acumuladores.

```js
let valor = arr.reduce(function(accumulator, item, index, array){
    ....
}, [initialValue]);
```

De esta manera vemos que los parametros que pasaremos (en orden) irán tomando estos valores:

* `accumulator`: es el resultado de la ejecución previa (acumulador). la primera vez tendra el valor de `initialValue` (si se especifica).
* `item`: el elemento actual del array.
* `index`: la posición del elemento del array.
* `array`: el propio array

```js
let numeros = [1, 2, 3, 4, 5];
let resul = numeros.reduce((acumulador, item) => acumulador + item, 0);
console.log(resul)          // 15
```

En este caso la función que se pasa a `.reduce()` solo consta de 2 parametros (habitualmente es suficiente). Veamos que pasa más en detalle:

1. En la primera ejecución, `acumulador` tiene el valor de 0 (es el último parametro de la función).
2. El valor de `item` es de 1.
3. Se ejecuta la función y el resultado se va acumulando en `acumulator`.
4. En la siguiente vuelta `acumulator` tiene el valor de 1 e `item` tiene el valor de 2. Se ejecuta la función y se almacena el valro en `acumulator`
5. ...
6. ...
7. ...
8. Al finalizar las iteraciones por los elementos se guarda el valor en la variable `resul` y se muestra por consola.

La función `.reduceRight()`, como hemos comentado hace los mismo pero en orden inverso, desde la última posición del array hacia la izquierda.


```js
let numeros = [20, 2, 3, 5];
let resulReduce = numeros.reduce((acumulador, item) => acumulador - item);
console.log(resulReduce)                 // 10

let resulReduceRight = numeros.reduceRight((acumulador, item) => acumulador - item);
console.log(resulReduceRight)            // -20
```

En caso de no asignar un valor inicial al parametro `initialValue` el primer valor que tendra el parametro `accumulator` será el primer elemento del array. Sería como si nos saltaramos la primera vuelta o la sumaramos con 0 (o nada).

### Creación alternativa de Arrays

Aunque hemos visto las formas principales de crear un `array` en Javascript, existen otras que permiten generar un `array` partiendo de otras (y muy variadas) estructuras de datos.

#### Concatenando varios `arrays`

Al igual que en los `string`, en los `array` tenemos el método `.concat()`, que nos permite unir los elementos pasados por parámetro en un array a la estructura que estamos manejando. Se podría pensar que los métodos `.push()` y `concat()` funcionan de la misma forma, pero no es exactamente así. Veamos un ejemplo:

```js
let elementos = [1, 2, 3];

elementos.push(4, 5);     // Devuelve 6. Ahora elements = [1, 2, 3, 4, 5]
elementos.push([6, 7]);   // Devuelve 7. Ahora elements = [1, 2, 3, 4, 5, [6, 7]]
```
Pero si utilizamos el método `.concat()` vemos que se comporta de forma diferente:

```js
let elementos = [1, 2, 3];

elementos.push(4, 5);           // Devuelve 6. Ahora elements = [1, 2, 3, 4, 5]
elementos.concat([6, 7]);       // Devuelve 7. Ahora elements = [1, 2, 3, 4, 5, 6, 7]

// diferente manera de concatenar los 2 arrays
let nuevoElementos = Array.prototype.concat(elementos, [8, 9])
console.log(nuevosElementos)    // [1, 2, 3, 4, 5, 6, 7, 8, 9]   
```
#### Desde otro `array` con `Array.from()`

El método estático `Array.from()`, aunque ahora quizás no le encontremos mucha utilidad, nos resultará muy interesante más adelante. Este método se suele utilizar para convertir variables *«parecidas»* a los `arrays` (pero que no son `arrays`) en un . Este es el caso de variables como `strings` o de lista de elementos del DOM (`nodelist`):

```js
let saludo = "Hola Mundo!";
let nuevoArr = Array.from(arr);         // ["H", "o", "l", "a", " ", "M", "u", "n", "d", "o", "!"]

let divs = document.querySelectorAll("div");
divs.constructor.name;                  // "NodeList"
let divsArr = Array.from(divs);         // ["div", "div", ...] (los que existan en al página)
```

De forma opcional, `Array.from(obj)` puede recibir un parámetro adicional: una función que actuará de forma idéntica a una función `map()`:

```js
let numerosTexto = "12345";
let numeros = Array.from(numerosTexto, (num) => Number(num));   // [1, 2, 3, 4, 5]

```

#### Desestructuración 

Vamos a ver como funciona la desestructuración de elementos en un `array`. Esto como veremos es aplicable a otro tipo de datos como los objetos.

```js
let elementos = [5, 2];
let [first, last] = elementos;    // first = 5, last = 2

elementos = [5, 4, 3, 2];
let [first, second] = elementos;  // first = 5, second = 4, rest = descartado

elementos = [5, 4, 3, 2];
let [first, , third] = elementos; // first = 5, third = 3, rest = descartado

elementos = [4];
let [first, second] = elementos;  // first = 4, second = undefined
```

* En el primer caso, bastante obvio, extraemos el primer y segundo valor del array elements en una variable denominada `first` y otra llamada `last`.
* En el segundo caso, hacemos lo mismo en las variables `first` y `second`, pero como el array tiene más elementos y sólo hemos indicado dos variables (`first` y `second`), el resto son descartadas.
* En el tercer caso pasa muy parecido, excepto que en el segundo parámetro de la parte izquierda, no colocamos ningún elemento, por lo tanto, ese dato se descartará.
* En el cuarto caso, nos pasa al contrario, y hay menos elementos que variables, por lo que `first` toma el primer (y único) elemento y `second` se queda sin ningún valor (obtiene el valor undefined).

Otro ejemplo donde podemos combinarlo con la asignación por defecto de una valor a una variable:

```js
let [saludo = "hey", nombre = "Sarah"] = ["Hola"];

console.log(saludo);          // "Hola"
console.log(nombre);              // "Sarah"
```
También disponemos del operador `...`, que puede actuar como `spread operator` (*expandir*) o como `rest operator` (*agrupar*) se puede usar cuando todos los elementos de un `object` o `array` deben incluirse en un nuevo `array` u `object`, o deben aplicarse uno por uno en la lista de argumentos de una llamada de función. 

```js
let debug = (param) => console.log(...param);
let arr = [1, 2, 3, 4, 5];
debug(arr);               // 1 2 3 4 5
```

En este caso se ha **expandido** el `array` haciendo que esos 5 elementos se conviertan en elementos individuales.

```js
let debug = (...param) => console.log(param);
debug(1, 2, 3, 4, 5);       // [1, 2, 3, 4, 5]

// La agrupación la hacemos en la definición de la función, de lo contraio, esto daría error.
let debug = (param) => console.log(...param);
debug(1, 2, 3, 4, 5); 
```

Veamos otro ejemplo mas ilustrativo:

```js
function showName(firstName, lastName, ...titles) {
  console.log(`${firstName} ${lastName}`); // Julius Caesar

  // the rest go into titles array
  // titles = ["Consul", "Imperator"]
  console.log(titles[0]); // Consul
  console.log(titles[1]); // Imperator
  console.log(titles.length); // 2
}

showName("Julius", "Caesar", "Consul", "Imperator");
```

#### Convertiendo a `string` un `array`

Ya hemos visto como podemos convertir una cadena te texto o `string` en un `array` separandolo con el método `.split()`. El paso inverso lo podemos realizar con el método `.join()`.

```js
let letras = ["a", "b", "c"];

// Une elementos del array por el separador indicado
letters.join("->");       // Devuelve 'a->b->c'
letters.join(".");        // Devuelve 'a.b.c'

// Separa elementos del string por el separador indicado
"a.b.c".split(".");       // Devuelve ['a', 'b', 'c']
"5-4-3-2-1".split("-");   // Devuelve ['5', '4', '3', '2', '1']
```

También podría interesarnos el método `.toString()` que lo que hace es convertir directamente el `array` en una cadena de texto concatenando todos sus elementos (incluidas las comas separadoras de elementos).

```js
let nombres = ["Jhon", "Mary", "Jordan", "Ann", "Jason", "Lucy"] 
nombres.toString()          // "Jhon,Mary,Jordan,Ann,Jason,Lucy"
```