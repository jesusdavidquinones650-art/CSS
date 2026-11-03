# CSS
# Taller CSS - Jerarquia y Especificidad

Resumen del trabajo realizado para la guia de CSS.

## Calculo de Especificidad
El navegador le da un peso a cada selector para saber cual aplicar:
- Etiqueta = 1 punto (ej: body, h1, a)
- Clase = 10 puntos (ej: .btn-comprar)
- ID = 100 puntos (ej: #btn-destacado)

## El conflicto del boton
En el HTML, el boton de "Mouse" tiene la clase `btn-comprar` y el ID `btn-destacado`.
Al principio en el CSS puse el ID con color rojo y la clase con color azul.
El boton se pintó de rojo porque el ID pesa 100 puntos y la clase solo 10, sin importar el orden en que escribí el código (la cascada).

## Refactorizacion
Para arreglar esto y no usar malas prácticas como `!important` o IDs en CSS, refactoricé el código:
- En el HTML le agregué una segunda clase al enlace: `class="btn-comprar destacado"`.
- En el CSS borré la regla del `#btn-destacado` y usé `.btn-comprar.destacado` (que vale 20 puntos). Así se mantiene el color rojo de forma limpia.

## Comandos de Git
Los comandos que usé para subir esto fueron:
git add .
git commit -m "feat(styles): maquetar catalogo semantico y aplicar jerarquia CSS"
git push origin develop
