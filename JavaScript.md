JavaScript es un lenguaje _débilmente tipado_ y _dinámico_. Las variables en JavaScript no están asociadas directamente con ningún tipo de valor en particular, y a cualquier variable se le puede asignar (y reasignar) valores de todos los tipos:
```js
let x = "hola mundo";
x = 2;
x = true;
```
## Variables
Es buena practica de programacion asignar un valor inicial a las variables cuando estas son declaradas.

Podemos declarar e inicializar mas de una variable en una sola linea

```js
var mensaje = "hola mundo";
let i = 0, j = 0, k = 0;
```
### Var
El valor predeterminado es `undefined`

El ámbito de una variable declarada con la palabra reservada **`var`** es su _contexto de ejecución_ en curso
### Let
Si no se especifica un valor inicial para una variable con la sentencia `let` la variable es declarada, pero su valor es `undefined` hasta que se le asigne un valor.
### Const
Las variables constantes presentan un **ámbito de bloque** (scope) tal y como lo hacen las variables definidas usando la instrucción let, con la particularidad de que el valor de una constante no puede cambiarse a través de la reasignación. Las constantes no se pueden redeclarar.

Es necesario **inicializar** la constante, es decir, se debe especificar su valor en la misma sentencia en la que se declara, lo que tiene sentido, dado que no se puede cambiar posteriormente.

Es una convención común (pero no universal) declarar constantes utilizando nombres con letras mayúsculas como `H0` o `HTTP_NOT_FOUND`
como forma de distinguirlas de las variables.

También se puede utilizar `const` para declarar variables para los bucles __for/in__ y __for/of__, siempre que el cuerpo del bucle no reasigne un nuevo valor. En este caso, la declaración `const` sólo está diciendo que el valor es constante durante la duración de una iteración del bucle:

```js
const lista = [1,2,3,4,5];
for (const data in lista)console.log(data)
for (const datum of lista) console.log(datum);
```

## Hoisting
El concepto de __Hoisting__ fue pensado como una manera general de referirse a cómo funcionan los contextos de ejecución en JavaScript (específicamente las fases de creación y ejecución)
una estricta definición de hoisting sugiere que las declaraciones de variables y funciones son físicamente movidas al comienzo del código, pero esto no es lo que ocurre en realidad. Lo que sucede es que las declaraciones de variables y funciones son **asignadas en memoria** durante la fase de compilación, pero quedan exactamente en dónde las has escrito en el código.

==Scope==
_El contexto en el que los valores y las expresiones son "visibles" o pueden ser referenciados. Si una variable u otra expresión no está "en el Scope- alcance actual", entonces no está disponible para su uso_

**La elevación (Hoisting) afecta la declaración** de variables, pero **no su inicialización**. El valor será asignado exactamente cuando la sentencia de asignación sea alcanzada.

### Hoisting Var
El ámbito de una variable declarada con la palabra reservada **`var`** es su _contexto de ejecución_ en curso, que puede ser la función que la contiene o, para las variables declaradas afuera de cualquier función, un ámbito global.

```js
console.log(pokemon); // undefined
var pokemon = "Charizard";
```

```js
var pokemon = "Diglett";

(function name(){

	console.log(pokemon) // undefined

	var pokemon = "Charizard"

	console.log(pokemon) // Charizard

}());
```

Los ejemplos anteriores se entiende implícitamente como:

```js
var pokemon; // "se elevo la declaracion"
console.log(pokemon); // undefined
var pokemon = "Charizard";
```

```js
var pokemon = "Diglett";

(function name(){
	var pokemon; //"se elevo la declaracion"
	console.log(pokemon) // undefined
	var pokemon = "Charizard"
	console.log(pokemon) // Charizard
}());
```

Como la declaración de variables se procesa antes de ejecutar cualquier código, declarar una variable en cualquier parte del código es igual a declararla al inicio del mismo. Lo que ocurre aquí y para que se entienda, es que hipotéticamente la variable se **eleva** y pasa a declararse **al comienzo de su contexto** (scope).

