# Como se definen variables en JavaScript
Las variables en JavaScript se crean mediante la palabra reservada `var`.

por ejemplo:

``` 

var numero_1 = 3;
var numero_2 = 1;
var resultado = numero_1 + numero_2;

```
Una de las características más sorprendentes de `JavaSript` para los programadores habituados a otros lenguajes de programación es que tampoco es necesario declarar las variables. En otras palabras, se pueden utilizar variables que no se han definido anteriormente mediante la palabra reservada `var`.  
El ejemplo anterior también es correcto en `JavaScript` de la siguiente forma:
```
var numero_1 = 3;  
var numero_2 = 1;  
resultado = numero_1 + numero_2;
```
La variable resultado no está declarada, por lo que `JavaScript` crea una variable global y le asigna el valor correspondiente. De la misma forma, también sería correcto el siguiente código:
```
numero_1 = 3;
numero_2 = 1;
resultado = numero_1 + numero_2;
```
En cualquier caso, se recomienda declarar todas las variables que se vayan a utilizar.

El nombre de una variable también se conoce como identificador y debe cumplir las siguientes normas:

+ Sólo puede estar formado por letras, números y los símbolos $ (dólar) y _ (guión bajo).
+ El primer carácter no puede ser un número.

Por tanto, las siguientes variables tienen nombres correctos:
```
var $numero1;  
var _$letra;  
var $$$otroNumero;  
var $_a__$4;
```
Sin embargo, las siguientes variables tienen identificadores incorrectos:
```
var 1numero;       // Empieza por un número  
var numero;1_123;  // Contiene un carácter ";"
```

# Ambito de variable (Scope)

El ámbito de una variable (llamado "scope" en inglés) es la zona del programa en la que se define la variable. JavaScript define dos ámbitos para las variables: global y local.
## Locales
Si una variable en `JS` es declarada dentro de una funcion, esta solo podra  ser utilizada por la propia funcion, este es el caso de las variables locales.  
En el siguente ejemplo se usara una variable local fuera de la funcion declarada.

```
function creaMensaje() {
  var mensaje = “Mensaje de prueba”;
}
creaMensaje();
alert(mensaje);
```
La variable `mensaje` a sido declarada dentro de la funcion `crearMensaje()` y la funcion `alert()` hace uso de la variable `mensaje` fuera de la funcion `crearMensaje()`, de esta forma escrita al momento de ejecutar no se mostrara el mensaje, ya que no se reconocera la variable `mensaje` fuera de la funcion `crearMensaje()`.
La manera correcta es la siguiente:

```
function creaMensaje() {
  var mensaje = “Mensaje de prueba”;  
  alert(mensaje);
}
creaMensaje();

```

## Globales
Por otra parte si se declara una variable fuera de cualquier funcion esta en automatico sera de ambito global. Se ilustrara lo anterior con los ejemplos ya hechos.

```
var mensaje = “Mensaje de prueba”;
function creaMensaje() {
    alert(mensaje);
}
creaMensaje();

```
En este caso la variable `mensaje` puede ser utilizada dentro y fuera de la funcion `crearMensaje()` ya que al ser declarada fuera de la funcion se entiende que se ambito global.

# Elevacion (Hoisting)

Para entender el concepto de elevacion nos iremos sobre el siguiente codigo:
```


    //Variable global
    var name = "Jose";

    function HelloWorld(){
      //Variable local
      var name = "Pepe";
      alert(name);
    }

    HelloWorld();

```
Las reglas de precedencia de variables en JavaScript dicen que las variables locales preceden a las globales, por lo que en este caso veríamos aparecer por pantalla la palabra “Pepe” que es el valor de la variable local.

Sin embargo ahora vamos a hacerle un sutil cambio al código anterior y haremos lo siguiente:

```
//Variable global
var name = "Jose";

function HelloWorld(){
   alert(name);
   //Variable local
   var name = "Pepe";
}

HelloWorld();
```
¿Qué veremos ahora por pantalla?

Por lógica parece que deberíamos ver “Jose”, ya que en el momento de llamar al alert todavía no se ha declarado la variable local, y por lo tanto se debería acceder a la global ¿verdad? Pues no.

Lo que veremos por pantalla es  “undefined”:

![Undefined](https://www.jasoft.org/Blog/image.axd?picture=Undefined.gif)

Aunque `JavaScript` es un lenguaje interpretado y procesa las líneas de código una a una según se las va encontrando, en realidad no es del todo así. En el caso de las variables que hay dentro de una función lo que hace el intérprete es declararlas todas a la vez al principio de la función, independientemente de donde estén realmente declaradas dentro de ésta.   
Por eso, en el ejemplo anterior aunque la variable está declarada y definida abajo del todo, cuando la vamos a mostrar nos devuelve un “undefined”: el intérprete “eleva” la declaración implícitamente al principio de la función, así que el código anterior es equivalente a este:

```
//Variable global
var name = "Jose";

function HelloWorld(){
   //Variable local
   var name;
   alert(name);
   name = "Pepe";
}

HelloWorld();
```