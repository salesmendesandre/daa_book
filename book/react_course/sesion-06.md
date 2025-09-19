(sesion06)=
# Sesion 6 - Ciclo de vida y useEffect (3h)

## Objetivos
- Relacionar el ciclo de vida clasico con los efectos en componentes funcionales.
- Utilizar `useEffect` para efectos secundarios y sincronizacion con el exterior.
- Consumir APIs publicas y gestionar la carga de datos.

## Contenidos
- Revision del ciclo de vida (mount, update, unmount) y su equivalencia con hooks.
- Uso basico de `useEffect`: dependencias, limpieza y patrones comunes.
- Fetching de datos: `fetch`, `async/await`, gestion de errores y estados de carga.
- Prevencion de estados inconsistentes (abort controllers, race conditions).

## Actividad guiada
1. Crear un componente que consulte la API publica de Pokemon o Star Wars.
2. Mostrar estados de `loading`, `error` y datos con renderizado condicional.
3. Anadir filtros o parametros controlados por el usuario.
4. Analizar cuando dividir efectos y como limpiar subscripciones o timers.

## Recursos recomendados
- `useEffect`: [react.dev/reference/react/useEffect](https://react.dev/reference/react/useEffect)
- Data fetching: [react.dev/learn/you-might-not-need-an-effect#fetching-data](https://react.dev/learn/you-might-not-need-an-effect#fetching-data)
