# Prompt Manager

Aplicación web progresiva (PWA) para gestionar, organizar y reutilizar prompts de inteligencia artificial de forma rápida y eficiente.

## ✨ Características

- **CRUD completo** — Crear, editar, eliminar y visualizar prompts.
- **Búsqueda en tiempo real** — Filtra prompts por título o contenido con acentos normalizados.
- **Selección múltiple** — Modo selección con *long press* (móvil) o *click* en el icono checklist (escritorio) para eliminar en lote.
- **Expansión inline** — Cada prompt se expande/colapsa con una animación suave para ver su contenido sin salir de la lista.
- **Copiado rápido** — Botón de copia en cada tarjeta para llevar el prompt al portapapeles con un solo clic.
- **Modo oscuro** — Alternancia entre tema claro/oscuro con persistencia en `localStorage`.
- **Offline primero** — Service Worker con estrategia *stale-while-revalidate* y precarga de assets. Los prompts se cachean en `localStorage` para funcionar sin conexión.
- **PWA instalable** — `manifest.json` e iconos permiten instalar la app en el dispositivo móvil o escritorio.
- **Atajos de teclado** — `Ctrl+K` / `Cmd+K` enfoca el buscador; `Escape` cierra el modal.

## 🚀 Stack

| Tecnología | Uso |
|-----------|-----|
| HTML5 + Tailwind CSS (CDN) | UI y estilos |
| Supabase (JS v2) | Backend y base de datos |
| Service Worker | Cache offline y PWA |
| Material Symbols | Iconografía |
| Google Fonts (Inter + JetBrains Mono) | Tipografía |

## 📦 Instalación

1. Clona el repositorio:
   ```bash
   git clone https://github.com/tuusuario/prompt-manager.git
   cd prompt-manager
   ```

2. Sirve la aplicación con cualquier servidor estático:
   ```bash
   npx serve .
   # o
   python3 -m http.server 8080
   ```

3. Abre `http://localhost:8080` en tu navegador.

> No requiere build step ni dependencias de Node. Todo se sirve desde archivos estáticos.

## 🔧 Configuración

La app se conecta a una instancia de Supabase. Las credenciales están en `index.html`:

```js
const SUPABASE_URL = 'https://tu-proyecto.supabase.co';
const SUPABASE_ANON_KEY = 'tu-anon-key';
```

Crea una tabla `prompts` en Supabase con las columnas:

| Columna | Tipo |
|---------|------|
| `id` | `uuid` (primary key, default `gen_random_uuid()`) |
| `title` | `text` |
| `content` | `text` |
| `created_at` | `timestamptz` (default `now()`) |

Asegúrate de habilitar **RLS** y crear una política que permita `SELECT`, `INSERT`, `UPDATE`, `DELETE` para el rol `anon` (o configura autenticación según necesites).

## 📁 Estructura

```
├── index.html       # Aplicación completa (UI + lógica)
├── manifest.json    # Configuración PWA
├── sw.js            # Service Worker (caching offline)
├── icon-192.png     # Icono 192x192
├── icon-512.png     # Icono 512x512
└── README.md
```

## 🧠 Uso

1. Presiona el botón **+** (abajo a la derecha) para crear un nuevo prompt.
2. Escribe un título y el contenido de tu prompt, luego guarda.
3. Haz clic en una tarjeta para expandir/colapsar su contenido.
4. Usa el icono **copy** para copiar el prompt al portapapeles.
5. Usa el buscador (o `Ctrl+K`) para filtrar rápidamente.
6. Activa el **modo selección** para eliminar varios prompts a la vez.

## 📄 Licencia

MIT
