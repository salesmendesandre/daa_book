(sesion01)=
# Sesion 1 - Introduccion y entorno

## Objetivos
- Entender que es React, en que se diferencia de otras opciones y por que es popular para interfaces web modernas.
- Reconocer los conceptos base: Single Page Applications (SPA), componentes y virtual DOM.
- Preparar un entorno de desarrollo funcional con Node.js y un tooling moderno (Vite o Create React App).
- Construir el primer proyecto "Hello World" y editarlo usando JSX.

## Que es React y por que se usa
React es una biblioteca de JavaScript enfocada en construir interfaces de usuario declarativas. Su enfoque se centra en describir **que** debe mostrar la UI para un estado concreto y dejar que React se encargue de los cambios necesarios en el DOM. Algunas de las razones por las que domina el ecosistema frontend son:

- **Productividad**: los componentes reutilizables permiten escalar proyectos complejos sin duplicar logica ni markup.
- **Ecosistema**: hay tooling maduro (Next.js, Remix, Vite, React Router, Redux, Zustand) y una comunidad enorme que genera contenido, librerias y soporte.
- **Rendimiento**: el virtual DOM compara versiones en memoria para aplicar solo las actualizaciones necesarias sobre el DOM real, minimizando operaciones costosas.
- **Mentalidad declarativa**: se trabaja describiendo estados y transiciones, lo que facilita razonar sobre la aplicacion y probarla.

### React vs otras bibliotecas o frameworks
- **Angular** ofrece una solucion todo-en-uno (routing, formularios, DI). React es mas flexible: eliges librerias segun la necesidad.
- **Vue** se centra en la curva de aprendizaje y la integracion gradual; React prioriza consistencia con JavaScript moderno y la modularidad.
- **Svelte** compila componentes a JavaScript plano, eliminando virtual DOM. React apuesta por un runtime ligero y un ecosistema enorme. Conocer varias opciones ayuda a entender decisiones de diseno.

## Conceptos clave

### Single Page Applications (SPA)
Una SPA carga un documento HTML inicial y luego actualiza la UI con JavaScript sin recargar la pagina completa. Ventajas:
- Navegacion fluida y rapida.
- Control total del estado en cliente.
- Posibilidad de precargar datos y vistas.

Retos: SEO, tamano del bundle inicial y necesidad de gestionar rutas y accesibilidad manualmente.

### Componentes
Los componentes encapsulan estructura (JSX), logica (hooks, estado) y estilos. Pueden componer otros componentes para formar vistas complejas. Se clasifican groso modo en:
- **Contenedores**: gestionan datos, estado y efectos.
- **Presentacionales**: reciben props y renderizan UI pura.

### Virtual DOM
React mantiene una representacion en memoria (virtual DOM) del arbol de componentes. Cuando cambia el estado, React calcula una diferencia entre la version anterior y la nueva, y actualiza solo los nodos necesarios en el DOM real. Esta optimizacion mejora el rendimiento frente a re-renderizar todo manualmente.

## Preparacion del entorno

### 1. Instalar Node.js
- Descarga la version LTS desde [nodejs.org](https://nodejs.org) o instala con un gestor de versiones (asdf, nvm, fnm).
- Verifica la instalacion:

```bash
node -v
npm -v
```

### 2. Elegir gestor de paquetes
- `npm` viene con Node.js y es suficiente para la mayoria de proyectos.
- `pnpm` y `yarn` ofrecen optimizaciones de cache y workflows mas rapidos; puedes instalarlos si lo prefieres.

### 3. Seleccionar una herramienta de scaffolding
- **Vite**: arranca mas rapido y usa ESBuild/Rollup. Ideal para proyectos nuevos.
- **Create React App (CRA)**: incluye configuraciones opinionadas listas para crear aplicaciones tradicionales con Webpack.

## Crear el primer proyecto con Vite
1. Ejecuta el asistente de Vite:

```bash
npm create vite@latest hello-react -- --template react
```

   - `hello-react` sera el nombre del directorio del proyecto.
   - `--template react` genera un proyecto con JSX y React moderno.

2. Instala dependencias y arranca el dev server:

```bash
cd hello-react
npm install
npm run dev
```

3. Abre `http://localhost:5173` en el navegador. Veras la pantalla de bienvenida de Vite + React.

### Alternativa: Create React App

```bash
npx create-react-app hello-react-cra
cd hello-react-cra
npm start
```

CRA tarda un poco mas en arrancar, pero la estructura es muy similar.

## Explorando la estructura del proyecto (Vite)
- `index.html`: documento base; Vite inyecta el bundle aqui.
- `src/main.jsx`: punto de entrada. Monta el componente raiz (`App`) en el DOM.
- `src/App.jsx`: componente principal inicial; contiene JSX de ejemplo.
- `src/assets/`: recursos estaticos (logos, imagenes).
- `package.json`: scripts (`dev`, `build`, `preview`) y dependencias.

## Primer componente Hello World
Abre `src/App.jsx` y reemplaza su contenido por algo mas simple:

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

Asegurate de definir un estilo minimo en `src/App.css` para apreciar los cambios:

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

`main.jsx` debe seguir montando el componente raiz, normalmente no es necesario modificarlo en esta etapa:

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

## JSX en accion
JSX permite escribir sintaxis similar a HTML dentro de JavaScript. Puntos basicos:
- Usa `className` en lugar de `class`.
- Las expresiones se interpolan con `{}` (`{name}` en el ejemplo anterior).
- Los eventos siguen la convencion camelCase (`onChange`, `onClick`).
- Todo componente debe devolver un unico nodo raiz; si necesitas varios elementos hermanos, envolvelos con un `<div>` o un fragmento (`<> ... </>`).

## Actividad guiada
1. Crea un componente `Greeting` que reciba un prop `name` y muestre un saludo personalizado.
2. Importa `Greeting` en `App.jsx` y reutilizalo dos veces con valores distintos.
3. Anade un boton que cambie el tema claro/oscuro modificando una clase CSS en el `body`.
4. Refactoriza el estado para guardar el nombre del usuario y el estado del tema en un objeto usando `useState` con `useState({ name: 'React', theme: 'light' })`.
5. Documenta cada paso en un README corto dentro del proyecto con comandos y lecciones aprendidas.

## Retos extra
- Instala `eslint` con `npm init @eslint/config` e integra reglas basicas (semi, quotes, react-hooks).
- Anade un archivo `.editorconfig` para definir sangrias y final de linea consistente entre editores.
- Prueba a generar el build (`npm run build`) y usa `npm run preview` para verificar el resultado.

En la siguiente sesion profundizaremos en la composicion de componentes y la comunicacion mediante props.
