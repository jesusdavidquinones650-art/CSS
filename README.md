# CSS
# Taller de CSS: Jerarquía, Especificidad y Modelo de Caja

Este repositorio contiene el desarrollo de las subactividades 1 y 2 del taller de CSS. El proyecto consistió en construir un catálogo de productos semántico y aplicar los conceptos fundamentales de estilos, desde la herencia hasta la configuración espacial de las cajas.

---

## Subactividad 1: Jerarquía de Estilos

El objetivo principal fue entender cómo el navegador aplica los estilos mediante la **herencia**, la **cascada** y la **especificidad**, además de estructurar correctamente el HTML.

### Conceptos aplicados:
*   **Herencia:** Se configuró la tipografía (`font-family`) y el color base en la etiqueta `body`. Todos los textos (títulos, párrafos, listas) heredaron estos valores automáticamente.
*   **Selectores combinados:** Para pintar los enlaces dependiendo de su ubicación sin afectar a los demás, se usaron reglas como `header nav ul li a` (azul), `aside ul li a` (verde) y `footer ul li a` (morado).
*   **Cálculo de especificidad:** El navegador le da un peso a cada selector:
    *   Etiqueta = 1 punto
    *   Clase = 10 puntos
    *   ID = 100 puntos

### El conflicto y la refactorización
Inicialmente, en el HTML un botón de compra tenía la clase `btn-comprar` y el ID `btn-destacado`. En el CSS, aunque la regla de la clase estaba escrita más abajo (cascada), el navegador aplicó el color del ID porque tenía mayor peso (100 pts vs 10 pts).

Para estandarizar el código y evitar malas prácticas, se **refactorizó** el código:
1. Se eliminó el `#btn-destacado` del HTML y del CSS.
2. Se agregó la clase `destacado` a la etiqueta (`class="btn-comprar destacado"`).
3. Se utilizó el selector `.btn-comprar.destacado` (20 pts) para lograr el mismo estilo visual sin usar IDs ni la regla `!important`.

---

## Subactividad 2: Anatomía Espacial (Modelo de Caja)

El objetivo fue dejar de ver el HTML como textos flotantes y entenderlo como cajas rectangulares, aplicando espacios internos y externos, y decorando los fondos.

### Acciones realizadas:
*   Se aplicó la regla universal `* { box-sizing: border-box; }` para garantizar que el `padding` y los bordes crezcan hacia adentro y no rompan la estructura de los contenedores.
*   Se asignaron colores de fondo diferentes a `<header>`, `<main>`, `<aside>` y `<footer>` para delimitar las "supercajas" de la interfaz.
*   Se aplicó un `padding: 20px` a los `<article>` (oxígeno interno para que el texto no toque los bordes).
*   Se aplicó un `margin: 15px` a los `<article>` (campo de fuerza externo para empujar las tarjetas y evitar que choquen).
*   Se decoró el `<header>` con una imagen de fondo desde CSS (`background-image`), asegurando que cubra el espacio (`background-size: cover`) y esté centrada (`background-position: center`).

### Hallazgos: El Modelo de Caja
1.  **Diferencia entre Margin y Padding:** El `padding` es el espacio interno (separa el contenido del borde de la propia caja). El `margin` es el espacio externo (aleja nuestra caja de las demás cajas vecinas).
2.  **Importancia de `box-sizing: border-box`:** Sin esta regla, si a una caja de 100% de ancho le agregamos padding, la caja se desborda de la pantalla porque el navegador suma el ancho + el padding. Con `border-box`, el navegador respeta el tamaño original y calcula el padding hacia adentro.
3.  **Efecto del margen en elementos hermanos:** Cuando a un artículo se le aplica un margen grande, este empuja a los artículos de arriba y de abajo, creando una separación visual que impide que las tarjetas se vean amontonadas.

