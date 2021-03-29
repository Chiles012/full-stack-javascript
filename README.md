# Full Stack Javascript

_Este proyecto sirve como una introducción al desarrollo moderno de aplicacion web con JavaScript, donde el foco principal esta puesto en construir SPAs (single page applications) con ReactJS que utilicen APIs REST construidas con Node.js. En este proyecto tambien se agregará una sección sobre GraphQL, una alternativa moderna a APIs REST._

_Se cubrirá algo de testing, configuración y manejo de entorno, y el uso de MongoDB para persistir los datos de la aplicación._


## Indice:

**Parte 0: Fundametos de las aplicaciones Webs**
1. [Fundamentos de las aplicaciones Web](#fundamentos-de-las-aplicaciones-web)
    * [HTTP GET](#http-get)
    * [Aplicaciones web tradicionales](#aplicaciones-web-tradicionales)
    * [La lógica de la aplicación corriendo en el navegador](#la-logica-de-la-aplicacion-corriendo-en-el-navegador)

## Parte 0: Fundamentos de las aplicaciones Web

_En esta parte se desarrollarán los conceptos basicos del desarrollo web y se hablará de como evolucionó el desarrollo de aplicaciones web en las últimas décadas._

<div id="#fundamentos-apps-web" />

### Fundamentos de las aplicaciones Web

_A continuación podremos observar unas imágenes en las que servirán para demostrar conceptos básicos pero que no quieren decir que sean ejemplos de como las aplicaciones Web deben ser. Por el contrario, muestran viejas tecnicas de desarrollo web que pueden considerarse_ **malas practicas** _hoy en día._

_Durante todo el proyecto se estará utilizando el navegador Chrome._

**_La primera regla del desarrollo Web:_** _Siempre tener a la vista la Consola de Desarrollo abierta en tu navegador. En macOS, la consola se abre presionando `F12` o `option-cmd-i` simultaneamente. En Windows o Linux, la consola se abre presionando `F12` o `ctrl-shift-i` simultaneamente._

_La consola se ve de la siguiente manera:_

![consola](./img/part0/1e.png)

_Es recomendable,en la pestaña Network, tener marcada la opcion de deshabilitar el cache (Disable cache) como se muestra en la imagen, ya que de no hacerlo es muy probable que no veamos los cambios que realicemos a nuestro código. Preservar el log (Preserve log) puede ser muy util ya que guarda los logs ya mostrados por la aplicacion cuando la página es recargada._

**Nota:** _La pestaña mas importante es la **Consola**. Sin embargo, en esta introducción se estará utilizando bastante la pestaña **Network**._

#### HTTP GET

_El servidor y el navegador web se comunican uno con el otro mediante el protocolo [HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP). La pestaña Network muestra como se comunican el navegador y el servidor._

_Cuando la pagina es recargada (presionando `F5` o en el simbolo ↺ del navegador), la consola muestra que dos eventos han sucedido:_

* _El navegador recupera (fetch) el contenido de la pagina fullstack-exampleapp.herokuapp.com del servidor._

* _Y descarga la imagen kuva.png_

![fetches](./img/part0/2e.png)

_En una pantalla pequeña puede que se deba ampliar la ventana de la consola para verlo._

_Clickeando en el primer evento hará que se nos muestre mas informacioón sobre lo que está sucediendo.:_

![event](./img/part0/3e.png)

_La parte de arriba, General, muestra que el navegador hizo una petición (request) a la dirección https://fullstack-exampleapp.herokuapp.com usando el método GET, y que la petición fue exitosa, porque la respuesta del servidor tiene un [Status code](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) **200**._

_La petición y la respuesta del servidor tiene varios encabezados (headers):_

![headers](./img/part0/4e.png)

_Los response headers (encabezados de la respuesta) nos dicen, por ejemplo, el tamaño de la respuesta en bytes, y el tiempo exacto de la respuesta. Un encabezado importante es el [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) que nos dice que la respuesta es un archivo de texto en formato [utf-8](https://en.wikipedia.org/wiki/UTF-8), cuyo contenido ha sido formateado en HTML. De esta manera el navegador sabe que la respuesta es una pagina [HTML](https://en.wikipedia.org/wiki/HTML), y que debe renderizarlo en el navegador 'como una pagina web'._

_La pestaña Response (respuesta) muestra los datos de la respuesta, una página HTML normal. La sección **body** determina la estructura de la página renderizada en la pantalla:_

![headers](./img/part0/5e.png)

_La página contiene un elemento [div](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/div), que dentro contiene un heading (encabezado), un link a una página notes, y un tag [img](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img), y muestra el número de notas creadas._

_Debido al tag img, el navegador realiza una segunda petición HTTP para recuperar la imagen kuva.png de el servidor. El detalle de la petición es el siguiente:_

![img tag](./img/part0/6e.png)

_La petición se realizó a la dirección https://fullstack-exampleapp.herokuapp.com/kuva.png y su tipo es HTTP GET. El encabezado de la respuesta nos dice que el tamaño de la respuesta es de 89350 bytes, y su [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) es image/png, asi que es una imagen png. El navegador usa esta información para renderizar la imagen correctamente en la pantalla._

_La cadena de eventos causada por abrir la página https://fullstack-exampleapp.herokuapp.com en el navegador genera el siguiente [diagrama de secuencia](https://www.geeksforgeeks.org/unified-modeling-language-uml-sequence-diagrams/):_

![secuence diagram](./img/part0/7e.png)

_Primero, el navegador hace una solicitud HTTP GET al servidor para recuperar el codigo HTML de la pagina. El tag img en el HMTL le indica al navegador que debe recuperar la imagen kuva.png. El navegador renderiza la pagina HTML y la imagen en la pantalla._

_Aunque es dificil de notar, la página HTML comienza a renderizarse antes de que la imagen sea recuperada del servidor._

#### Aplicaciones web tradicionales

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

#### La lógica de la aplicación corriendo en el navegador

_La siguiente imagen corresponde a la página notes, el navegador realiza cuatro solicitudes HTTP:_

![pagina notes](./img/part0/8e.png)

_Todas las solicitudes tienen **diferentes tipos**. El tipo de la primer solicitud es **document**. Es el codigo HTML de la pagina, y se ve de la siguiente manera:_

![first request](./img/part0/9e.png)

_Cuando comparamos la página mostrada en el navegador y el código HTML devuelto por el servidor, notamos que el codigo no contiene la lista de notas. La sección [head](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/head) contiene un tag [script](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script), que hace que el navegador recupere un archivo JavaScript llamado main.js._

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

_Inmediatamente después de recuperar el tag **script**, el navegador ejecuta el código._

_Las últimas dos lineas definen que el navegador hace una solicitud HTTP GET a la dirección del servidor /data.json:_

~~~
xhttp.open('GET', '/data.json', true)
xhttp.send()
~~~

_Esta es la solicitud es la mostrada al final de la lista en la pestaña Network._

![data.json](./img/part0/10e.png)

_Acá encontramos las notas en JSON como datos sin procesar. Por defecto, el navegador no es bueno mostrando datos JSON. Se puede utilizar plugins para manejar el formateo. Se puede instalar, por ejemplo, [JSONView](https://chrome.google.com/webstore/detail/jsonview/chklaanhfefbnpoihckbnefhakgolnmc) en Chrome, y al recargar la página, los datos se mostrarán bien formateados:_

![formatted json](./img/part0/11e.png)

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

_El código primero crea una lista no ordenada con el tag [ul](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/ul)..._

~~~
var ul = document.createElement('ul')
ul.setAttribute('class', 'notes')
~~~

_...y luego cada nota es agregada a un tag [li](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/li). Solo el valor **content** de cada nota se convierte en el contenido de el tag li. Los datos de las fechas no son utilizados en ningún lugar aquí._

~~~
data.forEach(function(note) {
  var li = document.createElement('li')

  ul.appendChild(li)
  li.appendChild(document.createTextNode(note.content))
})
~~~

_Ahora abrimos la pestaña Console en la consola de desarrollo:_

![console](./img/part0/12e.png)

_Clickeando en el pequeño triángulo al comienzo de la linea, se puede expandir el texto en al consola._

![expand console](./img/part0/13e.png)

_La salida de la consola es causada por el comando `console.log` en el código:_

~~~
const data = JSON.parse(this.responseText)
console.log(data)
~~~

_Así, cuando se reciben los datos del servidor, el código lo muestra en la consola._

_La pestaña Console y el comando `console.log` se convertiran en algo muy familiar durante el curso._