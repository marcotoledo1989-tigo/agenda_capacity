# Agenda Capacity 360 Pro · v2.0

Aplicación web responsiva para planificar y controlar la **agenda diaria de trabajos SSDD** según la capacidad operacional por zona, agencia y especialidad (PEXT / HAB).

## Inicio rápido

1. Para revisar la aplicación sin instalar nada, abre `index.html` en un navegador de escritorio compatible.
2. Para utilizarla desde iPhone/iPad u otros equipos, publica los archivos como sitio estático en **GitHub Pages**, **Render Static Site** o **Azure Static Web Apps**. El archivo HTML por sí solo no genera un enlace público.
3. Selecciona la **fecha operativa** en la barra superior.
4. Pulsa **Nueva asignación** e ingresa SSDD, agencia, tipo PEXT/HAB y cuadrilla/responsable. La zona se obtiene automáticamente.
5. Verifica los cupos libres en el formulario y guarda la asignación. Consulta las pestañas Resumen, Agenda diaria, Capacidad zonal, Historial y Datos y respaldo.

## Funciones de la edición Pro

- Interfaz ejecutiva con tipografías Manrope y DM Sans, modo claro/oscuro y navegación adaptable a móvil.
- KPIs de SSDD agendados, cupos ocupados/libres y éxitos diarios.
- Gráficos interactivos de ocupación por grupo y evolución de los últimos 7 días; pulsando una zona o fecha se abre su agenda.
- Vistas de tabla y tarjetas, búsqueda, filtrado, orden por ocupación/disponibilidad y selección de fecha.
- Edición, eliminación e historial por SSDD; controles de prioridad, estado, responsable y observaciones.
- Configuración editable de capacidad PEXT/HAB/flexible con bloqueo de sobreasignaciones.
- Importación masiva CSV y Excel (`.xlsx`, `.xls`), exportación CSV y respaldo/restauración JSON.

## Datos iniciales de capacidad

Los cupos se transcribieron de las imágenes de referencia: **27 cupos totales / día**, distribuidos en **15 PEXT**, **10 HAB** y **2 sin especialidad especificada**. Los 2 restantes corresponden a zona 1 y zona 3, cada una con un cupo configurado como flexible hasta definir PEXT o HAB.

- Las zonas **10, 11 y 14** comparten una capacidad de **3 PEXT + 1 HAB**.
- Las zonas **12 y 13** comparten una capacidad de **3 PEXT + 1 HAB**.
- Se utilizan las 15 zonas y todas las agencias indicadas en las imágenes.

Los estados **Cancelado** y **Reprogramado** liberan capacity del día. Un SSDD no puede repetirse en una misma fecha, pero sí en fechas distintas.

## Carga masiva

Plantilla incluida: `plantilla_agenda.csv`.

Columnas: `SSDD;FECHA;AGENCIA;TIPO;RESPONSABLE;PRIORIDAD;ESTADO;OBSERVACIONES`.

- Fecha: `AAAA-MM-DD` o `DD/MM/AAAA`.
- Tipo: `PEXT` o `HAB`.
- Campos obligatorios: SSDD, fecha, agencia, tipo y responsable.
- XLS y XLSX necesitan Internet para cargar la biblioteca SheetJS desde un CDN. CSV funciona sin conexión.
- Las filas que excedan cupos, repitan SSDD en un día o no sean válidas se omiten.

## Publicación en GitHub Pages

Sube `index.html` y los demás archivos del paquete a la raíz de un repositorio. En **Settings → Pages**, selecciona **Deploy from a branch**, la rama principal y la carpeta raíz (`/`). Una vez publicado, GitHub proporciona la URL real.

## Publicación en Render

Crea un servicio tipo **Static Site**, enlaza el repositorio y utiliza **Publish directory: `.`**. No requiere comando de build, Node.js ni base de datos para esta demostración. Se incluye `render.yaml` para despliegue desde blueprint si lo prefieres.

## Restricciones importantes

**Esta edición es un prototipo local por navegador.** Las agendas y las capacidades editadas se almacenan únicamente en `localStorage` en ese dispositivo y navegador. No se sincronizan entre personas, equipos o sesiones privadas. Un despliegue estático en GitHub/Render **no convierte** ese almacenamiento en una base de datos compartida. Exporta el respaldo JSON periódicamente.

Para uso operacional multiusuario se requiere una siguiente etapa con backend, PostgreSQL, autenticación, perfiles/roles, auditoría transaccional y validación de cupos desde el servidor.