---
## Subactividad 3: El Puente Lógico (Variables CSS)
*   Se creó una "central de mando" usando la pseudoclase `:root` para declarar **Tokens de Diseño**.
*   Se crearon variables para colores (`--color-primario`, `--color-texto`, etc.), tipografía (`--fuente-principal`) y medidas de espaciado (`--espacio-xs`, `--espacio-md`, `--espacio-lg`).
*   Se reemplazaron todos los valores "quemados" (hardcoded) del CSS por la función `var()`. 
*   **Beneficio:** Si el cliente pide cambiar la paleta de colores o la separación de los productos, ahora solo se modifica la variable en `:root` y toda la interfaz se actualiza automáticamente sin riesgo de dejar espacios desiguales.

## Subactividad 4: Programar la interactividad y decoración visual

El objetivo de esta fase fue darle vida al catálogo aplicando microinteracciones y decoraciones virtuales. Se utilizaron pseudoclases para reaccionar a los eventos del usuario (como el cursor o el teclado) y pseudoelementos para inyectar detalles visuales desde el CSS, manteniendo el HTML limpio y semántico.

### Acciones realizadas:
*   **Menú lateral (`<aside>`):** Se aplicó `:hover` a los enlaces de filtrado para cambiar su fondo y texto suavemente. Se inyectó un punto decorativo antes de cada categoría usando `::before { content: "• "; }`. Además, se añadió la pseudoclase `:focus` con un `outline` visible usando las variables del `:root` para mejorar la accesibilidad.
*   **Catálogo de productos (`<main>`):** Se aplicó `:hover` (cambio de color) y `:active` (efecto de hundimiento con `transform: scale()`) a los botones de compra. Se utilizó el pseudoelemento `::after` en el contenedor `<article>` para inyectar una insignia virtual con la palabra "¡Oferta!", usando los colores definidos en las variables globales.
*   **Auditoría:** Se inspeccionaron los estados en las DevTools del navegador para verificar cómo se inyectan los bloques `::before` y `::after` en el DOM virtual.

### Hallazgos: Pseudoclases y Pseudoelementos

1.  **Diferencia funcional entre una pseudoclase y un pseudoelemento:**
    La pseudoclase (como `:hover` o `:focus`) se utiliza para definir el **estado** de un elemento cuando el usuario interactúa con él. El pseudoelemento (como `::before` o `::after`) se utiliza para **inyectar contenido decorativo** en el DOM virtual (como texto, iconos o formas) sin necesidad de agregar etiquetas HTML reales.
2.  **Importancia técnica de la pseudoclase `:focus` para la accesibilidad:**
    Es fundamental porque permite que las personas que navegan usando el teclado (presionando la tecla Tab) sepan exactamente en qué enlace o botón se encuentran ubicados. Un contorno visible (`outline`) garantiza que la web sea inclusiva y fácil de usar para todos, cumpliendo con las buenas prácticas de accesibilidad web.
3.  **¿Por qué es buena práctica inyectar elementos decorativos desde CSS en lugar de ensuciar el HTML?**
    Porque mantiene la separación de responsabilidades (HTML para estructura, CSS para diseño). Si mañana la etiqueta "¡Oferta!" cambia de diseño, de color o decide quitarse, solo se modifica el CSS sin tener que alterar el documento HTML. Además, si un usuario con un lector de pantalla accede al sitio, el CSS puede ignorar el contenido decorativo, evitando que el lector lea cosas sin sentido (como "viñeta" o "oferta") interrumpiendo la experiencia.



## Subactividad 5: Refactorizar la arquitectura (Modularidad y BEM)

El objetivo de esta fase fue dejar de tener un archivo CSS monolítico y desordenado, para pasar a una arquitectura escalable, predecible y lista para el trabajo en equipo, aplicando el estándar de nomenclatura BEM (Block, Element, Modifier) y dividiendo los estilos en módulos.

