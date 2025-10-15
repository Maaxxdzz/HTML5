# Capitulo 07

## Breve historia de los trucos de almacenamiento local antes de HTML5

Microsoft creo Internet Explorer , y con el fue creando diversas cosas ,como por ejemplo "*DHTML Behaviors*"  y "*userData*".

* **userData**: permite que las paginas web almacenen como máximo 64 KB de información por cada dominio (**Los dominios de confianza pueden almacenar hasta 10 veces esa cantidad**).

Las "*Flash cookies*" fueron una función en flash 6 ,sin embargo su nombre correcto es "*Local Shared Objects*", esto permiten almacenar hasta 100 KB de información por dominio.

"*Gears*" fue lanzado y creado por Google® ,con el objetivo de dar una serie de capacidades extras a los navegadores ,ademas que permite almacenar una cantidad ilimitada de datos por dominio en tablas de bases de datos SQL.

Debido a que estos y algunos otros presentaban el mismo problema "*todas sus especificaciones eran para un único navegador y todas presentaban interfaces diferentes*" así que como solución se tomo crear un "*API*" estandarizado implementada de forma nativa ,con la finalidad de ya no depender de terceros.

## Introduciendo al almacenamiento de HTML5

"*HTML5 Storage*" es el medio por el cual se almacenan en pares de  valores y llaves nombrados localmente, generalmente estos datos continúan almacenados una vez que se salga del sitio web , lo que lo diferencia de las "*cookies*" es que nunca son transmitidas a un servidor remoto ,es decir nunca salen del ordenador.

Versiones de navegadores que soportan "*HTML5 Storage*"

<table>
    <thead>
        <tr>
            <th>
                IE
            </th>
            <th>
                FIREFOX
            </th>
            <th>
                SAFARI
            </th>
            <th>
                CHROME
            </th>
            <th>
                OPERA
            </th>
            <th>
                IPHONE
            </th>
            <th>
                ANDROID
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                8.0+
            </td>
            <td>
                3.5+
            </td>
            <td>
                4.0+
            </td>
            <td>
                4.0+
            </td>
            <td>
                10.5+
            </td>
            <td>
                2.0+
            </td>
            <td>
                2.0+
            </td>
        </tr>
    </tbody>
</table>

Con JS accederás al "*HTML5 Storage*" con el objeto de "*localStorage*" aun así se debe detectar si el navegador lo soporta.

##### Ejemplo:
```javascript
    function support_html5_storage(){
        try{
            return 'localStorage' in window && window['localStorage'] !== null;
        }catch(e){
            return false;
        }
    }
```

## Usando *HTML5 Storage*

Se basa en pares de claves y valores con algún nombre ,los datos pueden ser de cualquier tipo siempre y cuando sean compatibles con JS ,sin embargo los datos almacenados son de tipo "*String*" ,en ese caso será necesario usar funciones para convertirlos a tipo "*String*" como por ejemplo `parseInt()` en caso de datos tipo `Int`

##### Ejemplo de código 
```javascript
    interface Storage {
        getter any getItem(in DOMString key);
        setter creator void setItem(in DOMString key, in any data);
    };
```
* **setItem**: Si es llamado con un nombre clave que ya existe ,este sobrescribirá el valor anterior.

* **getItem**: Si es llamado con un nombre clave que no existe devolverá un valor nulo.

Se puede usar un "*array*" en vez de utilizar los 2 métodos anteriores.

##### Por ejemplo

```javascript
    var foo = localStorage.getItem("bar");
    // ...
    localStorage.setItem("bar", foo);
```

A su vez existen métodos para eliminar todos los valores y claves a la vez.

##### Ejemplo
```javascript
    interface Storage {
        deleter void removeItem(in DOMString key);
        void clear;
    };
```

Si se llama a `removeItem()` sin que exista la llave no hará nada.

De igual manera existe una propiedad para para poder obtener el numero total de valores dentro del área de almacenamiento 

##### Ejemplo

```javascript
    interface Storage {
        readonly attribute unsigned long lenght;
        getter DOMString key(in unsigned long index);
    };
```

## Rastreando cambios dentro de "*HTML5 Storage Data*"

Cada que se realiza un cambio queda un historial de cada cambio realizado.

Para enganchar el evento del almacenamiento se debe verificar que mecanismo admite el navegador , aquí un ejemplo de como hacerlo:

```javascript
    if(window.addEventListener){
        window.addEventListener("storage", handle_storage,false);
    }else{
        window.attachEvent("onstorage",handle_storage);
    };
```