### Hoisting let y const
No son inicializadas con un valor por defecto. Acceder a una variable declarada con let o const antes de que sea declarada resulta en un `ReferenceError`:

Funcionan casi de la misma manera que var, pero con algunas diferencias importantes. La más notable es que let tienen un ámbito (scope) de bloque, pero var tiene un ámbito de función.

```js
if (true){

let pokemon = "Charmander";

console.log(pokemon); // Charmander

}
console.log(pokemon); //ReferenceError: pokemon is not defined
```

## Tipo de datos
**Primitivos**
- Undefined 
- Boolean  
- Number
- String 
- BigInt 
- Symbol
- Null _Tipo primitivo especial_

Todos los primitivos son **inmutables**, es decir, no se pueden modificar. Es importante no confundir un primitivo en sí mismo con un valor primitivo asignado a una variable. Se puede reasignar un nuevo valor a la variable, pero el valor existente no se puede cambiar de la misma forma en que se pueden modificar los objetos, los arreglos y las funciones.


_El uso de un método de cadena no modifica la cadena_

```js
let pokemon = "Charizard";
pokemon.toUpperCase();
console.log(pokemon) // Charizard
```

_La asignación le da al primitivo un nuevo valor (no lo muta)_

```js
let pokemon = "Charizard";
pokemon = pokemon.toUpperCase();
console.log(pokemon) // CHARIZARD
```

Un primitivo se puede reemplazar, pero no se puede modificar directamente.

En lugar de cambiarlos directamente, modificas una _copia, sin afectar el original_


**Estructurales**

- Object
- Function

# Operadores

### Bitwise Operators


# Funciones


Una función es un bloque de código que realiza una acción o devuelve un valor. Las funciones son código personalizado definido por los programadores que son reutilizables, y por lo tanto pueden hacer que sus programas sean más modulares y eficientes.

**Parámetro** es una variable listada dentro de los paréntesis en la declaración de función (es un término para el momento de la declaración).

**Argumento** es el valor que es pasado a la función cuando esta es llamada (es el término para el momento en que se llama).

### Nomenclatura de funciones

Las funciones son acciones. Entonces su nombre suele ser un verbo. Debe ser breve, lo más preciso posible y describir lo que hace la función, para que alguien que lea el código obtenga una indicación de lo que hace la función.



```javascript
showMessage(..)     // muestra un mensaje
getAge(..)          // devuelve la edad (la obtiene de alguna manera)
calcSum(..)         // calcula una suma y devuelve el resultado
createForm(..)      // crea un formulario (y usualmente lo devuelve)
checkPermission(..) // revisa permisos, y devuelve true/false
```


## Funciones Declaradas.
Las declaraciones de funciones se cargan en el contexto de ejecución antes de que se ejecute cualquier código. Esto se conoce como **hoisting**, lo que significa que puedes utilizar la función antes de declararla.

El nombre de la funcion se convierte en una variable cuyo valor es la misma funcion.

```javascript
function sum(a, b) {
  return a + b;
}
```

La sentencia `return` hace que la función deje de ejecutarse
y devuelva el valor de su expresión (si lo tiene).Si la sentencia return no tiene una expresión asociada, el valor de retorno de la función sera `undefined`.

```javascript
console.log(sum(2, 2));

function sum(a, b) {
  return a + b;
}
```

## Expresión de función 

Una expresión de función es una función que no está precargada en el contexto de ejecución, y sólo se ejecuta cuando el código la encuentra. Se asignan a una variable, y pueden ser anónimas.

```javascript
let sum = function(num1, num2) {
return num1 + num2;
};
```

Si se intenta ejecutar la función antes de declararla, se producirá un error:

```javascript
console.log(sum(2,2)); // no se puede acceder antes de la inicializacion 
let sum = function(num1, num2) {
return num1 + num2;
};
```



## Funciones Flecha

Una **expresión de función flecha** es una alternativa compacta a una `expresión de función` tradicional

```javascript
let sum = (a, b) => a + b;
console.log(sum(2,3));
```

