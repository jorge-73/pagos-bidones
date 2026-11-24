# Anotador de pagos — Bidones de agua

App web instalable (PWA) para anotar, mes a mes, qué compañeros pagaron el servicio de bidones de agua.
Funciona en el celular como una app, **sin registro y sin servidor**: los datos quedan guardados en el navegador del dispositivo.

## Qué incluye

- **Mes actual** con navegación entre meses, total recaudado, pendiente y cuántos pagaron.
- Lista por **número de casillero** con botón para marcar **Pagó / Debe**.
- Filtros (Todos, Deben, Pagaron) y buscador por nombre, casillero o teléfono.
- **Compañeros**: casillero único, nombre y apellido, teléfono, observaciones y estado activo/inactivo.
- Acceso directo para **llamar o abrir WhatsApp**.
- **Recordatorios por WhatsApp** a quienes deben, uno por uno o desde una lista, con mensaje editable.
- **Monto general por mes**, editable cuando cambia el precio.
- **Copia de seguridad** en archivo `.json` (descargar, compartir e importar).
- Funciona **sin internet** después de la primera carga.
- Modo claro/oscuro automático según el teléfono.

## Archivos

```
index.html               La aplicación (todo el código va adentro)
manifest.webmanifest     Datos de instalación de la app
sw.js                    Service worker (funcionamiento sin internet)
icons/                   Iconos de la app
.nojekyll                Para que GitHub Pages no procese el sitio
README.md                Esta guía
```

## Probarla en la computadora

Hacé doble clic en `index.html` y se abre en el navegador.

> La instalación como app y el uso sin internet necesitan que el sitio se abra por `https://`.
> Por eso conviene publicarla (paso siguiente) antes de instalarla en el celular.

## Publicar en GitHub Pages

1. Entrá a [github.com](https://github.com) y creá un repositorio nuevo:
   - Nombre sugerido: **`pagos-bidones`**
   - Visibilidad: **Public** (GitHub Pages gratuito requiere repositorio público)
   - No hace falta agregar README ni licencia.
2. En el repositorio, elegí **Add file → Upload files**.
3. Arrastrá **el contenido** de esta carpeta (no la carpeta entera):
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `.nojekyll`
   - la carpeta `icons`
   - `README.md` (opcional)
4. Tocá **Commit changes**.
5. Entrá a **Settings → Pages** (Configuración → Páginas):
   - *Source*: **Deploy from a branch**
   - *Branch*: **main** y carpeta **/ (root)**
   - Tocá **Save**.
6. Esperá 1 o 2 minutos. La dirección va a ser:

   `https://TU-USUARIO.github.io/pagos-bidones/`

> El repositorio público solo contiene el código. Los nombres, teléfonos y pagos **no** se suben: quedan en el teléfono.

## Instalar en el celular

**Android (Chrome):**
Abrí la dirección, tocá el menú ⋮ y elegí **Instalar aplicación** (o *Agregar a la pantalla de inicio*).

**iPhone (Safari):**
Abrí la dirección, tocá **Compartir** (el cuadro con la flecha) y elegí **Agregar a pantalla de inicio**.

Después de instalarla, se abre como una app y funciona aunque no tengas internet.

## Uso diario

1. En **Ajustes**, poné el nombre del servicio y el **monto mensual predeterminado**.
2. En **Compañeros**, cargá a cada uno con su casillero, nombre y teléfono.
3. En **Mes**, tocá el botón que dice **Debe** cuando alguien pague. Se pone verde y dice **Pagó**.
   - Si te equivocaste, volvé a tocarlo para desmarcarlo.
4. Usá las flechas **‹ ›** para cambiar de mes. El botón **Ir al mes actual** te devuelve al presente.
5. Si cambia el precio del agua, tocá el monto en el recuadro azul (**“$ 3.500 c/u ✎”**) y escribí el nuevo valor.
   Ese monto se aplica al mes que estás viendo; los meses anteriores no se modifican.
6. El filtro **Deben** te muestra al instante quiénes falta que paguen.

### Compañeros inactivos

Si alguien deja de participar, editalo y desmarcá **Activo**. Deja de aparecer en los meses nuevos, pero sus pagos anteriores quedan guardados. También podés eliminarlo, con la salvedad de que se borran sus pagos de todos los meses.

## Recordatorios por WhatsApp

- En cada compañero que debe aparece un **botón verde de WhatsApp**. Al tocarlo se abre el chat con el mensaje ya escrito.
- El botón **Recordar a los que deben (N)** abre la lista completa de pendientes para enviarles uno por uno.
- Si el compañero no tiene un teléfono válido, el botón cambia a **Copiar**: copia el mensaje para pegarlo manualmente en WhatsApp.
- Al enviar o copiar un recordatorio, la app anota la fecha y muestra **“Recordado hoy”** o el día en la fila del compañero.
- El mensaje se puede editar en **Ajustes → Recordatorios por WhatsApp**. Podés usar `{nombre}`, `{mes}`, `{monto}` y `{servicio}`; la vista previa se actualiza mientras escribís.
- El teléfono debe incluir el **código de país** (por ejemplo, `5491123456789`), igual que para los links de WhatsApp.

## Copia de seguridad

Los datos viven **solo en ese teléfono**. Si se borran los datos del navegador o se pierde el celular, no hay forma de recuperarlos salvo que tengas una copia.

- **Ajustes → Descargar copia (.json)**: guarda un archivo con todo.
- **Compartir copia**: usa el menú del celular (WhatsApp, Drive, correo).
- **Importar copia**: reemplaza todo por el contenido del archivo.
- Guardá una copia cada tanto, por ejemplo al cerrar el mes.

## Novedades

### v1.1.0

- Recordatorio individual por WhatsApp en cada compañero que debe.
- Lista **Recordar a los que deben** con envío por persona y opción de copiar el mensaje.
- Seguimiento de la fecha del último recordatorio por mes.
- Plantilla de mensaje editable, con vista previa y opción de restaurar la predeterminada.

### v1.0.0

- Primera versión: registro de pagos por mes, compañeros, montos, copia de seguridad y uso sin internet.

## Actualizar la app más adelante

1. Reemplazá los archivos modificados en GitHub (**Add file → Upload files**, sobrescribiendo).
2. Para que los teléfonos tomen la versión nueva, cambiá la versión del caché en `sw.js`:
   ```js
   const CACHE = 'pagos-bidones-v1.1.1';
   ```
3. Cerrá y volvé a abrir la app. Se actualiza sola.

## Solución de problemas

| Problema | Solución |
|---|---|
| No aparece “Instalar aplicación” | Verificá que estés en la dirección `https://...` y recargá. En iPhone la instalación es manual desde **Compartir**. |
| “Este navegador no permite guardar datos” | Estás en navegación privada o el almacenamiento está bloqueado. Salí del modo privado o usá otro navegador. |
| WhatsApp no encuentra el número | Cargá el teléfono con código de país, por ejemplo `5491123456789`. |
| Sigue apareciendo una versión vieja | Cambiá la versión de `CACHE` en `sw.js`, volvé a subir el archivo y reabrí la app. |
| Los datos no aparecen en otro teléfono | Es esperado: no hay sincronización. Usá una copia de seguridad para pasarlos. |

## Privacidad

- No hay cuentas, publicidad ni servicios externos.
- No se envía información a ningún servidor.
- Todo se guarda en el almacenamiento local del navegador (`localStorage`) del dispositivo.
