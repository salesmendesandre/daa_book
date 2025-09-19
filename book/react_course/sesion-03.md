(sesion03)=
# Sesion 3 - Estado y eventos (3h)

## Objetivos
- Gestionar estado local con el hook `useState` y comprender cuando almacenarlo.
- Manejar eventos del DOM sinteticos en React (`onClick`, `onChange`, etc.).
- Implementar renderizado condicional para responder a cambios en el estado.

## Contenidos
- Concepto de estado como memoria local del componente.
- Declaracion de `useState`, actualizacion inmutable y re-render.
- Eventos sinteticos y paso de callbacks como props.
- Renderizado condicional con operadores logicos y expresiones ternarias.
- Buenas practicas: minimizar estado, derivar valores y evitar renders innecesarios.

## Actividad guiada
1. Crear un contador con botones de incremento, decremento y reset.
2. Mostrar mensajes condicionales en funcion del valor del contador (ej. limite alcanzado).
3. Anadir un campo de entrada que ajuste dinamicamente el paso del contador.
4. Debatir sobre split de componentes cuando el estado crece en complejidad.

## Recursos recomendados
- `useState`: [react.dev/reference/react/useState](https://react.dev/reference/react/useState)
- Manejo de eventos: [react.dev/learn/responding-to-events](https://react.dev/learn/responding-to-events)
