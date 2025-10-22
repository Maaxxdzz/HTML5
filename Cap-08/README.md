# CAPITULO 8

## El manifiesto del caché

Esto es una lista de todos los recursos que una pagina web llegue a necesitar para poderlos usar fuera de línea, para indicarlo se debe colocar dentro de la etiqueta `<html>`

```html
    <!DOCTYPE html>
    <html manifest="/cache.appcache">
        <body>
            ...
        </body>
    </html>
```

El manifiesto puede ubicarse en cualquier parte del servidor web , aunque debe colocarse con el tipo de contenido `text/cache-manifest`

El manifiesto se divide en 3 partes:
*   La sección "*explicita*" = `/clock.css`
*   La sección "*de reserva*" = `/clock.js`
*   La sección "*lista blanca en linea*" = `/clock-face.jpg`

Este no posee encabezados de sección,así que los recursos se encuentran en la sección "*explicita*" de forma predeterminada, los cuales se almacenaran en "*caché*" localmente, así cuando se desconecte de la red ,todos los recursos se cargaran del "*caché*".

### Secciones de la red

En ocasiones como realizar un seguimiento de los visitantes por medio de un "*script*" no debería almacenarse en "*caché*" ya que perdería completamente su sentido de funcionalidad , por lo tanto se coloca de otra manera , por ejemplo:

    Cache Manifest
        NETWORK:
            /tracking.cgi
        CACHE:
            /clock.css
            /clock.js
            /clock-face.jpg
            
Esto indica que lo que este dentro de "*Network*" nunca se almacenaran dentro del "*caché*" y no estarán disponibles sin conexión.

### Secciones de respaldo

Aquí se puede definir cosas que sustituyan a los objetos en linea , los cuales no se puedan almacenar en "*caché*",ejemplo:

    CACHE MANIFEST
        FALLBACK:
            / /offline.html
        NETWORK:
        *

Esto lo que hace es que algunos elementos de las paginas estén disponibles sin conexión.

Funcionan agregando o creando un "*appcache*" dependiendo el caso , si la pagina aun no es conocida esta lo creara , en cambio si ya es conocida , solamente lo añadirá.

Dentro del ejemplo, especificamente en `/ /offline.html`

No es una "*URL*" en cambio es un patrón de "*URL*" el carácter (`/`) buscara cualquier coincidencia dentro del *cache* de aplicaciones , en caso de no encontrar alguna página este mostrara la pagina `/offline.html`

Dentro del ejemplo , especificamente en `Network: *`

El `*` es un comodín que significa "*online whitelist wildcart flag*" , este lo que quiere decir es que cualquier cosa que no se encuentre en la *cache de aplicaciones* de puede descargar de la dirección web original.

## El flujo de los eventos

El flujo de eventos inicia cuando el navegador visita una página y esta apunta a un manifiesto de *cache* activa unos eventos dentro del evento `window.applicationCache`.

El evento se activa independientemente de si se ha visitado la página o no ,activara el evento de descarga ,al mismo tiempo el navegador activara eventos de progreso, los cuales contienen información acerca de cuantos archivos hay en cola de descarga y cuantos ya se han descargado.

Al final el navegador manda un evento final `catched` siendo esta la señal que informa que ya toda la pagina web esta almacenada en *cache* y ya puede usarse de modo "*offline*".

En el caso de que el navegador conozca la pagina y ya tenga información almacenada en *cache* ,este manda una señal para verificar si algo ha cambiado , en el caso de que no haya cambiado nada ,este devolverá el evento `noupdate`.

En el caso de que sea "si" y haya cambiado la pagina desde la ultima vez que entro a la página ,el navegador comenzara a descargar denuevo los nuevos recursos que haya en la página, al finalizar este proceso , disparara el evento `updateready`

Para realizar un cambio a la nueva versión sin la necesidad de recargar la página se puede llamar a la función `window.applicationCache.swapCache().`

## El delicado arte de depurar errores

La manera de que el navegador comprueba si un archivo del manifiesto del *cache* , es un proceso de 3 fases:

1.  A través de HTTP normal comprobara si el manifiesto de *cache* ha expirado.
1.  Si ha expirado ,el navegador preguntara al servidor si hay una nueva versión, y en caso de que si , este la descargara.
1.  Si el servidor web cree que el archivo de manifiesto ha cambiado desde esa fecha, devolverá un código de estado `HTTP 200 (OK)`,una vez ya descargado ,este lo comprara con la ultima versión que se tenia descargada.


Algo que se necesita hacer sin falta es reconfigurar tu servidor web para que tu archivo de manifiesto de caché no se pueda almacenar en caché mediante la semántica HTTP, en caso de que se este ejecutando en un servidor de "*Apache*" ,estas lineas en el archivo `.htaccess` harán el trabajo:

    ExpiresActive On
    ExpiresDefault "access"
    
Esto desactivara el almacenamiento en *cache* para ese directorio y todos los subdirectorios, en el caso de que el archivo de manifiesto de *cache* no cambiara en nada ,el navegador nunca notara el cambio en alguno de los recursos almacenados,ejemplo:

    CACHE MANIFEST
    # rev 42
    clock.js
    clock.css
    
Cada que se realize un cambio en alguno de los recursos de la aplicación web,se deberá cambiar el archivo de manifiesto de *cache*, como en el ejemplo , solamente cambian el numero dentro de la linea de `# rev 42`.

    CACHE MANIFEST
    # rev 43
    clock.js
    clock.css