No requieren los paréntesis si sólo desea utilizar un único parámetro. Si desea cero parámetros, o más de un parámetro, los paréntesis son necesarios.

```javascript
let square = x => x**2
console.log(square(2));
```

Del mismo modo, si el cuerpo requiere **líneas de procesamiento adicionales**, deberás volver a introducir los corchetes **Más el "return"**

```javascript
const saludar = (firsName, lastName) => {
	let saludo = "hola";
	return `${saludo}! ${firsName} ${lastName}`;
}
```

Al igual que las expresiones de función tradicionales, las funciones de flecha no se elevan, por lo que no es posible llamarlas antes de declararlas. También son siempre anónimas: no hay forma de nombrar una función de flecha. 

```javascript
console.log(sum(2,3)); // error
let sum = (a, b) => a + b;

```



# Arrays
Son listas ordenadas de datos, pero a diferencia de otros lenguajes, pueden contener cualquier tipo de
datos en cada indice. Esto significa que es posible crear un array que tenga una cadena en la primera posición un número en la segunda, un objeto en la tercera, y así sucesivamente. Las matrices de ECMAScript también tienen un tamaño dinámico es decir que va creciendo automáticamente para acomodar cualquier dato que se añada a ellos.

Las matrices pueden crearse de varias formas básicas. Una de ellas es utilizar el constructor Array

```javascript
const colors = new Array();
```

Si conoces el número de elementos que habrá en el array, puedes pasarselo al constructor
y la propiedad length se creará automáticamente con ese valor. 

```javascript
const colors = new Array(20);
```

Es posible omitir el operador `new` cuando se utiliza el constructor `Array()`. El resultado es el mismo.

```javascript
const colors = Array(3);
const pokemon = Array('Charizard');
```

Una segunda forma de crear un array es utilizando **array literal notation**. Un **array literal**  se especifica utilizando corchetes y colocando una lista de elementos separados por comas entre ellos.

```javascript
const colors = ["red", "blue", "green"];
const names = [];
const values = [1,2,];
```

Usa la sintaxis literal para la creación de arreglos

```javascript
// mal
const items = new Array();

// bien
const items = [];
```

# Objetos
Un objeto es una colección de propiedades, y una propiedad es una asociación entre un nombre (o _clave_) y un valor. El valor de una propiedad puede ser una función, en cuyo caso la propiedad es conocida como un método.

Cualquier valor en JavaScript que no sea una cadena, un número, un símbolo, o
verdadero, falso, nulo o indefinido es un objeto. Y aunque las
cadenas, números y booleanos no son objetos, pueden comportarse como
objetos inmutables.

> Los objetos son mutables y se manipulan por referencia
en lugar de por valor.

La forma comun de crear un objeto personalizado es crear una nueva instancia de `Object` y añadirle propiedades y métodos.

```js
const pokemon = new Object();

pokemon.name = "Onix";

pokemon.type = ["ground","rock"];

pokemon.attack = 45;

pokemon.defense = 160;
```


Otra manera de crear un objeto es haciendo uso de un **Objeto literal**

**Objeto literal** se le llama al objeto cuyas propiedades están declaradas textualmente en el código.

```js
const pokemon = {

	name: "Onix",

	type: ["ground", "rock"],

	attack: 45,

	defense: 160,

	sayName:function(){

		console.log(this.name)

	}

}
```


### CRUD
- **Create**

```js
pokemon.speed = 70;
```

- **Read**

Para obtener el valor de una llave en un objeto utilizamos la notación punto (`.`):

```js
console.log(pokemon.name);
```

Existe otra forma equivalente de obtener el valor de una llave utilizando corchetes cuadrados (`[]`)

```js
console.log(pokemon["name"]);
```

- **Update**

```js
pokemon.speed = 75;
```

- **Delete**

```js
delete pokemon.speed;
```


Comprobar si existe o no una propiedad en el objeto

El método **`hasOwnProperty()`** devuelve un booleano indicando si el objeto tiene la propiedad especificada.