La función de devolución *"handle_strogare"* va a almacenar el objeto se almacena en `window.event`

```javascript
    function handle_storage(e) {
        if (!e) { e = window.event; }
    }
```

La variable "*e*" tendrá las siguientes propiedades.

<table>
    <thead>
        <tr>
            <th>
                PROPERTY
            </th>
            <th>
                TYPE
            </th>
            <th>
                DESCRIPTION
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                key
            </td>
            <td>
                string
            </td>
            <td>
                the named key that was added ,removed , or modified
            </td>
        </tr>
        <tr>
            <td>
                oldValue
            </td>
            <td>
                any
            </td>
            <td>
                the previous value (now overwritten), or <b>null</b> if a new item was added
            </td>
        </tr>
        <tr>
            <td>
                newValue
            </td>
            <td>
                any
            </td>
            <td>
                the new value, or <b>null</b> if an item was removed
            </td>
        </tr>
        <tr>
            <td>
                url
            </td>
            <td>
                string
            </td>
            <td>
                the page which called a method that triggered this change
            </td>
        </tr>
    </tbody>
</table>

El evento de almacenamiento no es cancelable , no hay forma de evitar que se produzca el cambio.

## Limitaciones en navegadores actuales
Este tiene algunas limitaciones ,las respuestas con su orden de importancia a estas limitaciones son :
1.   **5 megabytes**
1.   **QUOTA_EXCEEDED_ERR**
1.   **no**

"*5 megabytes*" es la cantidad de espacio de almacenamiento que se tiene de forma predeterminada , y cada valor se almacenan en cadenas y no en su formato original.

"*QUOTA_EXCEEDED_ERR*" es la alerta que lanzara si se excede el almacenamiento de "*5 megabytes*" 

"*no*" es la respuesta a la pregunta que se hacia la cual era "**¿Puedo pedirle al usuario mas almacenamiento?**" ya que cuando se escribió el libro ,ningún navegador permitía solicitar mas espacio de almacenamiento al usuario.


## HTML5 Storage en acción
Con el almacenamiento se puede guardar algunos elementos dentro del propio navegador 

Usando el ejemplo realizado por mi para este resumen del capitulo:

##### Cada vez que se realiza un cambio se llama a esta función
    
```javascript
   function cargarcolor(){
                const carga = localStorage.getItem("Colorcito");
                if(carga){
                    const canva = document.getElementById('canva');
                    const contexto = canva.getContext("2d");
                    contexto.fillStyle = carga;
                    contexto.fillRect(0, 0, 500, 500);
                }else{
                    alert("Error en el guardado");
                }
            }     
```    

Aquí se utiliza el "*localStorage*" con esta se guarda el color con el cual se quedo la ultima vez antes de refrescar la pestaña ,ya obtenido el color se carga directamente al contexto del valor "*canva*".

Existe de igual manera la posibilidad de preguntarle al usuario si es que quiere cargar el ultimo color que le apareció de la siguiente manera:
 
##### Se agrega el botón:
```HTML
    <button 
        onclick="cargarcolor()"
        class="btn"
    >
        Cargar ultimo color
    </button>
```
Aquí solo se agrega el botón y se añade el evento del "*onclick*" dentro del mismo, en el cual se llama a la función al momento que el usuario da "*click*"

>Nota:
>El ejemplo completo se encuentra dentro de este mismo repositorio dentro de la carpeta src con el nombre de "index.html"


## Más allá de los pares Key-Value con nombre: visiones en competencia

Cuando Google® lanzo "*Gears*" este incluía una base de datos integrada en "*SQLite*" ,este dio pie a la creación de bases de datos "*Web SQL*",4 navegadores fueron los que implementaron estas especificaciones de bases de datos.

<table>
    <thead>
        <tr>
            <th>
                IE
            </th>
            <th>
                FIREFOX
            </th>
            <th>
                SAFARI
            </th>
            <th>
                CHROME
            </th>
            <th>
                OPERA
            </th>
            <th>
                IPHONE
            </th>
            <th>
                ANDROID
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                -
            </td>
            <td>
                -
            </td>
            <td>
                4.0+
            </td>
            <td>
                4.0+
            </td>
            <td>
                10.5+
            </td>
            <td>
                3.0+
            </td>
            <td>
                2.0+
            </td>
        </tr>
    </tbody>
</table>


La "*API de bases de datos*" expone lo que es un almacén de objetos,comparte muchos conceptos con una base de datos SQL ,los cambios dentro del almacén de objetos se manejan como "*transacciones*".