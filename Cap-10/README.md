# "Distribuido" "Extensibilidad" y otras palabras elegantes

## ¿Qué son los microdatos?

Estos se centran en vocabularios personalizados, por ejemplo "El conjunto de todos los elementos de HTML5".

Este incluye elementos para representar una sección o un articulo ,en cambio no incluye elementos para representar a una persona o un evento.

Para hacer eso ,debes definir tu propio vocabulario , y los "*microdatos*" sirven para eso, para incorporar propiedades personalizadas a la web.

Estos funcionan por medio de "*name/value*", para incluir una propiedad de microdatos específica en su página web, proporciona el nombre de la propiedad en un lugar específico.

Los microdatos dependen de su "alcance" , y su manera mas sencilla de saber su alcance , es pensar en la relación padre-hijo de los elementos en el "*DOM*" por ejemplo:

```html
    <html> //Elemento padre
        <head> //Elemento hijo
        </head>
        <body> //Elemento hijo
        </body>
    </html>
```
Los microdatos utilizan la organización del mismo "*DOM*", así para facilitar y poder usar mas de un vocabulario de microdatos en la misma página.

>No están diseñados para ser un elemento independiente , son un complemento de HTML.
  
Suelen ajustar excelentemente los datos que ya se encuentran en el "*DOM*".

## El modelo de microdatos

Para definir un vocabulario propio de microdatos, se necesita "*namespace*" , lo que es igual a una "*URL*".

##### EJEMPLO DEL LIBRO:
    
    Situación:
        Crear un vocabulario de microdatos que describa a una persona.
    
    Forma de resolver:
        Soy dueño de del dominio data-vocabulary.org , por lo tanto 
        usare la URL: 
            http://data-vocabulary.org/Person
Esa es la forma fácil de crear un identificador único global.

El nombre es una propiedad de microdatos (como por ejemplo nombre) el cual siempre se declara en un elemento HTML , en la mayoría de los elementos ,su valor es simplemente el contenido del texto del elemento.

##### Tabla de ejemplo de excepciones de valores
<style>
table tr td {
    border: 2px solid white;
}
.src-attribute  td {
    background:darkblue;
}
.href-attribute td{
    background:darkred;
}
</style>
<table>
    <thead>
        <tr>
            <th>
                Element
            </th>
            <th>
                Value
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                <code>
                    &lt;meta&gt;
                </code>
            </td>
            <td>
                <code>
                    content attribute
                </code>
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;audio&gt;
                </code>
            </td>
            <td>
                src attribute
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;embed&gt;
                </code>
            </td>
            <td>
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;iframe&gt;
                </code>
            </td>
            <td>
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;img&gt;
                </code>
            </td>
            <td>
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;source&gt;
                </code>
            </td>
            <td>
            </td>
        </tr>
        <tr class="src-attribute">
            <td>
                <code>
                    &lt;video&gt;
                </code>
            </td>
            <td>
            </td>
        </tr>
        <tr class="href-attribute">
            <td>
                <code>
                    &lt;a&gt;
                </code>
            </td>
            <td>
                href attribute
            </td>
        </tr>
        <tr class="href-attribute">
            <td>
               <code>
                    &lt;area&gt;
               </code>
            </td>
            <td>
            
            </td>
        </tr>
        <tr class="href-attribute">
            <td>
               <code>
                    &lt;link&gt;
               </code>
            </td>
            <td>
            
            </td>
        </tr>
        <tr>
            <td>
               <code>
                    &lt;object&gt;
               </code>
            </td>
            <td>
                data attribute
            </td>
        </tr>
        <tr>
            <td>
               <code>
                    &lt;time&gt;
               </code>
            </td>
            <td>
                datetime attribute
            </td>
        </tr>
        <tr>
            <td>
                all other elements
            </td>
            <td>
                text content    
            </td>
        </tr>
    </tbody>
</table>

Para agregar microdatos debes de agregar algunos atributos a los elementos HTML, se pueden seguir estos pasos:
*   Usando "**itemtype**" se declara que vocabulario de datos se esta usando.
*   Y usando "**itemscope**" se declara el alcance del vocabulario.

##### Ejemplo:
```html
    <section
        itemscope
        itemtype="http://data-vocabulary.org/Person"
    >
    </section>
```

Dentro del apartado creado por las etiquetas `<section>` tu nombre es el primer *bit* de datos el cual esta dentro de un elemento `<h1>` , y este no tiene algún procesamiento especial y se le trata igual de que a todos los demás elementos.

>NOTA: Funcionaria de igual manera si estuviera dentro de un elemento `<p>,<div> o <span>`

##### Ejemplo
```html
   <h1 itemprop="name">Mark Pilgrim</h1> 
```

Lo que se quiere decir con esa línea, es que aquí esta la propiedad del vocabulario "*[URL]*" y el valor de la propiedad es: *[Texto dentro de la etiqueta]*.

