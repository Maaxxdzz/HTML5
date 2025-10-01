# CAPITULO #1  
Este capitulo me fue enseñando poco a poco sobre la historia de HTML 5, y sobre los primeros creadores de paginas web, tambien sus diferentes funcionalidades de este mismo, asi como cuando accedes a una página web, esta envía un **'Header'** a tu navegador, permitiéndole interpretar y mostrar correctamente el contenido. Estos **'Header'** fueron incorporados en 1994 por el World Wide Web Consortium (W3C).

# MIME TYPES  

### ¿Qué son los MIME Types?  
Los **MIME types** (Multipurpose Internet Mail Extensions) son encabezados HTTP que indican al navegador cómo interpretar un recurso web. Son esenciales para que los navegadores rendericen correctamente páginas web, imágenes, scripts, videos y otros tipos de contenido.

## Ejemplos Comunes  
- **HTML**: `text/html`  
- **Imágenes**: `image/jpeg`, `image/png`  
- **JavaScript**: `application/javascript`  
- **CSS**: `text/css`  

## Importancia en la Web  
1. **Determinan el comportamiento del navegador**: El encabezado `Content-Type` es el único factor que define cómo se procesará un recurso.  
2. **Compatibilidad histórica**: En los inicios de la web (1993), los servidores no enviaban este encabezado, lo que llevó a prácticas como el "content sniffing".  
3. **Estándar moderno**: Hoy en día, todos los recursos deben incluir un MIME type correcto para garantizar una interpretación adecuada.  

## Relación con HTML5  
Entender los MIME types es fundamental para comprender la evolución de estándares web como HTML5. Este estándar fue diseñado considerando tanto la compatibilidad con tecnologías antiguas como la retroalimentación de implementaciones modernas.  


# El Origen de la Etiqueta `<img>`

En los primeros días de la web, cuando podías contar los servidores web con ambas manos, surgió la necesidad de incrustar imágenes en documentos HTML. Esto ocurrió antes de la existencia del **World Wide Web Consortium (W3C)**.

Existieron muchas propuestas para la creación de la etiqueta `<img>`, unas mejores que otras. Entre ellas destacaron:

- **Tony Johnson**, quien sugirió una etiqueta `<icon>` con un parámetro `name` para permitir imágenes integradas.
- **Tim Berners-Lee**, creador de la web, propuso usar `<a>` con relaciones específicas (`embed`, `present`).

Sin embargo, estas ideas no fueron implementadas debido a su complejidad o falta de flexibilidad.

Al final, **Marc Andreessen** revisó las diferentes propuestas y tomó la decisión de usar `<img src="url">`. Marc explicó:

> No estamos preparados para soportar INCLUDE/EMBED en este punto... Así que probablemente optemos por `<img src="url">` (no ICON, ya que no todas las imágenes incrustadas pueden llamarse íconos). Por ahora, las imágenes incrustadas no tendrán un tipo de contenido explícito; en el futuro planeamos soportarlo (junto con la adaptación general de MIME).

Así, con la etiqueta `<img>`, podemos agregar imágenes de manera sencilla a nuestros proyectos.


`HTML no fue creado en un laboratorio perfecto, sino a través de una conversación caótica entre desarrolladores, fabricantes de navegadores y otros entusiastas. A pesar de sus imperfecciones, ha evolucionado constantemente porque alguien siempre lanzó código que funcionaba. El caso del <img> es emblemático: Marc Andreessen lo implementó sin esperar estándares perfectos, y aunque su solución tenía fallos, fue el que "lanzó" y ganó. Al final, los estándares web triunfan cuando se mezcla innovación práctica con la capacidad de adaptarse al mundo real, no cuando se persigue la pureza teórica.`