### Acciones realizadas:
*   Se creó la carpeta `css/` para alojar los módulos independientes de los componentes repetitivos: `botones.css` y `tarjetas.css`.
*   Se conectaron estos módulos al archivo maestro `estilos.css` utilizando la regla `@import` al inicio del documento.
*   Se reescribió el HTML aplicando nomenclatura BEM estricta, eliminando clases genéricas propensas a colisiones (ej. de `.img-producto` a `.card__image`, o de `.btn-comprar` a `.btn`).
*   Se implementaron modificadores semánticos (usando doble guion medio `--`) para variaciones visuales, como `.card--destacada` y `.btn--destacado`.
*   Se actualizaron los selectores en los nuevos archivos CSS, aplanando la especificidad y reemplazando los selectores anidados antiguos por clases BEM directas, manteniendo el uso de las variables globales del `:root`.

### Hallazgos: Arquitectura BEM y Modularidad

1.  **¿Qué significa la sigla BEM y cómo se escribe visualmente?**
    BEM significa **Block, Element, Modifier** (Bloque, Elemento, Modificador). Visualmente se escribe utilizando doble guion bajo (`__`) para separar los elementos del bloque, y doble guion medio (`--`) para denotar los modificadores. Por ejemplo: `.card` (bloque), `.card__title` (elemento) y `.card--destacada` (modificador).
2.  **¿Por qué dividir el CSS en varios archivos facilita el trabajo colaborativo?**
    Porque permite que varios desarrolladores trabajen simultáneamente en diferentes partes del diseño (ej. uno en botones, otro en tarjetas) sin generar conflictos en Git ni pisarse el código. Además, hace que el proyecto sea mucho más fácil de leer, depurar y escalar, ya que si se daña un botón, sabemos exactamente en qué archivo buscar y no en una hoja de miles de líneas.
3.  **¿Cómo esta metodología evita la guerra de especificidad (Cascada) al mantener un peso plano?**
    Porque BEM prohíbe el uso de selectores anidados profundos (como `.main article h2`). Al usar una única clase plana por regla (ej. `.card__title`), la especificidad se mantiene siempre baja y predecible (peso 10). Esto significa que ninguna regla "pisa" a otra por accidente debido a la jerarquía del HTML, y los modificadores (como `--destacada`) se aplican de forma limpia sin necesidad de usar `!important`.

S## Subactividad 6: Construir layouts unidimensionales modernos (Flexbox)

El objetivo de esta fase fue dar el salto a un diseño elástico y profesional utilizando Flexbox. Se reemplazó el uso de `inline-block`, `floats` y posiciones absolutas por un sistema de distribución flexible (ejes y gravedad), logrando que la interfaz se adapte a diferentes tamaños de pantalla y que los componentes se alineen milimétricamente.

### Acciones realizadas:
*   **Macro-arquitectura (Layout Global):** Se creó el contenedor `.app-layout` con `display: flex; flex-direction: column; min-height: 100vh;` para estructurar la página. A su vez, se creó `.main-wrapper` con `display: flex; flex: 1;` para colocar el menú lateral y el catálogo lado a lado, absorbiendo el espacio central.
*   **Cabecera (`.header`):** Se aplicó `display: flex; justify-content: space-between; align-items: center;` para separar el logo y el menú. A la lista de navegación (`.header__list`) se le aplicó `display: flex; gap: var(--espacio-md);` para alinear los enlaces horizontalmente sin usar márgenes.
*   **Panel lateral (`.sidebar`):** Se aplicó `display: flex; flex-direction: column; gap: var(--espacio-lg);` para distribuir los filtros verticalmente con espacios perfectos.
*   **Pie de página (`.footer`):** Se aplicó `display: flex; justify-content: space-around; align-items: center;` para repartir los elementos (textos y enlaces) equitativamente en la zona inferior.
*   **Tarjetas de producto (`.card`):** Se aplicó `display: flex; flex-direction: column; height: 100%;` para garantizar que todas las tarjetas midan exactamente lo mismo. Al contenedor del texto (`.card__body`) se le aplicó `flex-grow: 1;` para empujar el botón de compra hacia el fondo. Finalmente, al contenedor de precios (`.card__price-wrapper`) se le aplicó un micro-flexbox (`justify-content: space-between; align-items: baseline;`) para alinear el precio de oferta y el precio tachado.
*   **Catálogo (`.catalog`):** Se aplicó `display: flex; flex-wrap: wrap; justify-content: center; gap: var(--espacio-md);` para permitir que las tarjetas salten de línea en pantallas pequeñas de forma automática (diseño responsive).

