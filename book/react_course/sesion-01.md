(sesion01)=
# Sesión 1 - Introducción y entorno

## Objetivos
- Entender qué es React, en qué se diferencia de otras opciones y por qué es popular para interfaces web modernas.
- Reconocer los conceptos base: Single Page Applications (SPA), componentes y virtual DOM.
- Preparar un entorno de desarrollo funcional con Node.js y un tooling moderno (Vite o Create React App).
- Construir el primer proyecto "Hello World" y editarlo usando JSX.

## Qué es React y por qué se usa
React es una biblioteca de JavaScript enfocada en construir interfaces de usuario declarativas. Su enfoque se centra en describir **qué** debe mostrar la UI para un estado concreto y dejar que React se encargue de los cambios necesarios en el DOM. Algunas de las razones por las que domina el ecosistema frontend son:

- **Productividad**: los componentes reutilizables permiten escalar proyectos complejos sin duplicar lógica ni markup.
- **Ecosistema**: hay tooling maduro (Next.js, Remix, Vite, React Router, Redux, Zustand) y una comunidad enorme que genera contenido, librerías y soporte.
- **Rendimiento**: el virtual DOM compara versiones en memoria para aplicar solo las actualizaciones necesarias sobre el DOM real, minimizando operaciones costosas.
- **Mentalidad declarativa**: se trabaja describiendo estados y transiciones, lo que facilita razonar sobre la aplicación y probarla.

### React vs otras bibliotecas o frameworks
- **Angular** ofrece una solución todo-en-uno (routing, formularios, DI). React es más flexible: eliges librerías según la necesidad.
- **Vue** se centra en la curva de aprendizaje y la integración gradual; React prioriza consistencia con JavaScript moderno y la modularidad.
- **Svelte** compila componentes a JavaScript plano, eliminando virtual DOM. React apuesta por un runtime ligero y un ecosistema enorme. Conocer varias opciones ayuda a entender decisiones de diseño.

## Conceptos clave

### Single Page Applications (SPA)
Una SPA carga un documento HTML inicial y luego actualiza la UI con JavaScript sin recargar la página completa. Ventajas:
- Navegación fluida y rápida.
- Control total del estado en cliente.
- Posibilidad de precargar datos y vistas.

Retos: SEO, tamaño del bundle inicial y necesidad de gestionar rutas y accesibilidad manualmente.

### Componentes
Los componentes encapsulan estructura (JSX), lógica (hooks, estado) y estilos. Pueden componer otros componentes para formar vistas complejas. Se clasifican groso modo en:
- **Contenedores**: gestionan datos, estado y efectos.
- **Presentacionales**: reciben props y renderizan UI pura.

### Virtual DOM
React mantiene una representación en memoria (virtual DOM) del árbol de componentes. Cuando cambia el estado, React calcula una diferencia entre la versión anterior y la nueva, y actualiza solo los nodos necesarios en el DOM real. Esta optimización mejora el rendimiento frente a re-renderizar todo manualmente.

## Preparación del entorno

### 1. Instalar Node.js
- Descarga la versión LTS desde [nodejs.org](https://nodejs.org) o instala con un gestor de versiones (asdf, nvm, fnm).
- Verifica la instalación:

```bash
node -v
npm -v
```

### 2. Elegir gestor de paquetes
- `npm` viene con Node.js y es suficiente para la mayoría de proyectos.
- `pnpm` y `yarn` ofrecen optimizaciones de cache y workflows más rápidos; puedes instalarlos si lo prefieres.

### 3. Seleccionar una herramienta de scaffolding
- **Vite**: arranca más rápido y usa ESBuild/Rollup. Ideal para proyectos nuevos.
- **Create React App (CRA)**: incluye configuraciones opinionadas listas para crear aplicaciones tradicionales con Webpack.

## Crear el primer proyecto con Vite
1. Ejecuta el asistente de Vite:

```bash
npm create vite@latest hello-react -- --template react
```

   - `hello-react` será el nombre del directorio del proyecto.
   - `--template react` genera un proyecto con JSX y React moderno.

2. Instala dependencias y arranca el dev server:

```bash
cd hello-react
npm install
npm run dev
```

3. Abre `http://localhost:5173` en el navegador. Verás la pantalla de bienvenida de Vite + React.

### Alternativa: Create React App

```bash
npx create-react-app hello-react-cra
cd hello-react-cra
npm start
```

CRA tarda un poco más en arrancar, pero la estructura es muy similar.

## Explorando la estructura del proyecto (Vite)
- `index.html`: documento base; Vite inyecta el bundle aquí.
- `src/main.jsx`: punto de entrada. Monta el componente raíz (`App`) en el DOM.
- `src/App.jsx`: componente principal inicial; contiene JSX de ejemplo.
- `src/assets/`: recursos estáticos (logos, imágenes).
- `package.json`: scripts (`dev`, `build`, `preview`) y dependencias.

## Primer componente Hello World
Abre `src/App.jsx` y reemplaza su contenido por algo más simple:

```jsx
import { useState } from 'react'
import './App.css'

export default function App() {
  const [name, setName] = useState('React')

  function handleChange(event) {
    setName(event.target.value)
  }

  return (
    <main className="container">
      <h1>Hola {name}!</h1>
      <p>Bienvenido a tu primer componente en React.</p>

      <label htmlFor="name-input">Personaliza el saludo:</label>
      <input
        id="name-input"
        value={name}
        onChange={handleChange}
        placeholder="Escribe un nombre"
      />
    </main>
  )
}
```

Asegúrate de definir un estilo mínimo en `src/App.css` para apreciar los cambios:

```css
.container {
  max-width: 420px;
  margin: 0 auto;
  padding: 2rem;
  font-family: system-ui, sans-serif;
}

input {
  display: block;
  margin-top: 0.5rem;
  padding: 0.5rem;
  width: 100%;
}
```

`main.jsx` debe seguir montando el componente raíz, normalmente no es necesario modificarlo en esta etapa:

```jsx
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App.jsx'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <App />
  </React.StrictMode>
)
```

## JSX en acción
JSX permite escribir sintaxis similar a HTML dentro de JavaScript. Puntos básicos:
- Usa `className` en lugar de `class`.
- Las expresiones se interpolan con `{}` (`{name}` en el ejemplo anterior).
- Los eventos siguen la convención camelCase (`onChange`, `onClick`).
- Todo componente debe devolver un único nodo raíz; si necesitas varios elementos hermanos, envuélvelos con un `<div>` o un fragmento (`<> ... </>`).

## Actividad guiada
1. Crea un componente `Greeting` que reciba un prop `name` y muestre un saludo personalizado.
2. Importa `Greeting` en `App.jsx` y reutilízalo dos veces con valores distintos.
3. Añade un botón que cambie el tema claro/oscuro modificando una clase CSS en el `body`.
4. Refactoriza el estado para guardar el nombre del usuario y el estado del tema en un objeto usando `useState` con `useState({ name: 'React', theme: 'light' })`.
5. Documenta cada paso en un README corto dentro del proyecto con comandos y lecciones aprendidas.

## Retos extra
- Instala `eslint` con `npm init @eslint/config` e integra reglas básicas (semi, quotes, react-hooks).
- Añade un archivo `.editorconfig` para definir sangrías y final de línea consistente entre editores.
- Prueba a generar el build (`npm run build`) y usa `npm run preview` para verificar el resultado.

En la siguiente sesión profundizaremos en la composición de componentes y la comunicación mediante props.
