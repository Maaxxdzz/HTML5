# Capitulo 3

## The DOCTYPE

Debido al problema que hubo cuando los navegadores se mejoraron causando que las páginas se mostrarán incorrectamente ,siendo así que Microsoft pensó que antes que se mostrara la página se mirara el ***DOCTYPE***  el cual suele ser la primera linea del código 

Esto se esparció rápido y ahora los navegadores tenían 2 modos los cuales eran:
* **Quirks mode**
* **Standards mode**

Aun así presentaban problemas con el modo estándar así que se creo el modo **"Almost Standards Mode"**

    <!DOCTYPE html
          PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN"
          "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
Este es un ejemplo de 1 de los 15 "***DOCTYPE***" que se usaban en el modo estándar , aunque también se puede usar el `<!DOCTYPE html5>` el cual ya activa el modo estándar.

## The root element
Las páginas de HTML son elementos en conjunto semejante a un árbol puede haber elementos hermanos e hijos y existe un principal al cual se le denomina padre y el elemento antecesor de todos se le llama elemento raíz, 
en el caso de HTML5 seria la etiqueta `<html>`.

Ejemplo:
    
    <html xmlns="http://www.w3.org/1999/xhtml">

El atributo xmlns es un vestigio de XHTML 1.0 sin embargo ya no es necesario declararlo explícitamente sin causar algún inconveniente.

Existen los atributos "***xml:lang***" y "***lang***" realizan a misma función ,y contienen el mismo valor.


## El elemento `<head>`

Este elemento contiene meta-datos y suele ser el primer sucesor de la etiqueta raíz ,elemento `<body>` el el cual contiene el cuerpo de la página web.

La etiqueta `<head>` puede contener distintos tipos de etiqueta como:
* *meta*
* *title*
* *head*

## Codificación de los caracteres
El texto esta compuesto por *"bits y bytes"* , el ***"Character encoding"*** es en el cual se almacenan cada texto que se imprime en la pantalla.

El navegador lo determina gracias al "***header***" en tipo HTTP, ejemplo:
       
    Content-Type: text/html; charset="utf-8"
    
    
**"HTML 4 proporcionó una forma de especificar la codificación de caracteres en el propio documento HTML."**(Pilgrim,S.F,Cap. 3),la cual es:

    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    
En **HTML5** toda esa etiqueta fue reducida para su uso en todos los navegadores a tan solo:
    
    <meta charset="uft-8" />

## Amigos y relaciones (*Links*)

La etiqueta `<a>` sirve como un apuntador a otra página 

Existen 2 tipos de "*link*" los cuales son:
* Link para archivos externos:
    
        Ejemplo:
        <link rel="stylesheet" type="text/css" href="style-original.css" />
        
* Link de hipervínculos

        Ejemplo:
        <link rel="shortcut icon" href="/favicon.ico" />
        
Generalmente la etiqueta `<link>` generalmente se encuentran en la etiqueta `<head>` sin embargo en raras ocasiones se pueden encontrar en las etiquetas `<a>` aunque es raro el caso.

### rel = Stylesheet
   
  Es la mas común y la mas usada, esta se utiliza para señalar hoja de estilo CSS las cuales se encuentran en otro archivo.
  
  `<link rel="stylesheet" href="styles.css">`
  
### rel= alternate

Este se puede combinar con los atributos  **RSS** o **Atom** en el *"type"*
el cual permite que algunos lectores como ***Google Reader*** descubran el tipo de contenido que tiene el documento

Se puede usar para describir el tipo de feed usando distintos atributos por ejemplo:

    type=application/atom+xml
    Indica que texto es de tipo Atom
    
## Otras relaciones de enlaces en HTML5

`<link rel="author">`
Es usada para dar información del autor.

`<link rel="external">`
Es usada para indicar que el documento no es parte del sitio donde se encuentra el usuario.

`<link rel="first">`
Indica que la página va en serie

`<link rel="license">`
Se usa para indicar las licencias de copyright

`<link rel="notfollow">`
Indica que el enlace o documento debido a una relación comercial

`<link rel="noreferrer">` 
Indica que no se filtrara algún tipo de dato al seguir al enlace

`<link rel="pingback">`
 Hace que cuando enlacen el sitio web a otro , este notifica automáticamente que se realizo el enlace , notifica a los autores de las páginas que su página fue enlazada con otra


`<link rel="search">`
Este sirve para búsquedas dentro de documentos y para ser útil debe apuntar a algún documento de "***OpenSearch***"

## Nuevos elementos semánticos en HTML5

`<section>` Sirve para clasificar los datos y elementos de una página, ya sean introducciones,títulos, objetos , datos de contacto.