# ¿Cómo llegamos al XHTML?
En diciembre de 1997, el W3C lanzó HTML 4.0 y, justo después, cerró el grupo de trabajo que lo desarrollaba. Poco tiempo más tarde, salió XML 1.0, lo que dio pie a un taller titulado “Shaping the Future of HTML”, donde básicamente se preguntaron: ¿el W3C ya no le va a dar más cariño al HTML?

La conclusión fue que HTML 4.0 ya no se podía seguir estirando y que convertirlo a XML era un lío. Entonces dijeron: “¿y si mejor empezamos de cero con HTML, pero como si fuera XML?”

Así nació XHTML 1.0 en 1998. Era como HTML 4.0 pero reescrito con reglas de XML. Permitía seguir usándolo como HTML de toda la vida (gracias a un “Apéndice C”) para que los navegadores viejos no explotaran.

Luego se metieron con los formularios y propusieron algo nuevo: XHTML Extended Forms, que después se renombró a XForms. Esta vez dijeron: “olvidémonos de la compatibilidad con lo viejo, hagámoslo bien desde el principio.”

Finalmente, en 2001 sacaron XHTML 1.1, una versión más estricta que ya no permitía seguir sirviendo páginas como text/html, sino que exigía el tipo MIME application/xhtml+xml. Ya era XHTML de verdad, sin atajos, pero... todo lo que sabes sobre **XHTML ESTA MAL**

### Todo lo que sabes sobre XHTML está mal

- HTML es *tolerante con errores* (olvidás cerrar etiquetas y no pasa nada).
- XHTML real (servido como `application/xhtml+xml`) **no perdona**: un solo error y la página **no se muestra**.
- El W3C quería mejorar la calidad del código con manejo draconiano de errores (como XML).
- XHTML 1.0 permitió una trampa: usar sintaxis XML pero servirla como `text/html`.
- XHTML 1.1 y 2.0 **eliminaron ese atajo** → solo funcionan si servís con el tipo MIME correcto.
- Hoy, millones de páginas dicen ser XHTML… pero si no usan `application/xhtml+xml`, **no lo son**.

> Si no sabés qué tipo MIME usás, casi seguro es `text/html`.

#  Una visión alternativa: nace WHATWG

- En 2004, Mozilla y Opera propusieron **evolucionar HTML 4** para apoyar aplicaciones web modernas.
- Su enfoque se basaba en 7 principios clave:
  1. Compatibilidad con HTML/CSS/JS existentes (como IE6).
  2. Manejo de errores detallado y predecible.
  3. Los usuarios no deben ver errores.
  4. Solo agregar funciones con uso práctico real.
  5. Scripting sí, pero mejor si se puede usar marcado.
  6. Las funciones deben funcionar igual en móvil y escritorio.
  7. Desarrollo abierto y público.

- El W3C **rechazó apoyar esta idea** (votación 11 contra 8).
- En respuesta, nació **WHATWG** (junio 2004), un grupo independiente para seguir desarrollando HTML de forma más abierta y práctica.



> 💡 En lugar de eliminar la compatibilidad hacia atrás, el WHAT Working Group trabajó para que **HTML siga siendo compatible** con contenido existente.

#  **De vuelta al W3C**

- **2006**: Después de años de trabajo paralelo, el **WHAT Working Group** había ganado impulso, mientras que **XHTML 2** seguía sin implementarse. 
- **Tim Berners-Lee**, fundador del W3C, anunció que el W3C trabajaría con el WHAT Working Group para evolucionar **HTML**.
- **Evolución incremental**: Se reconoció que **HTML debe evolucionar gradualmente**, en lugar de forzar cambios drásticos como el paso a XML.
- El nuevo grupo de trabajo del W3C se centraría en mejoras incrementales para **HTML y XHTML** y en extender **HTML Forms** con las ideas de Webforms.
- El **nuevo nombre para "Web Applications 1.0"** fue **HTML5**.

` 💡 En resumen: La transición hacia **HTML5** se hizo posible gracias al trabajo colaborativo entre el W3C y el WHAT Working Group.`








