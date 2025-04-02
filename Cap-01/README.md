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

- **Tony Johnson**, quien sugirió una etiqueta `<ICON>` con un parámetro `NAME` para permitir imágenes integradas.
- **Tim Berners-Lee**, creador de la web, propuso usar `<A>` con relaciones específicas (`EMBED`, `PRESENT`).

Sin embargo, estas ideas no fueron implementadas debido a su complejidad o falta de flexibilidad.

Finalmente, **Marc Andreessen** revisó las diferentes propuestas y tomó la decisión de usar `<IMG SRC="url">`. Marc explicó:

> No estamos preparados para soportar INCLUDE/EMBED en este punto... Así que probablemente optemos por `<IMG SRC="url">` (no ICON, ya que no todas las imágenes incrustadas pueden llamarse íconos). Por ahora, las imágenes incrustadas no tendrán un tipo de contenido explícito; en el futuro planeamos soportarlo (junto con la adaptación general de MIME).

Así, con la etiqueta `<img>`, podemos agregar imágenes de manera sencilla a nuestros proyectos.




