(sesion02)=
# Sesión 2 - Componentes y props

## Objetivos
- Profundizar en la creación de componentes funcionales reutilizables.
- Comprender cómo fluyen los datos mediante props entre componentes padre e hijo.
- Identificar patrones de composición (children, render props, componentes presentacionales).
- Preparar una base que facilite la escalabilidad del código en sesiones posteriores.

## Recordatorio: componentes funcionales
Un componente funcional es una función de JavaScript que recibe un objeto `props` y devuelve JSX. Siempre debe empezar con mayúscula para que React lo reconozca como componente.

```jsx
function Header(props) {
  return <h1>{props.title}</h1>
}

export default Header
```

En la práctica, se recomienda **desestructurar** las props para mejorar la legibilidad:

```jsx
function Header({ title }) {
  return <h1>{title}</h1>
}
```

Desde React 16.8, los hooks (`useState`, `useEffect`, etc.) nos permiten gestionar estado y efectos dentro de estos componentes funcionales, por lo que son el estándar actual.

## Props como contrato entre componentes
Las props permiten que un componente padre configure a un hijo. Piensa en ellas como los parámetros de una función:

- **Inmutables**: un componente no debe mutar sus props; si necesita cambiarlas, debe solicitarlo al padre mediante callbacks.
- **Tipadas de forma informal**: en JavaScript podemos definir defaults o validaciones ligeras, y reforzarlas con TypeScript o PropTypes.
- **Autodocumentadas**: al nombrarlas con claridad (`isPrimary`, `onDelete`, `variant`) facilitan el mantenimiento.

### Ejemplo: componente `UserCard`
Creamos un componente que recibe `name`, `role`, `avatar` y `children` opcionales para acciones extra.

```jsx
// src/components/UserCard.jsx
import PropTypes from 'prop-types'
import './UserCard.css'

export function UserCard({ name, role, avatar, children }) {
  return (
    <article className="user-card">
      <img className="user-card__avatar" src={avatar} alt={`Avatar de ${name}`} />
      <div className="user-card__info">
        <h2>{name}</h2>
        <p className="user-card__role">{role}</p>
        {children ? <div className="user-card__actions">{children}</div> : null}
      </div>
    </article>
  )
}

UserCard.propTypes = {
  name: PropTypes.string.isRequired,
  role: PropTypes.string.isRequired,
  avatar: PropTypes.string,
  children: PropTypes.node,
}

UserCard.defaultProps = {
  avatar: 'https://i.pravatar.cc/120?img=3',
  children: null,
}
```

`PropTypes` es opcional pero útil en equipos grandes; en proyectos nuevos considera TypeScript para contar con tipos estáticos.

### Uso del componente en una lista

```jsx
// src/App.jsx
import { UserCard } from './components/UserCard'

const USERS = [
  {
    id: 1,
    name: 'Ada Lovelace',
    role: 'Backend Engineer',
    avatar: 'https://i.pravatar.cc/120?img=5',
  },
  {
    id: 2,
    name: 'Grace Hopper',
    role: 'Staff Engineer',
    avatar: 'https://i.pravatar.cc/120?img=12',
  },
  {
    id: 3,
    name: 'Margaret Hamilton',
    role: 'Engineering Manager',
    avatar: 'https://i.pravatar.cc/120?img=8',
  },
]

export default function App() {
  return (
    <main className="layout">
      <h1>Equipo de producto</h1>

      <section className="user-grid">
        {USERS.map((user) => (
          <UserCard key={user.id} {...user}>
            <button className="button button--secondary">Ver perfil</button>
          </UserCard>
        ))}
      </section>
    </main>
  )
}
```

### Reutilización mediante composición
El patrón `children` permite que el componente padre inserte JSX arbitrario dentro del hijo. Otras estrategias frecuentes:

- **Render props**: pasar una función como prop (`renderItem`, `footer`) que devuelva JSX según datos internos.
- **Componentes contenedor/presentacional**: un contenedor gestiona datos y lógica (fetch, estado), mientras que un presentacional recibe props y solo dibuja UI.

```jsx
function UserList({ users, renderActions }) {
  return (
    <section className="user-grid">
      {users.map((user) => (
        <UserCard key={user.id} {...user}>
          {renderActions ? renderActions(user) : null}
        </UserCard>
      ))}
    </section>
  )
}
```

De esta forma separamos responsabilidad y reducimos duplicidad.

## Buenas prácticas al trabajar con props
- **Nombrado explícito**: evita abreviaturas confusas, incluso cuando el objeto prop tenga muchos campos.
- **Defaults razonables**: usa `defaultProps` (para componentes creados con `function`) o parámetros con valor por defecto al desestructurar.
- **Documentación**: añade comentarios o README cortos que expliquen qué espera cada prop cuando el componente es compartido.
- **Evita pasar props innecesarios**: si un componente hijo no los usa, mantenlos cerca de donde se necesitan para evitar “prop drilling”. En próximas sesiones veremos alternativas como context o librerías de estado global.

## Actividad guiada
1. Crea el archivo `src/components/UserCard.jsx` con el código anterior y su hoja de estilos `UserCard.css`.
2. Refactoriza `App.jsx` para importar `UserCard` y renderizar una lista de usuarios real o ficticia.
3. Agrega un botón `Contactar` que reciba un callback `onContact` como prop. Haz que muestre un `alert` con el nombre del usuario seleccionado.
4. Añade un campo opcional `status` (ej. `Disponible`, `En proyecto`). Si la prop existe, muéstrala con un badge de color.
5. Documenta los props admitidos en un comentario JSDoc o en el README del proyecto.

## Retos extra
- Implementa una versión de `UserCard` usando TypeScript (`UserCard.tsx`) y define una interfaz `User` con `name`, `role`, `avatar` y `status`.
- Crea un componente `UserSection` que acepte `title`, `users` y un `emptyMessage`. Si la lista está vacía, muestra el mensaje; de lo contrario reutiliza `UserList`.
- Extrae el dataset `USERS` a `src/data/users.js` y prepara la estructura para futuras peticiones reales.

En la próxima sesión abordaremos el manejo de estado (`useState`) y eventos para dotar de interactividad a estos componentes.
