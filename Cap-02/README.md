# CAPITULO 2  
## Compatibilidad
El capitulo nos indica que HTML 5 al ser una coleccion de caracteristicas individuales, por eso mismo no se puede _"detectar su compatibiliad"_ con los antiguos navegadores por que seria sin sentido, mas sin en cambio se puede buscar la compatibilidad con las diferentes caractersticas que forman HTML 5 como puede ser el **video** o la **geolocalizacion**, con las **tecnicas de deteccion** existen 4 tipos de tecmicas de deteccion las cuales son:  
1. Comprobar si existe una determinada propiedad en un objeto global _(como una "window" o un "navigator")_
2. Cree un elemento y, a continuación, compruebe si existe una determinada propiedad en ese elemento  
3. Cree un elemento, compruebe si existe un determinado método en ese elemento y, a continuación, llame al método y compruebe el valor que devuelve.
4. Cree un elemento, establezca una propiedad en un valor determinado y, a continuación, compruebe si la propiedad ha conservado su valor
 **Con esas tecnicas puedes detetar la compatibilidad del navegador**

## MODERNIZR
Modernizr es una biblioteca JavaScript de código abierto (licencia MIT) que detecta el soporte de múltiples características de HTML5 y CSS3; para ocuparla necesitamos poner este script al principio de nuestro archivo

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Mi página HTML5</title>
  <script src="modernizr.min.js"></script>
</head>
<body>
  ...
</body>
</html>

