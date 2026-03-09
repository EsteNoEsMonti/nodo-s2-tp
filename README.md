# Trabajo Práctico - Sprint 2: Watchlist

## 📌 Objetivo

Desarrollar una aplicación en React + Vite donde los usuarios puedan visualizar una lista de películas y agregar o eliminar películas de su **watchlist** (lista de películas favoritas). La watchlist debe almacenarse en el **Local Storage**, de manera que no se pierda al recargar la página.

<!-- Este proyecto es un paso más en el aprendizaje de React, reforzando el uso de **props, hooks (useState, useEffect), custom hooks y local storage**. -->

## 🔥 Requerimientos

### 1️⃣ Configuración inicial

-   Crear un nuevo proyecto en **Vite** con React.
-   Instalar y configurar **Tailwind CSS** siguiendo la documentación oficial.
<!-- -   Agregar los íconos de **Bootstrap Icons**. -->

### 2️⃣ Estructura del Proyecto

El código debe organizarse en **componentes reutilizables**. Si quieres puedes usar una estructura similar a esta:

```
/src
 ├── components
 │   ├── MovieCard.jsx
 │   ├── WatchlistModal.jsx
 │   ├── MovieList.jsx
 │   ├── Header.jsx
 │   └── Button.jsx
 ├── pages (la caperta pages deberia estar dentro de components -> /src/components/pages/Home.jsx
 │   ├── Home.jsx
 ├── hooks
 │   ├── useWatchlist.js
 ├── App.jsx
 ├── main.jsx

```
Pero siéntete libre al hacer tu estructura de archivos 

### 3️⃣ Funcionalidades Principales

✅ **Mostrar un listado de películas**

-   Renderizar una lista de películas en la pantalla principal.
-   Cada película debe mostrarse en una tarjeta (**MovieCard**) con su imagen, título y un botón para agregar a la watchlist.

✅ **Agregar películas a la Watchlist**

-   Al hacer clic en "Agregar a mi lista", la película debe almacenarse en un estado global de la aplicación (`useState`).
-   Guardar la watchlist en **Local Storage** para que no se pierda al recargar la página.

✅ **Ver la Watchlist**

-   Implementar un **modal** o **sidebar** que se abra al hacer clic en "Ver mi lista".
-   Mostrar la lista de películas guardadas.
-   Cada película en la watchlist debe tener un botón para **removerla**.

✅ **Persistencia de datos**

-   Usar `useEffect` para cargar la **watchlist desde Local Storage** cuando se monta el componente principal.

### 4️⃣ Estilos

-   Utilizar **Tailwind CSS** para el diseño.
-   La interfaz debe ser **responsive** y de fácil uso.

## 🚀 Recomendaciones y Ayudas

### 🔹 ¿Cómo manejar el estado de la Watchlist?

Puedes crear un estado en el componente principal (`Home.jsx` o `App.jsx`):

```jsx
const [watchlist, setWatchlist] = useState([]);

```

Para agregar una película:

```jsx
const addToWatchlist = (movie) => {
  setWatchlist([...watchlist, movie]);
  localStorage.setItem("watchlist", JSON.stringify([...watchlist, movie]));
};

```

Para eliminar una película:

```jsx
const removeFromWatchlist = (id) => {
  const updatedList = watchlist.filter(movie => movie.id !== id);
  setWatchlist(updatedList);
  localStorage.setItem("watchlist", JSON.stringify(updatedList));
};

```

Para cargar los datos desde Local Storage cuando la página se recarga:

```jsx
useEffect(() => {
  const savedWatchlist = JSON.parse(localStorage.getItem("watchlist")) || [];
  setWatchlist(savedWatchlist);
}, []);

```

### 🔹 ¿Cómo hacer el modal para la Watchlist?

Puedes usar un `useState` para manejar la visibilidad del modal:

```jsx
const [isModalOpen, setIsModalOpen] = useState(false);

```

Dentro del JSX:

```jsx
<button onClick={() => setIsModalOpen(true)}>Ver mi lista</button>
{isModalOpen && <WatchlistModal watchlist={watchlist} onClose={() => setIsModalOpen(false)} />}

```

### 🔹 ¿Cómo estructurar la información de una película?

Puedes usar un array de objetos con esta estructura:

```js
const movies = [
  { id: 1, title: "Inception", image: "URL de la imagen" },
  { id: 2, title: "Interstellar", image: "URL de la imagen" },
  { id: 3, title: "The Dark Knight", image: "URL de la imagen" },
];

```

### 🔹 ¿Cómo pasar props?

Cuando renderizas `MovieCard`, pásale la función `addToWatchlist` como prop:

```jsx
<MovieCard movie={movie} onAdd={addToWatchlist} />

```

En `MovieCard.jsx`:

```jsx
const MovieCard = ({ movie, onAdd }) => (
  <div>
    <h3>{movie.title}</h3>
    <button onClick={() => onAdd(movie)}>Agregar a mi lista</button>
  </div>
);

```

## 🎯 Evaluación

Se evaluará: ✅ Correcta implementación de los componentes y uso de props. ✅ Manejo de estado con **useState** y efectos con **useEffect**. ✅ Uso de **Local Storage** para persistencia de la watchlist. ✅ Diseño coherente y estilos con **Tailwind CSS**. ✅ Implementación de la lógica para agregar y eliminar películas).

----------

📌 **¡Manos a la obra!** Recuerden que pueden usar la plantilla HTML como referencia: [Watchlist en HTML](https://github.com/EsteNoEsMonti/nodo-diplomatura-watchlist-html/tree/master)

Cualquier duda, ¡pregunten en clase! 🎬🍿
