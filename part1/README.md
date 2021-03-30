# Parte 1: Introducción a React

_En esta parte nos familiarizaremos con la librería React, la cual utilizaremos para escribir el código que correrá en el navegador. Empezaremos con algunas funciones y características de JavaScrip que son importantes para entender React._

1. [JavaScript]()

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