```
_Modernizr se ejecuta automáticamente. No hay ninguna función modernizr_init() a la que llamar. Cuando se ejecuta, crea un objeto global denominado Modernizr, que contiene un conjunto de propiedades booleanas para cada característica que puede detectar._

Además de facilitar la detección, permite añadir clases CSS al <html> para aplicar estilos condicionales. Su uso ahorra tiempo, evita errores y mejora la compatibilidad entre navegadores antiguos y modernos.


# CANVAS

El elemento `<canvas>` en HTML5 permite crear un área de dibujo dentro de una página web. Usando JavaScript, puedes dibujar gráficos, animaciones, juegos u otros elementos visuales en tiempo real. HTML5 proporciona una API (conjunto de funciones) que permite dibujar formas, líneas, aplicar colores, degradados y realizar transformaciones como rotaciones o escalados sobre el lienzo.

**¿Mi navegador es compatible con canvas?**  
Para saber eso tienes que usar la _tecnica de deteccion #2_ Esta técnica crea un elemento `<canvas>` con JavaScript, pero no lo muestra en la página. Luego revisa si ese elemento tiene una función llamada `getContext()`. Si la tiene, significa que el navegador sí soporta la API de canvas.

```js
function supports_canvas() {
  return !!document.createElement('canvas').getContext;
}
```
Esta funcion lo que hace es que crea un elemento `<canvas>` que **nunca** se añade a tu pagina, se crea solo en la memoria del navegador para poder rectificar que si se tiene la funcion`getContext()`, la funcion solo aparecera si tu navegador es compatible.  
**ESTA FUNCION DETECTA EL SOPORTE PARA LA MAYORIA DE `<canvas>`**
 
 ## CANVAS TEXT
 Aun cuando tu navegador pueda soportar `<canvas>` puede que no llegue a soportar _canvas text_ ya que Canvas API crecio con el tiempo pero las funciones de texto fueron añadidas despues de tiempo, es por eso que puede que Canvas text no sea compatible en tu navegador; Para saber si es compatible se ultiza la misma **_tecnica de deteccion #2_**, es parecido a lo que hicimos arriba pero cambia en unas cosas

 ```js
  function supports_canvas_text() {
 if (!supports_canvas()) { return false; }
 var dummy_canvas = document.createElement('canvas');
 var context = dummy_canvas.getContext('2d');
 return typeof context.fillText == 'function';
 }
 ```
La funcion comienza checando que tu navegador soporte el Canvas API ya que si no lo hace, muchos menos puede soportar Canvas text, pero al utilizar esta funcion nos ayuda a detectar sobre las dos API.

## VIDEO
**HTML5** definio un nuevo elemento llamado `<video>`, se utiliza como su nombre lo dice para poner videos en nuestra pagina web, la etiqueta esta diseñada para usarse sin ningun metodo de deteccion, antes tener un video era casi imposible si no tenias una otra aplicacion o plugin para hacerlo como _Apple QuickTime_ o _Adobe flash_

Se implementó una solución para manejar la compatibilidad con video HTML5 en distintos navegadores. Cuando el navegador soporta el elemento `<video>`, se utiliza video HTML5 de forma nativa. En caso contrario, se recurre automáticamente a alternativas como Flash o QuickTime, gracias a la técnica Video for Everybody!, que no requiere JavaScript y funciona incluso en navegadores móviles. Para detectar soporte de video, se utiliza una función que verifica la existencia del método `canPlayType()` o, de forma más robusta, la librería Modernizr, que permite actuar en consecuencia dependiendo de si hay soporte nativo o no.  

## VIDEO FORMATS
Los formatos de video funcionan como idiomas: aunque dos videos pueden tener el mismo contenido, si el navegador no "habla" el códec en que está codificado, no podrá reproducirlo. En HTML5, ese “idioma” es el códec, una combinación de algoritmos que codifican el video y el audio. Actualmente no hay un códec universalmente soportado, por lo que los navegadores modernos tienden a admitir al menos uno de tres: H.264 (compatible con Safari y dispositivos Apple, pero con licencias de patente), Ogg Theora (libre y apoyado por navegadores como Firefox) y WebM (abierto y respaldado por Chrome, Firefox y Opera).

Para saber qué formato puede reproducir el navegador, se usa el método `canPlayType()` en un elemento `<video>` dinámico, que devuelve "probably", "maybe" o una cadena vacía según el nivel de compatibilidad. Esta verificación se puede automatizar con funciones personalizadas para cada formato o usando Modernizr, que detecta soporte para los códecs más comunes de forma estructurada (Modernizr.video.h264, .ogg, .webm). Esto permite ofrecer una experiencia de video adaptable y compatible con una amplia variedad de entornos.


## LOCAL STORAGE
HTML5 local storage permite que los sitios web almacenen datos en el navegador del usuario de forma persistente, sin necesidad de enviarlos al servidor en cada solicitud, como ocurre con las cookies. A diferencia de estas, local storage está pensado para guardar mayores volúmenes de información y es accesible desde JavaScript una vez que la página ha cargado. Aunque originalmente formaba parte del estándar HTML5, fue separado en una especificación aparte por razones organizativas.

Para verificar si el navegador lo soporta, se puede comprobar si existe la propiedad `localStorage` en el objeto window, envolviendo la prueba en un bloque `try..catch` debido a fallos en versiones antiguas de Firefox cuando las cookies están deshabilitadas. Alternativamente, se puede usar Modernizr (v1.1 o superior), que ofrece una forma más sencilla de detectar compatibilidad (`Modernizr.localstorage`). Cada sitio solo puede acceder a los datos que él mismo ha guardado, gracias a la restricción de mismo origen, pero los datos pueden ser visibles si alguien accede físicamente al dispositivo del usuario.

El uso de local storage es ideal para guardar configuraciones del usuario, contenido en caché o estados de interfaz sin depender de servidores externos. Sin embargo, no debe utilizarse para almacenar información sensible, ya que los datos se guardan en texto plano y pueden ser accedidos por cualquier persona con acceso físico al dispositivo. Además, aunque cada sitio solo puede acceder a su propio almacenamiento, es responsabilidad del desarrollador implementar prácticas seguras y considerar los límites de almacenamiento que varían según el navegador.


## WEB WORKERS
Los Web Workers permiten ejecutar scripts en segundo plano, liberando el hilo principal del navegador. Así, se pueden realizar tareas complejas como cálculos o procesamiento de datos sin que la interfaz se congele o se vuelva lenta. Para detectar si son compatibles, basta con verificar si window.Worker existe. También puedes usar Modernizr.webworkers.

## OFFLINE WEB APPLICATIONS
Las aplicaciones web offline permiten acceder a contenido incluso cuando no hay conexión a internet. Esto es posible gracias al applicationCache o, más recientemente, mediante Service Workers. Aunque el applicationCache está obsoleto, en su momento se detectaba con window.applicationCache. Modernizr también provee Modernizr.applicationcache para facilitar esta verificación.

## GEOLOCATION
La geolocalización permite a una web conocer la ubicación aproximada o precisa del usuario. Esta función es útil en apps de mapas, recomendaciones locales o rastreo de entregas. Se detecta si navigator.geolocation está presente.

Cabe señalar que esta API requiere permiso explícito del usuario, y puede no estar disponible si el navegador está en modo privado o si se deniega el acceso. Aunque no es parte de HTML5 como tal, ha sido ampliamente adoptada junto con sus avances.

Además, hay alternativas de geolocalización que funcionaban antes del soporte nativo, como Google Gears, pero actualmente son obsoletas.

## INPUT TYPES
HTML5 amplía la variedad de tipos de campo en los formularios: email, tel, url, date, entre otros. Esto mejora tanto la validación automática como la experiencia del usuario, ya que se activan teclados contextuales en móviles o mensajes específicos al ingresar datos inválidos.

## PLACEHOLDER TEXT
El atributo placeholder muestra texto de guía dentro de un campo vacío. Es muy útil para indicar qué debe ingresar el usuario sin necesidad de etiquetas adicionales ni JavaScript. Se verifica fácilmente con 'placeholder' in inputElement, y Modernizr lo cubre con Modernizr.input.placeholder.

## FORM AUTOFOCUS
autofocus permite que un campo de formulario obtenga el foco automáticamente al cargar la página. Aunque parece menor, mejora la usabilidad en formularios rápidos, como búsquedas o inicios de sesión. Se detecta con 'autofocus' in input, o usando Modernizr.input.autofocus.

## MICRODATA
Microdata permite incrustar metadatos dentro del HTML para definir con más claridad qué representa el contenido. Por ejemplo, un nombre, una dirección o una fecha de evento.

Esto mejora cómo motores de búsqueda como Google interpretan la página. La detección de soporte se hace comprobando si document.getItems existe, ya que Modernizr no lo incluye directamente.










