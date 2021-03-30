# Parte 0: Fundamentos de las aplicaciones Web

_En esta parte se desarrollarán los conceptos basicos del desarrollo web y se hablará de como evolucionó el desarrollo de aplicaciones web en las últimas décadas._

1. [Fundamentos de las aplicaciones Web](#-fundamentos-de-las-aplicaciones-web-)
    * [HTTP GET](#-http-get-)
    * [Aplicaciones web tradicionales](#-aplicaciones-web-tradicionales-)
    * [La lógica de la aplicación corriendo en el navegador](#-la-lógica-de-la-aplicación-corriendo-en-el-navegador-)
    * [Control de eventos y funciones Callback](#-control-de-eventos-y-funciones-callback-)
    * [DOM o Modelo de Objetos del Documento](#-dom-o-modelo-de-objetos-del-documento-)
    * [Manipulando el Document-Object desde la consola](#-manipulando-el-document-object-desde-la-consola-)
    * [CSS](#-css-)
    * [Cargando una página que contiene JavaScript](#-cargando-una-página-que-contiene-javascript)
    * [Formularios y HTTP POST](#-formularios-y-http-post-)
    * [AJAX](#-ajax-)
    * [SPA o aplicación de una página](#-spa-o-aplicación-de-una-página-)
    * [Librerías de JavaScript](#-librerías-de-javascript-)
    * [Desarrollo web full stack](#-desarrollo-web-full-stack-)



## 🔹🔹🔹 Fundamentos de las aplicaciones Web 🔹🔹🔹

_A continuación podremos observar unas imágenes que servirán para demostrar conceptos básicos pero que no quieren decir que sean ejemplos de como las aplicaciones Web deben ser. Por el contrario, muestran viejas tecnicas de desarrollo web que pueden considerarse_ **malas prácticas** _hoy en día._

_Durante todo el curso se estará utilizando el navegador Chrome._

**_La primera regla del desarrollo Web:_** _Siempre tener a la vista la Consola de Desarrollo abierta en tu navegador. En macOS, la consola se abre presionando `F12` o `option-cmd-i` simultaneamente. En Windows o Linux, la consola se abre presionando `F12` o `ctrl-shift-i` simultaneamente._

_La consola se ve de la siguiente manera:_

![consola](./img/1e.png)

_Es recomendable,en la pestaña Network, tener marcada la opcion de deshabilitar el cache (Disable cache) como se muestra en la imagen, ya que de no hacerlo es muy probable que no veamos los cambios que realicemos a nuestro código. Preservar el log (Preserve log) puede ser muy util ya que guarda los logs ya mostrados por la aplicacion cuando la página es recargada._

**Nota:** _La pestaña mas importante es la **Consola**. Sin embargo, en esta introducción se estará utilizando bastante la pestaña **Network**._



### 🔹🔹🔹 HTTP GET 🔹🔹🔹

_El servidor y el navegador web se comunican uno con el otro mediante el protocolo [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP). La pestaña Network muestra como se comunican el navegador y el servidor._

_Cuando la pagina es recargada (presionando `F5` o en el simbolo ↺ del navegador), la consola muestra que dos eventos han sucedido:_

* _El navegador recupera (fetch) el contenido de la pagina fullstack-exampleapp.herokuapp.com del servidor._

* _Y descarga la imagen kuva.png_

![fetches](./img/2e.png)

_En una pantalla pequeña puede que se deba ampliar la ventana de la consola para verlo._

_Clickeando en el primer evento hará que se nos muestre mas informacioón sobre lo que está sucediendo:_

![event](./img/3e.png)

_La parte de arriba, General, muestra que el navegador hizo una petición (request) a la dirección `https://fullstack-exampleapp.herokuapp.com` usando el método GET, y que la petición fue exitosa, porque la respuesta del servidor tiene un [Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) **200**._

_La petición y la respuesta del servidor tiene varios encabezados (headers):_

![headers](./img/4e.png)

_Los response headers (encabezados de la respuesta) nos dicen, por ejemplo, el tamaño de la respuesta en bytes, y el tiempo exacto de la respuesta. Un encabezado importante es el [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) que nos dice que la respuesta es un archivo de texto en formato [utf-8](https://en.wikipedia.org/wiki/UTF-8), cuyo contenido ha sido formateado en HTML. De esta manera el navegador sabe que la respuesta es una pagina [HTML](https://en.wikipedia.org/wiki/HTML), y que debe renderizarlo en el navegador 'como una pagina web'._

_La pestaña Response (respuesta) muestra los datos de la respuesta, una página HTML normal. La sección **body** determina la estructura de la página renderizada en la pantalla:_

![headers](./img/5e.png)

_La página contiene un elemento [div](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div), que dentro contiene un heading (encabezado), un link a una página notes, y una etiqueta [img](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img), y muestra el número de notas creadas._

_Debido a la etiqueta img, el navegador realiza una segunda petición HTTP para recuperar la imagen kuva.png de el servidor. El detalle de la petición es el siguiente:_

![img etiqueta](./img/6e.png)

_La petición se realizó a la dirección `https://fullstack-exampleapp.herokuapp.com/kuva.png` y su tipo es HTTP GET. El encabezado de la respuesta nos dice que el tamaño de la respuesta es de 89350 bytes, y su [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) es image/png, asi que es una imagen png. El navegador usa esta información para renderizar la imagen correctamente en la pantalla._

_La cadena de eventos causada por abrir la página `https://fullstack-exampleapp.herokuapp.com` en el navegador genera el siguiente [diagrama de secuencia](https://www.geeksforgeeks.org/unified-modeling-language-uml-sequence-diagrams/):_

![secuence diagram](./img/7e.png)

_Primero, el navegador hace una solicitud HTTP GET al servidor para recuperar el codigo HTML de la pagina. La etiqueta img en el HMTL le indica al navegador que debe recuperar la imagen kuva.png. El navegador renderiza la pagina HTML y la imagen en la pantalla._

_Aunque es dificil de notar, la página HTML comienza a renderizarse antes de que la imagen sea recuperada del servidor._



### 🔹🔹🔹 Aplicaciones web tradicionales 🔹🔹🔹

_La página de inicio de la aplicacion de ejemplo funciona como una aplicacion web tradicional. Cuando uno entra a la página, el navegador recupera el documento HTML detallando la estructura y el contenido textual de la página desde el servidor._

_El servidor ha formateado el documento de alguna manera. El documento puede ser una archivo de texto guardado en el directorio del servidor. El servidor tambien puede formar el documento HTML **dinamicamente** según el codigo de la aplicación, utilizando por ejemplo, datos de una base de datos. El codigo HTML de la aplicación de ejemplo ha sido formado dinamicamente, porque este contiene informacion sobre el número de notas creadas._

_El codigo HTML de la pagina de inicio es el siguiente:_

~~~
const getFrontPageHtml = (noteCount) => {
  return(`
    <!DOCTYPE html>
    <html>
      <head>
      </head>
      <body>
        <div class='container'>
          <h1>Full stack example app</h1>
          <p>number of notes created ${noteCount}</p>
          <a href='/notes'>notes</a>
          <img src='kuva.png' width='200' />
        </div>
      </body>
    </html>
`)
} 

app.get('/', (req, res) => {
  const page = getFrontPageHtml(notes.length)
  res.send(page)
})
~~~

_No es necesario entender el código todavía._

_El contenido de la página HTML ha sido guardado como un **template string**, o un string (cadena de texto) que permite, por ejemplo, evaluar variables dentro de ella. La parte de la página de inicio que cambia dinámicamente, el número de notas guardadas (en el código `noteCount`), es remplazado por el número actual de notas (en el código `notes.length`) en el template string._

_En una aplicación web tradicional el navegador es un poco "tonto". Solo recupera el HTML del servidor, y toda la lógica de la aplicación esta en el servidor. Un servidor puede ser creado, por ejemplo, usando Java Spring, Python Flask o con Ruby on Rails._

_En este curso se utilizará Node.js y su framework Express para crear un servidor web._



### 🔹🔹🔹 La lógica de la aplicación corriendo en el navegador 🔹🔹🔹

_La siguiente imagen corresponde a la página notes, el navegador realiza cuatro solicitudes HTTP:_

![pagina notes](./img/8e.png)

_Todas las solicitudes tienen **diferentes tipos**. El tipo de la primer solicitud es **document**. Es el codigo HTML de la pagina, y se ve de la siguiente manera:_

![first request](./img/9e.png)

_Cuando comparamos la página mostrada en el navegador y el código HTML devuelto por el servidor, notamos que el codigo no contiene la lista de notas. La sección [head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) contiene una etiqueta [script](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script), que hace que el navegador recupere un archivo JavaScript llamado main.js._

_El código JavaScript se ve de la siguiente manera:_

~~~
var xhttp = new XMLHttpRequest()

xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    const data = JSON.parse(this.responseText)
    console.log(data)

    var ul = document.createElement('ul')
    ul.setAttribute('class', 'notes')

    data.forEach(function(note) {
      var li = document.createElement('li')

      ul.appendChild(li)
      li.appendChild(document.createTextNode(note.content))
    })

    document.getElementById('notes').appendChild(ul)
  }
}

xhttp.open('GET', '/data.json', true)
xhttp.send()
~~~

_Los detalles del codigo no son importantes ahora, pero se agregó algo de codigo para darle vida a las imagenes y al texto. En la [parte 1]() se empezará a escribir codigo apropiadamente. El código de ejemplo utilizado en esta parte actualmente no es relevante para las tecnicas de desarrollo de este curso._

>_Algunos podrían perguntarse porque se utiliza el objeto xhttp en lugar del fetch moderno. Esto se debe a que no queremos introducirnos en promesas por el momento, y el código tiene un rol secundario en esta parte. En la [parte 2]() volveremos a la manera moderna de realizar solicitudes al servidor._<

_Inmediatamente después de recuperar la etiqueta **script**, el navegador ejecuta el código._

_Las últimas dos lineas definen que el navegador hace una solicitud HTTP GET a la dirección del servidor /data.json:_

~~~
xhttp.open('GET', '/data.json', true)
xhttp.send()
~~~

_Esta es la solicitud es la mostrada al final de la lista en la pestaña Network._

![data.json](./img/10e.png)

_Acá encontramos las notas en JSON como datos sin procesar. Por defecto, el navegador no es bueno mostrando datos JSON. Se puede utilizar plugins para manejar el formateo. Se puede instalar, por ejemplo, [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) en Chrome, y al recargar la página, los datos se mostrarán bien formateados:_

![formatted json](./img/11e.png)

_Así, el código JavaScript de la página anterior de notas descarga los datos JSON que contienen las notas, y genera una lista a partir del contenido de la nota._

_Esto está hecho por el siguiente código:_

~~~
const data = JSON.parse(this.responseText)
console.log(data)

var ul = document.createElement('ul')
ul.setAttribute('class', 'notes')

data.forEach(function(note) {
  var li = document.createElement('li')

  ul.appendChild(li)
  li.appendChild(document.createTextNode(note.content))
})

document.getElementById('notes').appendChild(ul)
~~~

_El código primero crea una lista no ordenada con la etiqueta [ul](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)..._

~~~
var ul = document.createElement('ul')
ul.setAttribute('class', 'notes')
~~~

_...y luego cada nota es agregada a una etiqueta [li](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li). Solo el valor **content** de cada nota se convierte en el contenido de la etiqueta li. Los datos de las fechas no son utilizados en ningún lugar aquí._

~~~
data.forEach(function(note) {
  var li = document.createElement('li')

  ul.appendChild(li)
  li.appendChild(document.createTextNode(note.content))
})
~~~

_Ahora abrimos la pestaña Console en la consola de desarrollo:_

![console](./img/12e.png)

_Clickeando en el pequeño triángulo al comienzo de la linea, se puede expandir el texto en al consola._

![expand console](./img/13e.png)

_La salida de la consola es causada por el comando `console.log` en el código:_

~~~
const data = JSON.parse(this.responseText)
console.log(data)
~~~

_Así, cuando se reciben los datos del servidor, el código lo muestra en la consola._

_La pestaña Console y el comando `console.log` se convertiran en algo muy familiar durante el curso._



### 🔹🔹🔹 Control de eventos y funciones Callback 🔹🔹🔹

_La estructura de este código es un poco extraña:_

~~~
var xhttp = new XMLHttpRequest()

xhttp.onreadystatechange = function() {
  // el código dentro de esta funcion 
  // se encarga de la respuesta del servidor
}

xhttp.open('GET', '/data.json', true)
xhttp.send()
~~~

_La petición al servidor es enviada en la ultima linea, pero el código que maneja la respuesta se encuentra más arriba. Qué está pasando?_

~~~
xhttp.onreadystatechange = function () {
~~~

_En esta linea, un controlador de eventos (event handler) **onreadystatechange** es definido para el objeto `xhttp` haciendo la petición. Cuando el estado del objeto cambia, el navegador llama a la funcion controladora de eventos. El codigo de la función verifica que el [`readyState`](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/readyState) sea igual a 4 (que significa que **la operación esta completada**) y que el codigo de estado HTTP (status code) de la respuesta es **200**._

~~~
xhttp.onreadystatechange = function() {
  if (this.readyState == 4 && this.status == 200) {
    // el código dentro de esta funcion 
    // se encarga de la respuesta del servidor
  }
}  
~~~

_Esta forma de llamar a los controladores de eventos en JavaScript es muy común. Las funciones controladoras de eventos (event handler functions) son llamadas funciones de [Callback](https://developer.mozilla.org/en-US/docs/Glossary/Callback_function). El codigo de la aplicación no llama por si mismo a la función, sino que lo hace el entorno de ejecución (runtime enviroment), que en este caso seria el navegador. Asi, cada vez que ocurre el evento, el navegador llama a la función en el momento apropiado._



### 🔹🔹🔹 DOM o Modelo de Objetos del Documento 🔹🔹🔹

_Podemos pensar a las páginas HTML como estructuras de árbol._

~~~
html
  head
    link
    script
  body
    div
      h1
      div
        ul
          li
          li
          li
      form
        input
        input
~~~

_Esta misma estructura puede verse en la pestaña de la consola **Elements**._

![elements console](./img/14e.png)

_Asi, el funcionamiento del navegador esta basado en la idea de representar los elementos HTML como un árbol._

_El DOM es una Interfaz de Programación de Aplicaciones (mas conocida como API), que permite la modificación de los elementos del árbol correspondientes a las páginas webs a través de la programación._

_El codigo JavaScript introducido previamente en este capítulo usa la DOM-API para agregar la lista de notas a la página._

_El siguiente código crea un nuevo nodo en la variable `ul`, y agrega algunos nodos hijos a él:_

~~~
var ul = document.createElement('ul')

data.forEach(function(note) {
  var li = document.createElement('li')

  ul.appendChild(li)
  li.appendChild(document.createTextNode(note.content))
})
~~~

_Por último, la rama del árbol de la variable `ul` es colocada en el lugar apropiado en el árbol del HTML de toda la página:_

~~~
document.getElementById('notes').appendChild(ul)
~~~

### 🔹🔹🔹 Manipulando el Document-Object desde la consola 🔹🔹🔹

_El nodo principal del DOM del cual derivan el resto de nodos en un documento HTML es llamado `document` object (objeto document). Podemos realizar varias operaciones en una pagina web usando la DOM-API. Podemos acceder al objeto `document` desde la pestaña Console:_

![document object](./img/15e.png)

_Vamos a agregar una nueva nota a la página desde la consola._

_Primero debemos obtener la lista de notas de la página. La lista está en el primer elemento `ul` de la página:_

~~~
list = document.getElementsByTagName('ul')[0]
~~~

_Luego creamos un nuevo elemento `li` y le agregamos algun texto con el metodo de elementos `textContent`:_

~~~
newElement = document.createElement('li')
newElement.textContent = 'Page manipulation from console is easy'
~~~

_Y finalmente agregamos el nuevo elemento li a la lista:_

~~~
list.appendChild(newElement)
~~~

![element added](./img/16e.png)

_Hay que aclarar que aunque la página se actualiza en el navegador con el nuevo elemento, el cambio no es permanente. Si la pagina es recargada, la nueva nota que agregamos a través de la consola desaparecerá debido a que los cambios no son hechos en el servidor sino en el navegador._



### 🔹🔹🔹 CSS 🔹🔹🔹

_El elemento **head** de el código HTML de la pagina de Notas contiene una etiqueta [link](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link), que le dice al navegador que debe recuperar un archivo de estilos CSS de la dirección main.css._

_CSS (Cascading Style Sheets) que significa hojas de estilo en cascada, es un lenguaje de markup usado para determinar la apariencia de las páginas web._

_El archivo CSS recuperado se ve de la siguiente manera:_

~~~
.container {
  padding: 10px;
  border: 1px solid; 
}

.notes {
  color: blue;
}
~~~

_El archivo define dos [selectores de clase](https://developer.mozilla.org/en-US/docs/Web/CSS/Class_selectors). Estos son utilizados para seleccionar ciertas partes de la página y definir sus reglas de estilo para cambiar su apariencia._

_Las **clases** son [atributos](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/class), que pueden agregarse a los elementos HTML._

_Los atributos CSS pueden examinarse en la pestaña Elements de la consola:_

![css elements tab console](./img/17e.png)

_El elemento **div** mas externo tiene la clase **container**. El elemento **ul** que contiene la lista de notas tiene la clase **notes**._

_Las reglas de CSS definen que el elemento que tenga la clase container será delineado con un borde de un pixel de grosor. Este tambien tendrá un padding de 10 pixel que agrega un espacio vacio entre el contenido del elemento y el borde._

_La segunda regla de CSS nombrada como **notes** configura el color del texto en azul._

_Los elementos HTML tambien pueden tener otro atributos aparte de las clases. El elemento **div** que contiene las notas tiene un atributo [id](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/id). El código JavaScript usa el atributo id para encontrar **un** elemento._

_La pestaña Elements de la consola puede ser usada para cambiar los estilos de los elementos._

![changing css](./img/18e.png)

_Los cambios hechos en la consola no son permantes. Al igual que con los cambios en el DOM, si se quiere que los cambios de estilo sean permanentes deben ser guardados en el servidor._


### 🔹🔹🔹 Cargando una página que contiene JavaScript 🔹🔹🔹

_Cuando abrimos en el navegador una página como la de notas que contiene JavaScript, el diagrama de secuencia es el siguiente:_

![secuence diagram js](./img/19e.png)

* _El navegador recupera el código HTML que define el contenido y la estructura de la página desde el servidor utilizando una solicitud HTTP GET._
* _Los links en el código HTML hacen que el navegador también recupere las hojas de estilo CSS, en este caso, main.css._
* _Y también el archivo de código JavaScript main.js._
* _El navegador ejecuta el código JavaScript. El código hace una petición HTTP GET a la dirección `https://fullstack-exampleapp.herokuapp.com/data.json` que retorna las notas como datos JSON._
* _Una vez que los datos han sido recuperados, el navegador ejecuta el controlador de eventos, que renderiza las notas en la página utilizando la DOM-API._



### 🔹🔹🔹 Formularios y HTTP POST 🔹🔹🔹

_A continuación veremos como se agrega una nueva nota a la lista._

_La página notas contiene un elemento [form](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Your_first_HTML_form)._

![form element](./img/20e.png)

_Cuando el botón del formulario es presionado, el navegador enviará la entrada del usuario al servidor. Veamos como se ve el envio del formulario en la pestaña Network:_

![form submit network tab](./img/21e.png)

_Enviar el formulario causa **cinco** peticiones HTTP. La primera equivale al evento de enviar el formulario. Vemamos que muestra:_

![form submit headers](./img/22e.png)

_Esta es una peticion HTTP POST realizada a la direccion del servidor `/new_note`. El servidor responde con un HTTP status code 302, que significa **encontrado**. Esto es una [redirección a un URL](https://en.wikipedia.org/wiki/URL_redirection), con la cual el servidor le solicita al navegador que realice una solicitud HTTP GET a la dirección que esta definida en los headers de la respuesta: `Location: /notes`_

_Así, el navegador recarga la página Notes. La recarga genera tres solicitudes HTTP más: La de recuperar la hoja de estilos (main.css), la del codigo JavaScript, y la de los datos en crudo de las notas (data.json)._

_La pestaña Network también muestra la información enviada en el formulario:_

![form submit data](./img/23e.png)

_La etiqueta Form tiene como atributos **action** y **method**, que definen que el envio del formulario debe hacerse como una petición POST a la dirección `/new_notes`._

![form attr](./img/24e.png)

_El código en el servidor que responde a la petición POST es bastante simple (Nota: Este código esta en el servidor y no en el código JavaScript recuperado por el navegador):_

~~~
app.post('/new_note', (req, res) => {
  notes.push({
    content: req.body.note,
    date: new Date(),
  })

  return res.redirect('/notes')
})
~~~

_Los datos son enviados en el [body](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST)(cuerpo) de la petición POST._

_El servidor puede acceder a los datos accediendo al campo `req.body` del objeto de la solicitud `req`._

_El servidor crea un objeto para la nueva nota, y lo agrega al array llamado `notes`._

~~~
notes.push({
  content: req.body.note,
  date: new Date(),
})
~~~

_El objeto Note tiene dos campos: **content** que contiene el contenido actual de la nota, y **date** que contiene la fecha y la hora en la cual la nota fue creada._

_El servidor no graba la nueva nota en una base de datos, solamente se guarda en espacio de memoria, por lo que al reiniciar el servidor las nuevas notas agregadas desaparecerán._



### 🔹🔹🔹 AJAX 🔹🔹🔹

_La página Notas de la aplicación sigue un estilo noventoso de desarrollo web y "utiliza AJAX". Como tal, estuvo en la cresta de la ola de la tecnología web de principios de los 2000._

_AJAX (Asynchronous JavaScript and XML), o JavaScript y XML asíncrono, es un termino introducido en febrero del 2005 gracias a los avances en las tecnologías de los navegadores para describir un nuevo enfoque revolucionario que permitió la búsqueda de contenido en páginas web utilizando JavaScript incluido dentro del HTML, sin la necesidad de volver a recargar la página._

_Antes de esto, todas las páginas funcionaban como la aplicación web tradicional vista anteriormente en este capítulo. Todos los datos que se muestran en la página se obtuvieron con el código HTML generado por el servidor._

_La pagina Notas utiliza AJAX para recuperar los datos de las notas. El envio del formulario utiliza el mecanismo tradicional._

_Las URLs de la aplicación son un claro reflejo de los viejos tiempos sin preocupaciones. Los datos JSON son recuperados directamente de la url `https://fullstack-exampleapp.herokuapp.com/data.json` y las nuevas notas son enviadas a la URL `https://fullstack-exampleapp.herokuapp.com/new_note`._
_Hoy en dia URLs como estas no son concideradas aceptables, ya que no siguen las conveciones de las APIs [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer#Applied_to_Web_services), que se veran en profundidad en la parte 3._

_Lo que se denomina AJAX ahora es tan común que se da por sentado, y así el termino se desvanecio en el olvido y la nueva generación ni siquiera escuchó hablar de esto._



### 🔹🔹🔹 SPA o aplicación de una página 🔹🔹🔹

_En la app de ejemplo, la página de inicio trabaja como una página web tradicional: Toda la lógica esta en el servidor, y el navegador solo renderiza el HTML como se le indica._

_La página de notas le da algo de responsabilidad al navegador al generar el codigo HTML para cada nota existente. Esta tarea la realiza ejecutando el código JavaScript que obtuvo del servidor. El código recupera las notas del servidor como datos JSON y agrega elementos HTML para mostrar las notas en la página utilizando la [DOM-API](#-dom-o-modelo-de-objetos-del-documento-)._

_En los últimos años ha surgido el estilo de aplicaciones de una sola página (SPA) para crear aplicaciones web. Los sitios web de estilo SPA no  obtienen todas sus paginas por separado del servidor como lo hace la aplicacion de muestra vista anteriormente, sino que consisten en una página HTML obtenida del servidor, cuyo contenido se manipula con JavaScript que se ejecuta en el navegador (ésta pagina HTML le indica al navegar que debe obtener éste codigo JavaScript que va a manipular la página)._

_La página de Notas de la aplicación vista tiene algo de parecido con las aplicaciones de estilo SPA, pero todavia no esta del todo lista. Aunque la lógica para renderizar las notas esta corriendo en el navegador, la página todavia usa la manera tradicional de agregar las notas nuevas. Los datos son enviados al servidor con un submit (envio) del formulario, y el servidor le dice al navegador que recargue la página Notas con un redireccionamiento._

_Vamos un ejemplo de como sería una versión SPA de la aplicación de ejemplo. A primera vista, la aplicación se ve exactamente como la anterior. El codigo HTML es casi idéntico, pero el archivo JavaScript es diferente (spa.js) y hay un pequeño cambio in como la etiqueta **form** es definida:_

![spa form](./img/25e.png)

_El formulario no tiene atributos **action** o **method** para definir como y a dónde son enviados los datos ingresados._

_Sí abrimos la pestaña Network, la limpiamos con el símbolo 🚫 y creamos una nueva nota, al enviarla vemos que el navegador realiza solo una petición al servidor._

![spa send form](./img/26e.png)

_La petición POST a la dirección `/new_note_spa` contiene la nueva nota como datos JSON con los campos **content**, que tiene el contenido de la nota, y **date** con la fecha:_

~~~
{
  content: "single page app does not reload the whole page",
  date: "2021-03-30T15:15:59.905Z"
}
~~~

_El header (encabezado) Content-Type de la petición le dice al servidor que los datos incluidos estan representados con un formato JSON._

![spa request headers](./img/27e.png)

_Sin este encabezado, el servidor podría no saber cómo analizar (parsear) correctamente los datos._

_El servidor responde con un status code [201 created](https://httpstatuses.com/201), indicando que la nota fue creada correctamente. Esta vez el servidor no le dice al navegador que redireccione y este se mantiene en la misma página, y no envía mas solicitudes HTTP._

_La versión SPA de la aplicación no envia los datos del formulario de la manera tradicional, sino que utiliza el codigo JavaScript que recuperó del servidor. Miremos un poco este código JavaScript, aunque entenderlo al detalle no es importante ahora._

~~~
var form = document.getElementById('notes_form')
form.onsubmit = function(e) {
  e.preventDefault()

  var note = {
    content: e.target.elements[0].value,
    date: new Date(),
  }

  notes.push(note)
  e.target.elements[0].value = ''
  redrawNotes()
  sendToServer(note)
}
~~~

_La instrucción `document.getElementById('notes_form')` recupera el elemento form que tenia el id `notes_form` y luego le registra un controlador de eventos (event handler) para manejar los eventos del envío de formulario. Este controlador de eventos, que es una función, lo primero que hace es llamar al método `e.preventDefault()`, que es un método del objeto evento (comunmente nombrado con la letra `e`), que evita el manejo por defecto que tiene el envío del formulario. Este método por defecto lo que haría es enviar los datos al servidor y causar una nueva solicitud GET que ahora no queremos que pase._

_Luego el controlador de eventos crea una nueva nota en la variable `note` y luego la agrega al array `notes` cone el metodo push con la instrucción `notes.push(note)`, rerenderizando la lista de notas en la página con la función `redrawNotes()` y enviando la nota al servidor con la función `sendToServer(note)`._

_El código de la función `sendToServer` sería el siguiente:_

~~~
var sendToServer = function(note) {
  var xhttpForPost = new XMLHttpRequest()
  // ...

  xhttpForPost.open('POST', '/new_note_spa', true)
  xhttpForPost.setRequestHeader(
    'Content-type', 'application/json'
  )
  xhttpForPost.send(JSON.stringify(note))
}
~~~

_El código determina que los datos son enviados con una petición HTTP POST y que el tipo de datos es JSON. Como vimos anteriormente el tipo de datos es indicado en el encabezado `Content-Type`. Luego estos datos son eviados como una cadena de texto tipo JSON convertidos con el método `JSON.stringify()`._

_El código de la aplicación esta disponible en `https://github.com/szuviria/app-ejemplo`. Es importante aclarar que **la aplicación solo esta destinada solo a demostrar los conceptos del curso**. El código sigue un estilo de desarrollo deficiente en cierta medida y debe de usarse de ejemplo al crear sus propias aplicaciones. Lo mismo pasa con las URLs utilizadas. La URL `new_note_spa`, a donde son enviadas las nuevas notas, **no corresponde a buenas prácticas**._



### 🔹🔹🔹 Librerías de JavaScript 🔹🔹🔹

_La aplicación de ejemplo esta hecha con lo que se llama [vanilla JavaScript](https://medium.freecodecamp.org/is-vanilla-javascript-worth-learning-absolutely-c2c67140ac34), utilizando solo la DOM-API y JavaScript para manipular la estructura de las páginas._

_En lugar de usar JavaScript y la DOM-API solamente, existen diferentes librerías que contienen herramientas que facilitan el trabajo al manipular páginas en comparación con la DOM-API. Una de estas librerías que es muy popular es [JQuery](https://jquery.com/)._

_JQuery fue desarrollada cuando las aplicaciones web seguían principalmente el estilo tradicional donde el servidor generaba las páginas HTML, cuya funcionabilidad se mejoró del lado del navegador usando JavaScript escrito con JQuery. Una de las razones del éxtio de JQuery fue la compatibilidad entre navegadores. La librería funcionaba independientemente del navegador o de la empresa que lo fabricaba, por lo que no había necesidad de soluciones específicas para el navegador. Hoy en día el uso de Jquery no está justificado con los avances que tuvo VanillaJS, ya que los navegadores más populares generalmente soportan muy bien las funcionalidades básicas._

_El auge que tuvieron las SPAs trajo formas más "modernas" del desarrollo web que JQuery. La favorita en un principio fue [BackboneJS](http://backbonejs.org/). Luego de su [lanzamiento](https://github.com/angular/angular.js/blob/master/CHANGELOG.md#100-temporal-domination-2012-06-13) en 2012, [AngularJS](https://angularjs.org/) de Google se convirtió rapidamente casi en el estandar de facto del desarrollo web moderno._

_Sin embargo, la popularidad de Angular de desplomó después de que anunciaran en octubre del 2014 que el soporte para la version 1 se terminaría, y Angular 2 no sería retrocompatible con la primera versión. Angular 2 y las versiones más nuevas no han sido bien recibidas._

_Actualmente la herramienta mas populares para implementar la lógica del lado del navegador en el desarrollo de aplicaciones web es la librería de Facebook, [React](https://reactjs.org/). Durante éste curso, trataremos con React y la librería [Redux](https://github.com/reactjs/redux), que son utilizadas frecuentemente en conjunto._

_El estado de React pare bastante sólido, pero el mundo de JavaScript está cambiando constantemente. Por ejemplo, recientemente ha llegado [VueJS](https://vuejs.org/) que ha despertado cierto interés._

### 🔹🔹🔹 Desarrollo web full stack 🔹🔹🔹

_Qué significa Desarrollo web full stack (Full stack web development)? Full stack es una ppalabra de moda de la que todos hablan pero que nadie sabe muy bien que significa. O al menos, no existe una definición acordada para el término._

_Practicamente todas las aplicaciones web tiene dos "capas": El navegador, que está mas cerca del usuario, lo que sería la capa superior, y la del servidor la inferior. A menudo también hay una capa de base de datos debajo del servidor. Por eso, podemos pensar en la arquitectura de una aplicación web como una especie de pila (stack) de capas._

_Frecuentemente también se habla sobre el [frontend](https://en.wikipedia.org/wiki/Front_and_back_ends) y el [backend](https://en.wikipedia.org/wiki/Front_and_back_ends). El navegador es el frontend, y JavaScript que corre en el navegador es el código frontend. El servidor por el otro lado es el backend._

_En el contexto de éste curso, el desarrollo web full stack significa que haremos foco en todas las partes de la aplicacion: el frontend,el backend, y la base de datos. A veces, el software en el servidor y su sistema operativo son vista como parte del stack, pero no meteremos ahí._

_Escribiremos el código del backend con JavaScript, usando el entorno de ejecución [Node.js](https://nodejs.org/en/). El uso del mismo lenguaje de programación en multiples capas del stack le da al desarrollo web una dimensión completamente nueva y para quién está empezando le facilita mucho las cosas. Sin embargo, no es un requisito del desarrollo web full stack utilizar el mismo lenguaje de programación (JavaScript) para todas las capas del stack._

_Lo común era que los desarrolladores se especializaran en una capa del stack, por ejemplo, el backend. Las tecnologías en el backend y en el frontend son bastante diferentes. Con esta tendencia Full Stack, se ha vuelto común que los desarrolladores dominen todas las capas de la aplicación y la base de datos. A menudo, los desarrolladores full stack tambien deben tener suficientes habilidades de configuración y administración para operar su aplicación, por ejemplo, en la nube._



