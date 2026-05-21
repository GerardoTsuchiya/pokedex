# Pokédex con PokéAPI

**Materia:** Aplicaciones Web  
**Fecha inicio:** 2026-05-12  
**Stack:** React + Vite + TypeScript + React Router  
**API:** https://pokeapi.co/api/v2  
**Repo:** Aplicaciones_Web/Pokedex/pokedex/

---

## Progreso por clase

### Clase 1 — Completada ✅
**Objetivo:** Estructura base y primer consumo de API

Archivos creados:
- `src/types/pokemon.ts` — interfaces TypeScript
- `src/services/pokemonService.ts` — funciones de fetch
- `src/pages/HomePage.tsx` — listado de 20 Pokémon con sprites
- `src/App.tsx` y `src/main.tsx` — entrada de la app

**Entregable:** 20 Pokémon visibles en pantalla con nombre e imagen.

### Clase 2 — Completada ✅
**Objetivo:** Componentes reutilizables, navegación y pantalla de detalle

Archivos creados/modificados:
- `src/components/PokemonCard.tsx` — tarjeta reutilizable que hace su propio fetch para obtener tipos, imagen y número
- `src/pages/DetailPage.tsx` — pantalla de detalle con imagen, tipos, peso, altura, habilidades y estadísticas base
- `src/App.tsx` — React Router configurado con rutas `/` y `/pokemon/:id`
- `src/pages/HomePage.tsx` — actualizado para usar `PokemonCard` en lugar de `<li>` inline

**Entregable:** Listado con tarjetas completas (RF01) y pantalla de detalle funcional (RF02) con navegación entre ambas.

### Clase 3 — Completada ✅
Búsqueda por nombre/número, filtros por tipo, favoritos con persistencia en localStorage, estados de carga, error y sin resultados.

### Clase 4 — Completada ✅
Comparador de estadísticas entre dos Pokémon, diseño final responsive, paginación y preparación para demo.

---

## Historial de commits

| Hash | Mensaje |
|------|---------|
| `717568e` | feat: creación de estructura base e instalación de dependencias base |
| `f995d56` | feat(clase1): tipos, servicio y listado inicial de 20 pokémon |
| `cdc0a6c` | docs(pokedex): reemplazar README de Vite con nota del proyecto |
| `3d32fd1` | Aplicaciones-Web Clase 2: componentes, detalle y navegación (asistido) |



---

## Instalación y ejecución

```bash
npm install
npm run dev
```

Si usas pnpm:

```bash
pnpm install
pnpm dev
```

## Build de producción

```bash
npm run build
```

## Funcionalidades implementadas

- Listado de Pokémon con nombre, imagen, número y tipos.
- Detalle de Pokémon con imagen, tipos, peso, altura, categoría, descripción, habilidades con explicación, estadísticas base y cadena evolutiva.
- Búsqueda por nombre y número.
- Filtro por tipo y generación.
- Ordenamiento por número, nombre, altura y peso.
- Favoritos con persistencia en localStorage.
- Constructor de equipo de 6 Pokémon con persistencia en localStorage.
- Comparador de estadísticas base entre dos Pokémon.
- Estados de carga, error y sin resultados.
- Paginación.
- Diseño responsive.

## Estructura principal

```txt
src/
  components/   # UI reutilizable: tarjetas, filtros, detalle, equipo, favoritos y comparador
  hooks/        # lógica reutilizable: API, filtros, favoritos, equipo y comparador
  pages/        # pantallas principales
  services/     # consumo de PokéAPI
  storage/      # lectura y escritura en localStorage
  types/        # interfaces TypeScript
  utils/        # funciones auxiliares de formato
```

## Notas técnicas

El listado básico de PokéAPI solo devuelve nombre y URL. Para mostrar imagen, tipos, altura, peso, habilidades y estadísticas, el servicio `getPokemonBatch` primero obtiene la lista y luego consulta el detalle de cada Pokémon con `Promise.all`.

La pantalla principal `HomePage.tsx` funciona como contenedor: conecta hooks con componentes visuales. La lógica se separó en custom hooks:

- `usePokemonData` carga Pokémon desde PokéAPI y maneja `loading` y `error`.
- `usePokemonExtraDetails` carga la descripción, categoría, explicaciones de habilidades y cadena evolutiva del Pokémon seleccionado.
- `usePokemonFilters` maneja búsqueda, filtro por tipo/generación, ordenamiento y paginación.
- `useFavorites` maneja favoritos y persistencia local.
- `useTeam` maneja el equipo de 6 Pokémon y persistencia local.
- `usePokemonCompare` maneja la comparación de dos Pokémon.

Los favoritos y el equipo se guardan como arreglos de IDs en `localStorage` para mantenerlos al recargar o cerrar la aplicación.


## Mejora de detalle visual

El panel de detalle consulta información extra solo cuando el usuario selecciona un Pokémon. Esto evita cargar descripciones, habilidades y evoluciones de todos los Pokémon desde el inicio. La información adicional viene de:

- `pokemon-species/{id}` para descripción, categoría y URL de cadena evolutiva.
- `ability/{name}` para descripción de habilidades.
- URL de `evolution_chain` para mostrar las etapas evolutivas.

Si una petición secundaria falla, la app conserva el detalle básico del Pokémon y muestra la información disponible.
