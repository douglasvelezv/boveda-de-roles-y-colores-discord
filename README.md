# 🎨 Bóveda de Roles y Colores — Discord

> **Herramienta web para copiar roles y colores exactos entre servidores de Discord.**
> 100% del lado del cliente, sin instalación, funciona directo en el navegador.

---

## ⚠️ ADVERTENCIA IMPORTANTE — LEE ANTES DE USAR

> **El uso de tokens de usuario (user tokens) para automatizar acciones en Discord va en contra de los [Términos de Servicio de Discord](https://discord.com/terms).**
>
> Esta herramienta fue creada con **fines educativos y de investigación personal**.
>
> - ❌ No nos hacemos responsables de suspensiones, baneos o cualquier consecuencia derivada del uso de esta herramienta.
> - ✅ Úsala **bajo tu propio riesgo** y responsabilidad.
> - 🔒 Tu token **nunca sale de tu navegador** — todo el código se ejecuta localmente.
> - 🚫 **Nunca compartas tu token** con nadie ni lo subas a ningún repositorio.

---

## 📋 ¿Qué hace esta herramienta?

Permite **copiar roles y sus colores exactos** de un servidor Discord origen a un servidor Discord destino, directamente desde el navegador, sin instalar nada.

### Funcionalidades principales

- ✅ Lista todos los servidores a los que perteneces
- ✅ Selección de servidor origen y servidor destino
- ✅ Muestra todos los roles del servidor origen con:
  - Nombre del rol
  - Vista previa del color exacto (cuadro visual + código HEX)
  - Posición actual en la jerarquía
  - Indicador de hoist (mostrado separado) y mentionable
- ✅ Checkbox individual para seleccionar qué roles copiar
- ✅ Botón "Seleccionar todos" / "Deseleccionar todos"
- ✅ Opciones avanzadas configurables
- ✅ Log en tiempo real con timestamps
- ✅ Barra de progreso visual
- ✅ Manejo automático de rate limits

---

## 🚀 Cómo usar

1. Descarga el archivo `discord-role-copier.html`
2. Ábrelo en tu navegador (Chrome, Firefox, Edge — sin servidor web)
3. Introduce tu **token de usuario** de Discord
4. Haz clic en **"Cargar servidores"**
5. Selecciona el servidor **origen** y el servidor **destino**
6. Haz clic en **"Cargar roles"** para ver los roles disponibles
7. Marca los roles que deseas copiar
8. Configura las opciones avanzadas según tus necesidades
9. Haz clic en **"Iniciar copia de roles"**

---

## ⚙️ Opciones configurables

| Opción | Descripción | Recomendación |
|--------|-------------|---------------|
| **Copiar color exacto** | Mantiene el color HEX exacto del rol original | ✅ Siempre activado |
| **Copiar hoist (separado)** | Si el rol se muestra separado en la lista de miembros | Según necesidad |
| **Copiar mentionable** | Si cualquier miembro puede mencionar el rol con @ | Según necesidad |
| **Copiar permisos** | Copia el bitfield exacto de permisos del rol | ⚠️ Revisar antes de activar |
| **Respetar orden/posición** | Recrea la jerarquía de roles en el mismo orden | ✅ Recomendado |
| **Eliminar roles existentes** | Borra todos los roles del destino antes de copiar (excepto @everyone) | 🔴 Irreversible |
| **Delay entre peticiones (ms)** | Milisegundos de espera entre cada llamada a la API | 300ms recomendado |

> 🔴 **La opción "Eliminar roles existentes"** es **IRREVERSIBLE**. Todos los roles del servidor destino (excepto `@everyone`) serán eliminados permanentemente antes de crear los nuevos. Úsala con mucha precaución.

---

## 🔑 ¿Cómo obtener tu token de Discord?

> ⚠️ **NUNCA compartas tu token.** Quien tenga tu token tiene acceso total a tu cuenta.

### Método (navegador web)

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

- **Lenguaje:** HTML + CSS + JavaScript vanilla (sin frameworks ni librerías)
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
| `PATCH` | `/guilds/{guild.id}/roles/{role.id}` | Ajustar posición de rol |
| `DELETE` | `/guilds/{guild.id}/roles/{role.id}` | Eliminar rol (si se activa esa opción) |

### Conversión de colores

Discord almacena los colores de roles como **enteros decimales** (no hexadecimal). La herramienta convierte automáticamente:

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

### Sobre el rol `@everyone`
- El rol `@everyone` **no puede ser creado ni eliminado** mediante la API.
- Esta herramienta lo omite automáticamente en todas las operaciones.
- Sus permisos **no se copian** para evitar consecuencias no deseadas en el servidor destino.

### Sobre los permisos de administrador
- Para crear roles en un servidor necesitas el permiso **"Gestionar roles"** en ese servidor.
- Solo puedes crear roles con permisos **iguales o inferiores** a los tuyos en la jerarquía.

### Sobre el rate limiting
- Discord limita la cantidad de peticiones que puedes hacer por segundo.
- Se recomienda un delay de al menos **300ms** entre peticiones.
- Si recibes errores 429, aumenta el delay en las opciones avanzadas.

### Sobre los colores
- Un rol con color `#000000` o valor `0` se interpreta como **"sin color"** en Discord.
- La herramienta muestra estos roles con la etiqueta `Sin color` en lugar del código hex.

---

## 🔗 Herramientas relacionadas

- 📦 [Bóveda de Canales y Categorías](https://github.com/douglasvelezv/boveda-de-canales-y-categorias-discord) — Copia la estructura de canales y categorías entre servidores

---

## 📜 Licencia y Disclaimer

Este proyecto se distribuye **sin garantía de ningún tipo**, únicamente con fines educativos.

El autor **no se responsabiliza** por:
- Suspensiones o baneos de cuentas de Discord
- Pérdida de datos o configuraciones en servidores
- Cualquier consecuencia derivada del uso de esta herramienta

**Usar bajo propia responsabilidad.**

---

<div align="center">

Hecho con ❤️ para la comunidad hispana de Discord

*Si esta herramienta te fue útil, considera darle una ⭐ al repositorio*

</div>