```js
const pokemon = {

	name: "Onix",

	type: ["ground", "rock"],

	attack: 45,

	defense: 160,

	sayName:function(){

		console.log(this.name)

	}

}

console.log(pokemon.hasOwnProperty("name")) //true
console.log(pokemon.hasOwnProperty("speed")) //false

```

> Las funciones flecha no se deben utilizar como metodos

## Enumerar las propiedades de un objeto

==**for in**==
devuelve un array con los nombres de las propiedades propias enumerables de un objeto. No incluye propiedades no enumerables, propiedades heredadas o propiedades
cuyo nombre es un `Symbol`

- **Mostrar las key del objeto**

```js
for (const property in pokemon){

	console.log(pokemon[property])

}
//name
//type
//attack
//defense
//sayName
```

- **Mostrar los valores del objeto**

```js
for (const property in pokemon){

	console.log(property)

}
```

==**getOwnPropertyNames**==

El método `Object.getOwnPropertyNames()` devuelve un array con todas las propiedades (numerables o no) encontradas en un objeto dado.

```js
for (const property of Object.getOwnPropertyNames(pokemon)){

	console.log(property)

}
// name
//type
//attack
//defense
//sayName

// Object.getOwnPropertyNames(pokemon)
//[ 'name', 'type', 'attack', 'defense', 'sayName' ]
```

==**Object.values()**==

Devuelve un array con los valores correspondientes a las propiedades **enumerables** de un objeto.

```js
for (const values of Object.values(pokemon)){

	console.log(values)

}
//Onix
//[ 'ground', 'rock' ]
//45
//160
//[Function: sayName]
```

==**Object.entries()**==

Devuelve una matriz de pares propios de una propiedad enumerable [key value] de un objeto dado.

```js
for (const x of Object.entries(pokemon)){

	console.log(x)

}
//[ 'name', 'Onix' ]
//[ 'type', [ 'ground', 'rock' ] ]
//[ 'attack', 45 ]
//[ 'defense', 160 ]
//[ 'sayName', [Function: sayName] ]
```

==**Object.keys()**==
Devuelve un array cuyos elementos son strings correspondientes a las propiedades enumerables que se encuentran directamente en el objeto.

```js
for (const key of Object.keys(pokemon)){

	console.log(key)

}
//name
//type
//attack
//defense
//sayName
```

## Funcion Fabrica

Cuando una función devuelve un objeto, la llamamos función de fábrica. Cada vez que llamamos a esta funcion fábrica, devolverá una nueva instancia del objeto.

No tenemos que anteponer los nombres de nuestras fábricas con create pero puede hacer que la intención de la función sea más clara para los demás.  

```js
function createPokemon(name, attack, defense,type){
	return{
		name,
		attack,
		defense,
		type,
		sayName(){
			return `I am ${name}`;
		}
	}
}

const charizard = createPokemon("charizard",84,78,["Fire","Flying"]);
const onix = createPokemon("onix",45,160,["Ground","Rock"]);

console.log(charizard.sayName());
console.log(onix.sayName());
```



## Funcion Constructora

```js
function Pokemon(name,attack,defense,type){
	this.name = name;
	this.attack = attack;
	this.defense = defense;
	this.type = type;

	// this.sayName = () => `I am ${this.name}`
	this.sayName = () => {
		return `I am ${this.name}`;
	}

}

const charizard = new Pokemon("charizard",84,78,["Fire","Flying"]);
console.log(charizard.sayName());
```



## Prototipos

Los prototipos son un mecanismo mediante el cual los objetos en JavaScript heredan características entre sí

Un objeto prototipo del objeto puede tener a su vez otro objeto prototipo, el cual hereda métodos y propiedades, y así sucesivamente. Esto es conocido con frecuencia como la **cadena de prototipos**, y explica por qué objetos diferentes pueden tener disponibles propiedades y métodos definidos en otros objetos.

Para ser exactos, los métodos y propiedades son definidos en la propiedad `prototype`, que reside en la función constructora del objeto, no en la instancia misma del objeto.



















