Las propiedades de las fotos son "*URL's*" y su elemento HTML es `<img>` , su valor es el elemento `src`, es necesario declarar que ese elemento es de la propiedad "*photo*"
###### Ejemplo:
```html
    <p>
        <img
            itemprop="photo"
            src="http://www.example.com/photo.jpg"
        >
    </p>
```
Ese pequeño código indica que el valor de la propiedad es "`http://www.example.com/photo.jpg`".

De igual manera existe la propiedad "*url*", y esta se emplea en el elemento `<a>` y su valor es su atributo "*href*" , y tan solo se debe indicar que el elemento `<a>` es la propiedad "*url*".

##### Ejemplo:
```html
    <a
        itemprop = "url"
        href = "http://diveintomark.org/"
    >
        Dive into mark
    </a>
```
Aquí indica que la propiedad de la "*url*" es `http://diveintomark.org/`.

Los "*Markups*" se puede colocar en diferentes presentaciones , tales como una tabla:
##### Ejemplo:
```html
    <table>
        <tr>
            <td>
                Name
            </td>
            <td>
                Mark Pilgrim
            </td>
        </tr>
        <tr>
            <td>
                Link
            </td>
            <td>
                <a 
                    href="#" 
                    onclick="goExternalLink()"
                >
                    http://diveintomark.org
                </a>
            </td>
        </tr>
    </table>
```
En este caso basta tan solo con agregar el atributo "*itemdrop*" a la casilla donde se encuentre el valor:
#### Ejemplo:
```html
    <td itemdrop="name">
        Mark Pilgrim
    </td>
```

## Marcando a la gente (MARKING UP THE PEOPLE)

Los microdatos son generalmente usados en el apartado "*Sobre nosotros*" ya que es la manera mas fácil de integrarlos.

Lo primero que se tiene que hacer es declarar el vocabulario que se esta usando y su alcance que tienen las propiedades que se van a agregar.
##### Ejemplo:
```html
    
    <section 
        itemscope        //Declara el alcance
        itemtype="http://data-vocabulary.org/Person" //Declara el vocabulario a usar
    >
    </section>
```
Con el link de "`http://data-vocabulary.org/Person`" se puede comenzar a definir propiedades de microdatos , en el caso de que no conozca las propiedades, estas se pueden ver en la pagina solamente introduciendo el link en el navegador.

Solo es necesario definirlos una vez, colocando los atributos "*itemscope y itemtype*" en el contenedor más externo.

Esto apoya incluido a los estilos CSS ya que
si se tiene un "*itemtype*" distinto se puede dar estilos completamente diferentes, actuando cada contenedor del texto de manera independiente.

##### Ejemplo:
```html
    <dt>
        Position        
    </dt>
    <dd>
        <span itemprop="title">
            Developer advocate
        </span>
        <span itemprop="affiliation">
            Google, Inc.
        </span>
    </dd>
```
Igualmente con ese mismo link existen los microdatos para "Direcciones" y este define 5 propiedades:
1.  **street-address**:Dirección de calle
1.  **locality**:Localidad
1.  **region**:Region
1.  **postal-code**:Código Postal
1.  **country-name**:País

##### Ejemplo de uso:
```html
    <dd 
        itemprop="address" 
        itemscope
        itemtype="http://data-vocabulary.org/Address"
    >
        <span 
            itemprop="street-address"
        >
            100 Main Street
        </span>
        <br>
        <span 
            itemprop="locality">
                Anytown
        </span>,
        <span 
            itemprop="region">
                PA
        </span>
        <span itemprop="postal-code">
                19999
        </span>
        <span
            itemprop="country-name">
                USA
        </span>
    </dd>
```
Los elementos `<a>` tienen un procesamiento especial, ya que su valor de la propiedad de microdatos es el atributo "*href*" no en el contenido de texto secundario.

### Introduciendo a los fragmentos enriquecidos de Google (Google Rich Snippets)

Existen 2 aplicaciones principales que consumen HTML:
*   **Navegadores web**:Estos definen un conjunto de "*API DOM*" con la finalidad de extraer elementos , como los microdatos , propiedades y valores de las propiedades de una pagina web.
*   **Motores de búsqueda**: Hace que se pueda integrar la información tal como el *título*,*extractos de textos* y la pueda mostrar.

Google admite los microdatos dentro de su programa "*Rich Snippets*", estas leen y analizan la página y si encuentra propiedades con microdatos las almacena junto al resto de la pagina , además que existe una propiedad con la que se puede ver como Google "*visualiza*" las propiedades y se veria de la siguiente manera:
##### Ejemplo proporcionado por el libro:}
```plaintext
    Item
    Type : http://data-vocabulary.org/person
    name = Mark Pilgrim 
    title = Developer advocate 
    affiliation = Google, Inc. 
    address = Item( 1 ) 
    url = http://diveintomark.org/ 
    url = http://www.google.com/profiles/pilgrim 
    url = http://www.reddit.com/user/MarkPilgrim 
    url = http://www.twitter.com/diveintomark 
    
    Item 1
    Type: http://data-vocabulary.org/address
    street-address = 100 Main Street
    locality = Anytown
    region = PA
    postal-code = 19999
    country-name = USA
``` 
Su manera de uso esta a decisión de Google , ya que el es quien decide que valores mostrar y cuales no , podria mostrarlo de la siguiente manera:
##### Imagen de ejemplo del libro
<img 
    src="src/imagenes/imagen_ejemplo.png" 
    width="100%">
  
