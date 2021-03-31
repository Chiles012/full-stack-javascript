# Parte 1: Introducción a React

_En esta parte nos familiarizaremos con la librería React, la cual utilizaremos para escribir el código que correrá en el navegador. Empezaremos con algunas funciones y características de JavaScrip que son importantes para entender React._

1. [JavaScript](#-javascript-)
    * [Variables](#-variables-)

## 🔹🔹🔹 JavaScript 🔹🔹🔹

_Durante el curso, vamos a tener la necesidad de aprender basta JavaScript además del desarrollo web en si._

_JavaScript a avanzado rapidamente en los últimos años y aquí utilizaremos las nuevas características de las nuevas versiones. El nombre oficial de lo que sería el estándar JavaScript es ECMAScript. En este momento, la última versión es [ECMAScript®2020](https://www.ecma-international.org/ecma-262/), también conocido como ES11._

_Los navegadores todavía no soportan todas las nuevas funciones de JavaScript. Debido a esto, mucho código que corre en el navegador debe ser **transpilado** de una versión nueva de JavaScript a una versión más vieja, con mayor compatibilidad._

_Hoy en día, la manera mas común de transpilar código es utilizando [Babel](https://babeljs.io/). Como veremos más adelante las aplicaciones creadas con `create-react-app`, la transpilación es configurada automaticamente. En la [parte 7]() del este curso veremos más de cerca la configuración de la transpilación._

_[Node.js](https://nodejs.org/en/) es un entorno de ejecución de JavaScript basado en el motor [Chrome V8](https://developers.google.com/v8/) de Google y funciona practicamente en todos lados, desde servidores hasta en celulares. En un principio veremos como escribir algo de JavaScript utilizando Node. Para esto es recomendado utilizar la versión 14.8.0 o superiores de Node, que ya entienden las ultimas versiones de JavaScript, por lo que no es necesario transpilar el código._

_El código es escrito en archivos con la extensión **.js** y pueden ser ejecutados en consola utilizando el comando `node nombre_de_archivo.js`_

_Es posible escribir código JavaScript en la consola de Node.js, que puede ser abierta utilizando el comando `node` en la linea de comando, como también se hace en la consola de desarrollo del navegador. Las nuevas versiones de Chrome manejan las nuevas funciones [bastante bien](http://kangax.github.io/compat-table/es2016plus/) sin transpilar el código. De manera alternativa se puede utilizar una herramienta como [JS Bin](https://jsbin.com/?js,console)._

_Como me ocurría a mi en un principio, es muy común confundir JavaScript con Java por nombre y sintaxis, pero cuando uno se interioriza en el mecanismo central del lenguaje son muy diferentes en realidad. Si uno viene de Java, el comportamiento de JavaScript puede parecer bastante extraño, especialmente si uno no trata de buscar sus caracteristicas._

_Hay un artículo escrito por [Stephen Curtis](https://twitter.com/stephenthecurt) que puede ser leído [aquí](https://medium.com/@stephenthecurt/33-fundamentals-every-javascript-developer-should-know-13dd720a90d1), del cual nació este respositorio, llamado [33 conceptos que todo desarrollador de JAvaScript debería saber](https://github.com/leonardomso/33-js-concepts), el cual fue considerado uno de los mejores proyectos open source del año 2018, que recopila información de todos estos conceptos._

_Más adelante desarrollaré estos conceptos en profundidas, asi y todo trataré de que se entiendan lo mejor posible a lo largo de este curso._

### 🔹🔹🔹 Variables 🔹🔹🔹

_En JavaScript hay varias formas de definir variables:_

~~~
const x = 1
let y = 5

console.log(x, y)   // 1, 5 son mostrados
y += 10
console.log(x, y)   // 1, 15 son mostrados
y = 'sometext'
console.log(x, y)   // 1, sometext son mostrados
x = 4               // causa un error
~~~

_En realidad, [const](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/const) no define una variable, sino que define constante cuyo valor no se puede cambiar. Por otro lado, [let](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/let) define una variable normal._

_En el ejemplo anterior, también vemos que el tipo de datos asignados a la variable puede cambiar durante la ejecución. Al principio `y` almacena un número entero y al final un string. Esta caracteristica del lenguaje se la suele llamar [tipado dinámico](https://developer.mozilla.org/es/docs/Web/JavaScript/Data_structures)._

_Es posible también definir variables en JavaScript utilizando la palabra reservada [var](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Statements/var). `var` era, hace un tiempo atras, la única manera para definir variables. const y let fueron agregados recientemente en la version ES6. En situaciones especiales, var funciona de una manera direferente comparado con la definición de variables de la mayoría de los lenguajes. Durante este curso yo no recomiendo utilizar `var` sino utilizar const y let. Aunque está en inglés, recomiendo ver este video en Youtube: [var, let and const - What, why and how - ES6 JavaScript Features](https://www.youtube.com/watch?v=sjyJBL5fkp8) de [mpj](https://twitter.com/mpjme)._