`<nav>` Es un apartado donde se coloca una barra de navegación para otras páginas o partes de la misma página.

`<article>` Sirve para una publicación en un foro , algún articulo de revista o comentarios hechos por usuarios.

`<aside>` Sirve para indicar que es una barra que estará en una lateral del contenido central

`<header>` Contiene el titulo de la sección, generalmente en etiquetas tipo h1-h6.

`<footer>` Se coloca al final de la página y se colocan *links* y/o información del autor , sobre la página   

## Como los navegadores manejan los elementos desconocidos
Cuando los navegadores encuentran elementos que desconocen suele haber problemas con el "*DOM*" y no respetan la sintaxis que da HTML5 

Como por ejemplo:
    
    Así lo envía
    HTML5
    article
    |
    +--h1 (child of article)
    |      |
    |      +--text node "Welcome to Initech"
    |
    +--p (child of article, sibling of h1)
       |
       +--text node "This is your "
       |
       +--span
       |  |
       |  +--text node "first day"
       |
       +--text node "."
     
    Así lo crea el navegador cuando detecta algún elemento desconocido:
     
    article (no children)
    h1 (sibling of article)
    |
    +--text node "Welcome to Initech"
    p (sibling of h1)
    |
    +--text node "This is your "
    |
    +--span
    |  |
    |  +--text node "first day"
    |
    +--text node "."
    
Una solución para este problema es creando el elemento con JS  antes de usarlo dentro de la pagina , y así el elemento sera reconocido por el navegador

`<script>document.createElement("article");</script>`

## HEADERS
Dentro de este es recomendable usar elementos  `<h1>` y `<h2>` para darle estructura a la pagina 

`<h1>` -  `<h6>` Son elementos de bloque dentro de ellos ,hay un orden especifico , y ese orden es dependiente a su numero , entre menor sea el numero,mas arriba estará en la jerarquía.

El elemento `<hgroup>` soluciono la problemática que había en HTML4 el cual existía un nodo fantasma el cual se robaba los elemento secundarios del nodo raíz.

Con este elemento solo se crea un único nodo en el esquema dentro del documento

## Articles
Este crea nuevas secciones , un nodo en el esquema del documento y cada seccion que se crea puede tener diferentes elementos 

    <article>
    <p class="post-date">October 22, 2009</p>
    <h2>
        <a href="#"
         rel="bookmark"
         title="link to this post">
        Travel day
     </a>
    </h2>
     …
    </article>
    
    
Anteriormente en HTML4 solo se podian crear esquemas de los documentos con etiquetas `<h1>-<h6>`,esto causaba que solo hubiera un nodo raíz ,ahora con este elemento ya es posible crear distintos nodos con distintas raíces

## Navegación
La navegación en una pagina web debe ser sencilla ya que pueden existir diversas dificultades con la cuales las personas no puedan interactuar de una manera correcta con la pagina.

Así que se puede usar un complemento del navegador como por ejemplo:
* Lectores de pantalla
* Texto a voz

Dentro de HTML5 nos permite marcar las seccions de navegacion con la etiqueta `<nav>`

    <nav>
      <ul>
        <li><a href="#">home</a></li>
        <li><a href="#">blog</a></li>
        <li><a href="#">gallery</a></li>
        <li><a href="#">about</a></li>
      </ul>
    </nav>
    
## Footers
Suele ser la ultima cosa en la página ,suele contener información acerca de la pagina web ,datos generales,existen los "**Fat footers**" el cual se compone por 3 columnas

    <footer>
     <div class="w3c_footer-nav">
       <h3>Navigation</h3>
       <ul>
         <li><a href="/">Home</a></li> 
         <li><a href="/standards/">Standards</a></li> 
         <li><a href="/participate/">Participate</a></li> 
         <li><a href="/Consortium/membership">Membership</a></li> 
         <li><a href="/Consortium/">About W3C</a></li> 
       </ul>
     </div>
     <div class="w3c_footer-nav">
       <h3>Contact W3C</h3>
       <ul>
         <li><a href="/Consortium/contact">Contact</a></li> 
         <li><a href="/Help/">Help and FAQ</a></li> 
         <li><a href="/Consortium/sup">Donate</a></li> 
         <li><a href="/Consortium/siteindex">Site Map</a></li> 
       </ul>
     </div>
     <div class="w3c_footer-nav">
       <h3>W3C Updates</h3>
       <ul>
         <li><a href="http://twitter.com/W3C">Twitter</a></li>
         <li><a href="http://identi.ca/w3c">Identi.ca</a></li>
       </ul>
     </div>
     <p class="copyright">Copyright © 2009 W3C</p>
    </footer>
    
# Fin