## Marcando Organizaciones

De igual manera se deben establecer los atributos ya antes mencionados en el elemento mas externo.

Y al igual que el vocabulario de "*Person*" tienen sus propiedades: 
<table>
    <thead>
        <tr>
            <th>
                Propiedad
            </th>
            <th>
                Descripción
            </th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>
                name
            </td>
            <td>
                Nombre de la organización.
            </td>
        </tr>
        <tr>
            <td>
                url
            </td>
            <td>
                Link de la pagina principal de la organización.
            </td>
        </tr>
        <tr>
            <td>
                address
            </td>
            <td>
                Dirección física de la organización.
            </td>
        </tr>
        <tr>
            <td>
                tel
            </td>
            <td>
                Numero telefónico de la organización.
            </td>
        </tr>
        <tr>
            <td>
                geo
            </td>
            <td>
                Especifica las coordenadas geográficas de la ubicación.
            </td>
        </tr>
    </tbody>
</table>

Su estructura es similar a la de "*Person*" ya que en el titulo se coloca la propiedad "*name*",y las direcciones se colocan en el respectivo contenedor donde se encuentren las direcciones.

En este caso existe la propiedad "*tel*" y esta se coloca donde se encuentre el numero de contacto.

> Nota:Con la propiedad tel se pueden colocar mas de un numero de contacto , es decir se puede repetir la propiedad.

Con "*url*" ocurre lo mismo que en "*Person*"(*Tiene un procesamiento especial debido a su valor*).

En este caso la geolocalización no es como el "*API*" , este no muestra como tal la latitud y longitud, como solución a esto existe una manera de anotar datos invisibles ,siendo que se usa como ultimo recurso ya que en ocasiones estos suelen ser olvidados y quedar obsoletos rápidamente.

Su ventaja son que se pueden colocar los datos invisibles inmediatamente después del texto que es visible.

##### Ejemplo de creación de un `<span>` invisible
```html
    <span 
        itemprop="geo" 
        itemscope
        itemtype="http://data-vocabulary.org/Geo"
    >
        <meta 
            itemprop="latitude" 
            content="37.4149" 
        />
        <meta 
            itemprop="longitude" 
            content="-122.078"
        />
    </span>
```
La geolocalización se define en su propio vocabulario , por lo tanto ocupa 3 atributos:
1.  **itemprop="geo"**:Indica que este elemento representa la propiedad geográfica de la organización. 
1.  **itemtype="[URL]"**:Indica que vocabulario de microdatos se ajustan a las propiedades de este elemento.
1.  **itemscope**:Indica que este es el elemento que encierra un grupo de microdatos con su propio vocabulario.

Los microdatos se anotan dentro de las etiquetas `<meta>`.

## Marcando Eventos
Los eventos de igual manera tienen su vocabulario con sus propiedades:

<img
    src="src/imagenes/tabla_event_vocabulary.png"
    >
En este caso el nombre del evento no se marca con "*name*" en cambio se marca con "*summary*".

Se incluye la propiedad "*description*" en la cual es solamente un párrafo con texto libre.

Lo mas resaltante es que se agregan las propiedades: 
*   **starDate**:Su valor debe ser cuando inicia el evento.
*   **endDate**:Su valor debe ser cuando termina el evento.
 
 Estas se deben colocar con el elemento `<time>`.
 
##  Marcando Reseñas

Para las reseñas existe su vocabulario con sus propiedades:

<img
    src="src/imagenes/tabla_review_vocabulary.png"
    >
    
En el caso de que se quiera marcar la fecha de la reseña y de usuario que reseño se debe colocar la fecha dentro de un elemento `<time>` y quien reseño dentro de un elemento `<span>`.

De igual manera al reseñar se deben colocar limites en la escala que se va a utilizar y para eso existe la propiedad "*rating*":
  
##### Ejemplo de uso:
```html
    <p 
        itemprop="rating" 
        itemscope
        itemtype="http://data-vocabulary.org/Rating"
    >
    ★★★★★★★★★☆
    <span 
        itemprop="value"
    >
        9
    </span> 
    on a scale of
    <span itemprop="worst">
        0
    </span> 
    to
    <span itemprop="best">
        10
    </span>
</p>
```

>   NOTA: El link de http://data-vocabulary.org ya ha cambiado por https://schema.org