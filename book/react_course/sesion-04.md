(sesion04)=
# Sesion 4 - Listas y claves (3h)

## Objetivos
- Renderizar colecciones de datos de forma eficiente con `Array.prototype.map`.
- Comprender el papel de las `key` para el reconciler de React.
- Construir una lista de tareas interactiva usando estado local.

## Contenidos
- Repaso de metodos de arrays y estrategias para normalizar datos.
- Renderizado de listas: patrones comunes y extraccion de subcomponentes.
- Seleccion de `key` estables y riesgos de usar indices del array.
- Mutaciones seguras de listas en estado con operaciones inmutables.

## Actividad guiada
1. Definir una estructura de datos para tareas (`id`, `texto`, `completado`).
2. Renderizar la lista con `map`, incorporando un campo para anadir nuevas tareas.
3. Implementar acciones de marcar como completada y eliminar tarea.
4. Discutir como persistir la lista (localStorage, API) como paso siguiente.

## Recursos recomendados
- List rendering: [react.dev/learn/rendering-lists](https://react.dev/learn/rendering-lists)
- Keys y reconciliacion: [react.dev/learn/keeping-components-pure#keys-and-immutability](https://react.dev/learn/keeping-components-pure#keys-and-immutability)
