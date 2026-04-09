# 🎨 Bóveda de Roles y Colores — Discord

> Herramienta web para copiar roles con colores HEX exactos, íconos y configuraciones entre servidores de Discord.
> 100% del lado del cliente · Sin instalación · Funciona directo en el navegador.

---

## ⚠️ ADVERTENCIA IMPORTANTE — LEE ANTES DE USAR

> **El uso de tokens de usuario (user tokens) para automatizar acciones en Discord puede violar los [Términos de Servicio de Discord](https://discord.com/terms).**
>
> Esta herramienta fue creada con **fines educativos y de investigación personal**.
>
> - ❌ **No nos hacemos responsables** de suspensiones, baneos o cualquier consecuencia derivada del uso de esta herramienta.
> - ✅ Úsala **bajo tu propio riesgo** y responsabilidad.
> - 🔒 Tu token **nunca sale de tu navegador** — todo el código se ejecuta localmente.
> - 🚫 **Nunca compartas tu token** con nadie ni lo subas a ningún repositorio.

---

## 📋 ¿Qué hace esta herramienta?

Permite **copiar roles y sus colores exactos** de un servidor Discord origen a un servidor Discord destino, directamente desde el navegador, sin instalar nada.

### Funcionalidades principales

✅ Flujo guiado paso a paso (1 → 5) con indicadores visuales  
✅ Lista todos los servidores a los que perteneces (con íconos de servidor)  
✅ Selección de servidor origen y servidor destino  
✅ Muestra todos los roles del servidor origen con:
  - Nombre del rol con **color de texto en su propio HEX**
  - Cuadro de color circular + código HEX exacto
  - Vista previa del ícono (emoji unicode o ícono personalizado)
  - Posición en la jerarquía
  - Indicadores de hoist (separado), mentionable y managed

✅ **Barra de búsqueda** para filtrar roles por nombre  
✅ **Checkbox individual** para seleccionar qué roles copiar  
✅ **Botón "Seleccionar todo"** / **"Deseleccionar todo"**  
✅ **Vista previa dinámica** de "Roles que se copiarán (X seleccionados)"  
✅ **Botón "Copiar roles seleccionados"** (solo los marcados)  
✅ **Botón "Copiar TODOS los roles"** (excepto @everyone y roles managed) — más destacado  
✅ **Botón "Descargar íconos como ZIP"** — siempre visible  
✅ Copia de **unicode_emoji** directamente  
✅ Copia de **íconos personalizados** (icon_hash → descarga CDN → sube en base64)  
✅ Opciones avanzadas configurables  
✅ Log en tiempo real con timestamps  
✅ Barra de progreso visual con porcentaje y "Rol X de N"  
✅ Manejo automático de rate limits y reintentos  
✅ Pantalla de resultado con resumen detallado  

---

## 🚀 Cómo usar

1. Descarga el archivo `discord-role-copier.html`
2. Ábrelo en tu navegador (Chrome, Firefox, Edge — sin servidor web)
3. **Paso 1:** Introduce tu token de usuario de Discord → "Continuar"
4. **Paso 2:** Selecciona el servidor origen → "Cargar roles"
5. **Paso 3:** Filtra y selecciona los roles que deseas copiar — consulta la vista previa
6. **Paso 4:** Selecciona el servidor destino y configura las opciones
7. Haz clic en **"Copiar roles seleccionados"** o **"⚡ Copiar TODOS los roles"**
8. Sigue el progreso en tiempo real en el log y la barra de progreso

---

## 🖼 Manejo de íconos de roles

### Emojis Unicode
Los roles con `unicode_emoji` se copian directamente en el mismo API call de creación del rol. No requieren ningún paso adicional.

### Íconos personalizados (icon_hash)
1. La herramienta descarga el ícono desde el CDN de Discord (`cdn.discordapp.com/role-icons/`)
2. Lo convierte a Base64 (formato `data:image/png;base64,...`)
3. Lo sube al servidor destino vía PATCH a la API

> **⚠️ Importante:** Los íconos personalizados requieren que el servidor destino tenga **Nivel 2 de Boost** (o superior). Si el servidor no cumple el requisito, la herramienta mostrará un mensaje claro en el log y te ofrecerá descargar el ZIP.

---

## 📦 Descarga de íconos como ZIP

Si el servidor destino no tiene Nivel 2 de Boost, puedes descargar todos los íconos en un ZIP con estructura de carpetas perfectamente organizada.

### Estructura del ZIP

```
[Nombre del Servidor Original]/
├── [Nombre del Rol 1]/
│   ├── icon.png          ← Ícono descargado desde el CDN de Discord
│   └── info.txt          ← Metadatos completos del rol
├── [Nombre del Rol 2]/
│   ├── icon.png
│   └── info.txt
└── ...
```

### Contenido de `info.txt`

```
Nombre del rol: Moderador
Color HEX: #5865F2
Color decimal: 5793778
Posición: 8
Hoist (separado): Sí
Mentionable: No
Managed por Discord: No
Emoji Unicode: Ninguno
Icon Hash: abc123def456...
```

> El botón de descarga ZIP está **siempre visible** en el paso 4 y también en la pantalla de progreso/resultado.

---

## ⚙️ Opciones configurables

| Opción | Descripción | Por defecto |
|--------|-------------|-------------|
| 🎨 Copiar color exacto | Mantiene el HEX del rol original | ✅ Activado |
| 📌 Copiar hoist (separado) | El rol aparece separado en la lista de miembros | ✅ Activado |
| 🔔 Copiar mentionable | Cualquier miembro puede @mencionar el rol | ❌ Desactivado |
| 🔐 Copiar permisos (bitfield) | Copia el bitfield exacto de permisos | ❌ Desactivado |
| 📊 Respetar posición/orden | Recrea la jerarquía en el mismo orden | ✅ Activado |
| 🖼 Copiar íconos de roles | Unicode emoji e íconos personalizados | ✅ Activado |
| 🤖 Saltar roles managed | Omite roles de bots e integraciones | ✅ Activado |
| 🗑️ Eliminar roles existentes | Borra todos los roles del destino antes de copiar | ❌ Desactivado |
| ⏱ Delay entre peticiones | Milisegundos de espera entre cada llamada a la API | 400ms |

> 🔴 **"Eliminar roles existentes"** es **IRREVERSIBLE**. Todos los roles del servidor destino (excepto @everyone y roles managed) serán eliminados permanentemente. La herramienta requiere que marques un **checkbox de confirmación** en un modal de seguridad antes de activar esta opción.

---

## 🔑 ¿Cómo obtener tu token de Discord?

> ⚠️ **NUNCA compartas tu token. Quien tenga tu token tiene acceso total a tu cuenta.**

**Método (navegador web):**

1. Abre Discord en el navegador: [https://discord.com/app](https://discord.com/app)
2. Presiona `F12` para abrir las herramientas de desarrollador
3. Ve a la pestaña **"Console"** (Consola)
4. Pega este código y presiona Enter:

```javascript
(webpackChunkdiscord_app.push([[''],{},e=>{m=[];for(let c in e.c)m.push(e.c[c])}]),m).find(m=>m?.exports?.default?.getToken!==void 0).exports.default.getToken()
```

5. Copia el token que aparece entre comillas

> 💡 También puedes encontrarlo en la pestaña **Network** filtrando por `api/v9` y revisando el header `Authorization` en cualquier petición.

---

## 🛠️ Detalles técnicos

- **Lenguaje:** HTML + CSS + JavaScript vanilla (sin frameworks ni librerías externas)
- **Librería ZIP:** JSZip 3.10.1 — cargada dinámicamente desde CDN al usarse
- **API utilizada:** Discord API v9 (endpoints de usuario)
- **Autenticación:** User Token (header `Authorization`)
- **Ejecución:** 100% en el navegador, sin backend, sin servidor
- **Persistencia:** Ninguna — el token no se guarda en ningún lugar

### Endpoints de la API Discord utilizados

| Método | Endpoint | Uso |
|--------|----------|-----|
| `GET` | `/users/@me/guilds` | Listar servidores del usuario |
| `GET` | `/guilds/{guild.id}/roles` | Obtener roles del servidor origen |
| `POST` | `/guilds/{guild.id}/roles` | Crear nuevo rol en el destino |
| `PATCH` | `/guilds/{guild.id}/roles` | Ajustar posición de roles |
| `PATCH` | `/guilds/{guild.id}/roles/{role.id}` | Subir ícono personalizado |
| `DELETE` | `/guilds/{guild.id}/roles/{role.id}` | Eliminar rol (si se activa esa opción) |

### Conversión de colores

Discord almacena los colores de roles como enteros decimales (no hexadecimal):

```
HEX #5865F2  →  Decimal 5793778
HEX #ED4245  →  Decimal 15548997
HEX #000000  →  Decimal 0 (sin color / predeterminado)
```

---

## 📁 Estructura del repositorio

```
boveda-de-roles-y-colores-discord/
│
├── discord-role-copier.html   ← Herramienta completa (un solo archivo)
└── README.md                  ← Este archivo
```

---

## ⚠️ Consideraciones importantes

### Sobre el rol @everyone
- El rol `@everyone` no puede ser creado ni eliminado mediante la API.
- Esta herramienta lo omite **automáticamente** en todas las operaciones.

### Sobre los roles managed (bots e integraciones)
- Los roles managed son creados y gestionados por Discord/bots automáticamente.
- No pueden ser creados manualmente mediante la API de usuario.
- La herramienta los **omite automáticamente** cuando la opción "Saltar roles managed" está activada (por defecto).

### Sobre los permisos de administrador
- Para crear roles en un servidor necesitas el permiso **"Gestionar roles"** en ese servidor.
- Solo puedes crear roles con permisos iguales o inferiores a los tuyos en la jerarquía.

### Sobre el rate limiting
- Discord limita la cantidad de peticiones por segundo.
- Se recomienda un delay de al menos **300ms** entre peticiones.
- Si recibes errores 429, la herramienta espera automáticamente el tiempo indicado por Discord.
- Para servidores con muchos roles, considera aumentar el delay a 500–600ms.

### Sobre los íconos personalizados y el Nivel 2
- Subir íconos personalizados a roles requiere que el servidor destino tenga **Nivel 2 de Boost** (o superior).
- Si el servidor no cumple el requisito, la herramienta mostrará un aviso en el log.
- Usa el botón de **descarga ZIP** para guardar los íconos y subirlos manualmente cuando el servidor alcance el nivel requerido.

### Sobre los colores
- Un rol con color `#000000` o valor `0` se interpreta como "sin color" en Discord.
- La herramienta muestra estos roles con la etiqueta **Sin color**.

---

## 🔗 Herramientas relacionadas

📦 [Bóveda de Canales y Categorías](https://github.com/douglasvelezv/boveda-de-canales-y-categorias-discord) — Copia la estructura de canales y categorías entre servidores

---

## 📜 Licencia y Disclaimer

Este proyecto se distribuye **sin garantía de ningún tipo**, únicamente con fines educativos.

El autor no se responsabiliza por:
- Suspensiones o baneos de cuentas de Discord
- Pérdida de datos o configuraciones en servidores
- Cualquier consecuencia derivada del uso de esta herramienta

**Usar bajo propia responsabilidad.**

---

Hecho con ❤️ para la comunidad hispana de Discord

*Si esta herramienta te fue útil, considera darle una ⭐ al repositorio*
