# Tu Lado B 🎧

**Los hábitos y obsesiones que tu historial esconde.**

Tu Lado B es una app web que transforma tu historial ampliado de Spotify en gráficas, hallazgos curiosos y una identidad musical. Descubre qué artistas te acompañan, a qué horas escuchas música, qué canciones repites y cómo han cambiado tus gustos con los años.

Puedes probarla con cuatro usuarios de ejemplo o cargar tus propios archivos. La interfaz está en español mexicano, con un diseño oscuro inspirado en Spotify.

**[Abrir la app](https://tu-lado-b.streamlit.app/)** · **[Ver el repositorio](https://github.com/EnriqueOlveraMonroy/tu-lado-b)**

## ¿Qué puedes descubrir?

| Sección | Qué muestra |
|---|---|
| 📊 Resumen | Reproducciones, minutos escuchados, artistas y canciones únicos, saltos, diversidad y un calendario de actividad. |
| 🧬 Tu arquetipo | Una identidad musical con avatar, descripción narrativa y señales que explican la clasificación. |
| 🕐 Cuándo escuchas | Tus horarios, días y franjas de escucha mediante mapas de calor y perfiles por hora. |
| 🎤 Artistas | Tus artistas y canciones principales, junto con gráficas para explorar tus descubrimientos. |
| ✨ Mi Lado B · Wrapped | Una tarjeta con tu arquetipo, avatar, artistas favoritos y una frase basada en tus datos, lista para descargar como PNG. |
| 🔎 Hallazgos insólitos | Repeticiones de madrugada, días con muchos saltos, artistas amor-odio y canciones que regresan después de una larga pausa. |
| 📈 Evolución anual | Cómo cambia la presencia de tus artistas favoritos entre los años disponibles. |

### Tu historia, año por año

Resumen, Tu arquetipo, Cuándo escuchas y Artistas tienen filtros independientes por año. Por defecto muestran todo el historial cargado. Puedes descubrir que tu arquetipo de 2024 es distinto al de 2026.

La tarjeta Wrapped usa todos los años cargados; no hereda los filtros de otras pestañas. La evolución anual compara los años disponibles por artista, no por género.

### Hallazgos insólitos

- **La canción de la madrugada:** la canción más reproducida entre las 02:00 y antes de las 05:00, en la zona horaria seleccionada.
- **Bucle insomne:** rachas de al menos tres reproducciones consecutivas de la misma canción durante esa franja.
- **El día de mayor caos:** un día con más de 70% de saltos que cumple el mínimo de registros conocidos elegido en la app.
- **Tu artista amor-odio:** entre tus diez artistas más reproducidos que cumplen la muestra mínima, el que acumula más saltos.
- **El regreso del ex musical:** una canción que vuelve tras al menos 90 días sin registros y suma al menos tres reproducciones en los siguientes 30 días.

Los nombres son una forma divertida de contar tus hábitos. Un salto no demuestra que te disguste una canción y una pausa en los registros no demuestra que hayas dejado de escucharla.

### También puedes analizar videos

Activa **Analizar historiales de video** para consultar un ranking de los videos más reproducidos y gráficas sencillas de actividad. Este modo utiliza los archivos de video por separado de los de audio.

### Guarda tus resultados

Cada pestaña de análisis, además del reporte de video, permite descargar una imagen de su sección. La captura incluye el año seleccionado y el contenido visible; abre los detalles que quieras incluir antes de descargarla. Wrapped también permite generar su propia tarjeta PNG para compartir.

## Cómo usar la app

### Probar con ejemplos

1. Abre [Tu Lado B](https://tu-lado-b.streamlit.app/).
2. Elige tu zona horaria.
3. Selecciona **Explorar ejemplos** y uno de los cuatro usuarios.
4. Recorre las pestañas, cambia los filtros y descarga tus resultados.

No necesitas tus propios archivos para conocer la app. El Usuario 4 tiene un historial más grande y puede tardar más en procesarse.

### Analizar tu historial

1. Ten a la mano tu exportación del **historial ampliado de reproducción de Spotify** y descomprime el ZIP en tu computadora.
2. En la app, selecciona **Subir mis archivos**.
3. Para música, carga los archivos `Streaming_History_Audio_*.json`. Puedes seleccionar varios archivos y años al mismo tiempo.
4. Para video, activa el modo correspondiente y carga `Streaming_History_Video_*.json`.
5. Revisa el periodo y los archivos incluidos antes de interpretar las gráficas.

La app trabaja con los archivos exportados: no necesita que conectes tu cuenta de Spotify ni una clave de su API. Los PDF informativos de la exportación no se usan para el análisis.

## Cómo funciona por dentro

```text
Archivos JSON propios o ejemplos
              ↓
Lectura, limpieza y ajuste de zona horaria
              ↓
Cálculo de métricas y patrones de escucha
              ↓
Clasificación del arquetipo y creación de gráficas
              ↓
Exploración por pestañas y descargas PNG
```

`app.py` es el punto de entrada: organiza los controles y coordina los módulos. El procesamiento prepara los registros, calcula las métricas y construye las vistas. Al cambiar un control, Streamlit vuelve a ejecutar el script para actualizar el resultado; la caché permite reutilizar parte del procesamiento de audio.

Los arquetipos se asignan mediante reglas y puntuaciones ponderadas sobre hábitos como diversidad, horarios, saltos y concentración en artistas. No requieren un modelo de IA externo ni constituyen una evaluación psicológica.

## Tecnologías

| Tecnología | Uso |
|---|---|
| Python | Lógica y procesamiento de datos. |
| Streamlit | Interfaz web y controles interactivos. |
| Pandas y NumPy | Limpieza, agrupación y cálculo de métricas. |
| Plotly | Gráficas interactivas. |
| Pillow | Generación de tarjetas Wrapped. |
| html2canvas | Captura de las secciones como imágenes desde el navegador. |
| GitHub y Streamlit Community Cloud | Versionado del código y publicación de la app. |

## Ejecutar en tu computadora

Requiere Git y Python 3.12 o posterior. El despliegue publicado se configuró con Python 3.14.

```bash
git clone https://github.com/EnriqueOlveraMonroy/tu-lado-b.git
cd tu-lado-b
python -m venv .venv
```

En Windows PowerShell, instala y ejecuta usando directamente el Python del entorno:

```powershell
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m streamlit run app.py
```

En macOS o Linux:

```bash
.venv/bin/python -m pip install -r requirements.txt
.venv/bin/python -m streamlit run app.py
```

Abre la dirección que aparezca en la terminal, normalmente `http://localhost:8501`. Mantén la terminal abierta mientras uses la app local.

## Estructura del proyecto

| Archivo o carpeta | Responsabilidad |
|---|---|
| `app.py` | Entrada de la app, carga de datos y navegación. |
| `etl.py` | Lectura y limpieza de historiales de audio. |
| `metrics.py` | Métricas de escucha. |
| `archetypes.py` y `archetype_lore.py` | Reglas, puntuaciones y descripciones de arquetipos. |
| `insights.py`, `insight_views.py` y `musical_comeback.py` | Hallazgos curiosos y evolución. |
| `viz.py` y `rich_charts.py` | Gráficas. |
| `year_filters.py` | Filtros por año. |
| `video.py` | Procesamiento y visualización de videos. |
| `wrapped.py` y `section_export.py` | Tarjetas y descargas de imágenes. |
| `design.py` y `.streamlit/config.toml` | Estilos y tema visual. |
| `examples.py` y `data/` | Carga de los cuatro perfiles de ejemplo. |
| `assets/` | Avatares y recursos visuales. |
| `example_manifest.json` | Inventario de archivos de ejemplo y sus registros. |
| `requirements.txt` y `packages.txt` | Dependencias de Python y del sistema. |
| `test_*.py` | Pruebas automatizadas de procesamiento y funciones. |

## Datos y privacidad

Los cuatro perfiles de ejemplo cuentan con autorización para su publicación. Sus historiales se distribuyen como JSON comprimidos con gzip. Se conservaron las filas y los campos necesarios para el análisis; no se incluyen IP, país de conexión, datos de cuenta, ZIP originales ni documentos adicionales. Las etiquetas Usuario 1 a Usuario 4 no garantizan el anonimato del historial.

Los archivos que sube un visitante se procesan en el servidor que ejecuta la app. No se incorporan al repositorio ni a los perfiles públicos, y el código de la app no los escribe en disco. El procesamiento de audio utiliza una caché en memoria con vencimiento de 30 minutos y un máximo de ocho entradas; las sesiones activas también conservan información en memoria.

## Cómo interpretar los resultados

- Los resultados describen únicamente los archivos cargados. Si falta parte del historial, un año o una comparación pueden estar incompletos.
- Los horarios dependen de la zona seleccionada y de las marcas de tiempo de la exportación.
- El tiempo reproducido no siempre equivale a la duración completa de una canción. Los minutos de audio excluyen reproducciones de menos de cinco segundos.
- Las tasas de salto usan registros con ese dato conocido; su ausencia no equivale a un salto ni a una reproducción completa.
- La app no deduce géneros, ritmo ni estados de salud mental a partir de información que el historial no proporciona.
- En video, un registro de reproducción no confirma que hayas visto el contenido completo ni cuánto tiempo miraste la pantalla.

## Publicación y mantenimiento

La app está publicada en [tu-lado-b.streamlit.app](https://tu-lado-b.streamlit.app/) desde la rama `main`, con `app.py` como archivo principal. Las dependencias se declaran en `requirements.txt` y `packages.txt`.

Para actualizarla, modifica el código, guarda los cambios en un commit y envíalos al repositorio con `git push`. Streamlit Community Cloud toma los cambios de la rama conectada. Consulta `PUBLICAR.md` para ver los datos del despliegue.

## Pruebas

Instala `pytest` en tu entorno y ejecuta la suite desde la raíz del proyecto:

```bash
python -m pip install pytest
python -m pytest -q
```

Usa el Python de `.venv` si no has activado el entorno virtual.

---

Proyecto independiente, sin afiliación con Spotify. Las descripciones de los arquetipos son narrativas y están pensadas para explorar tus hábitos musicales.
