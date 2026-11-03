# CSS

# Taller CSS - Modelo de Caja

## Hallazgos: El Modelo de Caja

1. **Margin vs Padding:** El `padding` es el espacio por dentro de la caja (aleja el texto del borde). El `margin` es el espacio por fuera (empuja la caja para alejarla de las demás).
2. **box-sizing: border-box:** Es obligatorio para que el padding y el borde no agranden la caja hacia afuera. Así el tamaño total se mantiene y no se daña el diseño.
3. **Margen grande entre hermanos:** Si le pongo un margen grande a un artículo, empuja a los otros artículos, creando un espacio de separación muy grande entre ellos.

## Comandos Git

```bash
git checkout -b feature/modelo-caja
git add .
git commit -m "feat(ui): implementar modelo de caja y backgrounds"
git push origin feature/modelo-caja