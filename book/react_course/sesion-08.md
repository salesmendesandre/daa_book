(sesion08)=
# Sesion 8 - Componentes avanzados (3h)

## Objetivos
- Compartir estado entre componentes mediante el patron de lifting state up.
- Implementar comunicacion de hijo a padre a traves de callbacks.
- Construir una lista de productos con un carrito de compras basico.

## Contenidos
- Identificacion de la minima representacion comun del estado.
- Lifting state up: cuando mover estado hacia arriba y como pasar setters.
- Callbacks como props para emitir eventos desde componentes hijos.
- Derivar datos: totales, subtotales y estados derivados.
- Consideraciones sobre contextos globales para estados compartidos mas amplios.

## Actividad guiada
1. Definir un catalogo simple de productos con `id`, `nombre`, `precio` y `stock`.
2. Crear un componente `ProductList` que reciba el catalogo y callbacks para anadir al carrito.
3. Gestionar el carrito en un componente padre y calcular el total en tiempo real.
4. Analizar mejoras futuras: contexto global, persistencia y manejo de stock.

## Recursos recomendados
- Sharing State: [react.dev/learn/sharing-state-between-components](https://react.dev/learn/sharing-state-between-components)
- Thinking in React (repaso): [react.dev/learn/thinking-in-react](https://react.dev/learn/thinking-in-react)
