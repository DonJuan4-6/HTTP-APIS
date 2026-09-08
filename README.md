# Pokédex — Aplicación web con React

## 1. Objetivo del proyecto

El proyecto es una aplicación web creada con React que funciona como una Pokédex. Sus funciones principales son:

- Buscar Pokémon por nombre.
- Consultar la información desde PokéAPI.
- Agregar Pokémon al equipo personal.
- Guardar el equipo en una API local usando JSON Server.
- Subir el nivel de los Pokémon y marcar o quitar favoritos.
- Eliminar Pokémon desde el servicio local (pendiente por implementar en la interfaz)。

La lógica principal se encuentra en `App.jsx`, `Pokedex.jsx` y `MiEquipo.jsx`。



## 2. Tecnologías utilizadas

- **React 19:** creación de componentes e interfaz.
- **JavaScript y JSX:** lógica y estructura de los componentes。
- **Vite:** servidor de desarrollo y herramienta de compilación。
- **Fetch API:** realización de solicitudes HTTP。
- **PokéAPI:** consulta externa de información de Pokémon。
- **JSON Server:** creación de una API REST local。
- **CSS:** estilos visuales y diseño responsive。
- **Oxlint:** herramienta de revisión y análisis del código。

Estas dependencias y comandos están definidos en `package.json`。



## 3. PokéAPI como API externa de consulta

PokéAPI es un servicio externo que proporciona información sobre Pokémon。

En `pokeApi.js`, la aplicación utiliza la dirección base:

```js
const API_URL = "https://pokeapi.co/api/v2";
```

La función `buscarPokemon` realiza una solicitud `GET`:

```js
fetch(`${API_URL}/pokemon/${nombre.toLowerCase()}`)
```

Por ejemplo, para buscar a Pikachu se consulta:

```text
https://pokeapi.co/api/v2/pokemon/pikachu
```

La respuesta contiene datos como:

- Nombre。
- Imagen。
- Altura。
- Peso。
- Información adicional del Pokémon。



Si el Pokémon no existe, la aplicación muestra el mensaje `"Pokémon no encontrado"`。



## 4. JSON Server como API local de práctica

JSON Server convierte el archivo `db.json` en una API REST local。

La colección principal es:

```text
http://localhost:3001/equipo
```

Esta API permite:

- Consultar el equipo guardado。
- Agregar nuevos Pokémon。
- Actualizar el nivel o el estado de favorito。
- Eliminar Pokémon。





El servicio está definido en `equipoApi.js`。

El archivo `db.json` contiene datos de ejemplo como:

```json
{
  "id": 1,
  "nombre": "pikachu",
  "nivel": 20,
  "favorito": false
}
```

El campo `id` identifica de forma única a cada Pokémon del equipo y es el que se usa en las operaciones de actualización y eliminación。

JSON Server es útil para practicar APIs y métodos HTTP sin necesidad de crear un backend completo。



## 5. Explicación de GET, POST, PATCH y DELETE

### GET

Se utiliza para obtener información。 En este proyecto se usa en dos contextos:

- **JSON Server:** obtiene la lista de Pokémon guardados en el equipo:

```text
GET http://localhost:3001/equipo
```

- **PokéAPI:** consulta la información de un Pokémon externo：

```js
fetch(`${API_URL}/pokemon/${nombre.toLowerCase()}`)
```

### POST

Se utiliza para crear un nuevo recurso。 En este proyecto agrega un Pokémon al equipo:

```js
fetch(API, {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify(pokemon)
})
```

Solicitud:

```text
POST http://localhost:3001/equipo
```

### PATCH

Se utiliza para modificar parcialmente un recurso existente。 El proyecto lo utiliza para actualizar el nivel o el estado de favorito:

```js
fetch(`${API}/${id}`, {
  method: "PATCH",
  headers: {
    "Content-Type": "application/json"
  },
  body: JSON.stringify(cambios)
})
```

Ejemplo de cuerpo de solicitud:

```json
{
  "nivel": 2
}
```

o:

```json
{
  "favorito": true
}
```

### DELETE

Se utiliza para eliminar un recurso。 El proyecto tiene implementada la función:

```js
fetch(`${API}/${id}`, {
  method: "DELETE"
})
```

Solicitud:

```text
DELETE http://localhost:3001/equipo/id-del-pokemon
```

Esta función está disponible en el servicio, aunque actualmente no hay un botón visible en la interfaz que la ejecute。



## 6. Instrucciones para ejecutar el proyecto

Desde la carpeta del proyecto:

```powershell
cd C:\3409609\Carolina\HTTP\HTTP_APIS
```

> Nota: reemplaza esta ruta por la ubicación real del proyecto en tu equipo。

### Instalar dependencias

```powershell
npm install
```

### Ejecutar JSON Server

En una terminal:

```powershell
npm run api
```

La API local estará disponible en:

```text
http://localhost:3001
```

### Ejecutar React con Vite

En otra terminal:

```powershell
npm run dev
```

Vite mostrará una dirección similar a:

```text
http://localhost:5173
```

Ambos comandos deben ejecutarse al mismo tiempo: `npm run api` mantiene activa la API local y `npm run dev` ejecuta la aplicación React。