### Hallazgos: Arquitectura Total con Flexbox

1. **¿Por qué fue crucial aplicar `min-height: 100vh` y `flex-direction: column` al contenedor global para controlar el pie de página?**
   Porque esto garantiza que la página siempre ocupe como mínimo el 100% del alto de la pantalla del usuario, sin importar si hay mucho o poco contenido. Al usar `flex-direction: column` en el `.app-layout`, los elementos se apilan verticalmente. Luego, al darle `flex: 1` al `.main-wrapper`, este actúa como un resorte que absorbe todo el espacio sobrante. El resultado es que el footer siempre queda anclado milimétricamente al fondo de la ventana y nunca flota en la mitad de la pantalla (conocido como *sticky footer*).

2. **¿Cómo la propiedad `gap` reemplazó el uso excesivo de márgenes laterales en los menús de navegación?**
   Antes, para separar los enlaces (como los del header o el aside), teníamos que usar `margin-right` o `margin-bottom` en cada elemento hijo. Eso ensuciaba el código y a veces generaba un margen extra no deseado en el último elemento. Con `gap`, ahora el contenedor padre es el único que se encarga de calcular el espacio exacto entre los elementos. Esto hace que el código sea mucho más limpio, fácil de modificar y garantiza una separación perfecta y simétrica.

3. **¿Cómo la unión de BEM, Custom Properties y Flexbox te permitió crear una tarjeta de producto resistente a diferentes longitudes de texto?**
   * **BEM** nos dio nombres de clases claros y predecibles (como `.card__body`) que no chocan con otros elementos.
   * **Custom Properties** (variables) mantuvieron los colores y espacios unificados y fáciles de cambiar.
   * **Flexbox** resolvió el problema del tamaño variable: al aplicar `display: flex; flex-direction: column` a la tarjeta y `flex-grow: 1` a su cuerpo de texto (`.card__body`), logramos que, sin importar si el título o la descripción son cortos o largos, el texto siempre ocupe el espacio disponible y empuje el botón de "Comprar" hacia el borde inferior. Así, todas las tarjetas mantienen la misma altura y los botones quedan perfectamente alineados en fila.

## Comandos de Git Utilizados

Para respaldar el avance técnico de ambas subactividades, se ejecutaron los siguientes comandos en la terminal:

```bash
# Subactividad 1
git add .
git commit -m "feat(styles): maquetar catalogo semantico y aplicar jerarquia CSS"
git push origin develop

# Subactividad 2 (en una nueva rama)
git checkout -b feature/modelo-caja
git add .
git commit -m "feat(ui): implementar modelo de caja y backgrounds"
git push origin feature/modelo-caja

# Subactividad 3
git checkout -b feature/variables-css
git add .
git commit -m "refactor(css): implementar variables y tokens de diseno"
git push origin feature/variables-css

# Subactividad 4
git checkout -b feature/interactividad-css
git add .
git commit -m "feat(ui): implementar pseudoclases interactivas en aside y pseudoelementos en productos"
git push origin feature/interactividad-css

# Subactividad 5
git checkout -b feature/arquitectura-bem
git add .
git commit -m "refactor(styles): modularizar codigo en archivos css independientes"
git add index.html
git commit -m "refactor(html): aplicar nomenclatura BEM en los componentes del catalogo"
git add .
git commit -m "refactor(styles): actualizar modulos css con clases BEM planas y documentar hallazgos"
git push origin feature/arquitectura-bem

# Subactividad 6
git checkout -b feature/arquitectura-flexbox
git add .
git commit -m "feat(layout): implementar arquitectura total flexbox en todas las vistas y componentes del proyecto"
git push origin feature/arquitectura-flexbox