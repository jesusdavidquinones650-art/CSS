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