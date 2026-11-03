# Roblox-Studio-Webcam

# Roblox Webcam Bridge

Muestra tu **cámara web** o tu **pantalla compartida** dentro de una pantalla en **Roblox Studio**.

Roblox no permite acceder a la cámara ni a la pantalla desde código. Este proyecto lo resuelve con un puente:

```
Cámara / Pantalla -> programa de Python (localhost:8000) -> plugin de Studio -> EditableImage en una pantalla
```

> Pensado para uso local en Studio (pruebas, demos, proyectos personales). No funciona para otros jugadores ni en un juego publicado, y transmitir video de personas puede ir contra las normas de Roblox.

## Requisitos

- Windows, macOS o Linux
- Python 3.9 o superior (en Windows, marca "Add Python to PATH" al instalarlo)
- Roblox Studio

## Instalación

1. Descarga o clona este repositorio.
2. Instala las dependencias:
   - Windows: doble clic en `iniciar.bat` (también instala y abre el programa).
   - macOS / Linux: `./iniciar.sh`
   - A mano: `pip install -r requirements.txt` y luego `python bridge/app.py`
3. Instala el plugin: en Studio ve a **Plugins > Plugins Folder**, copia ahí `roblox/WebcamBridgePlugin.lua` y reinicia Studio.
4. En Studio activa **Home > Game Settings > Security > Allow HTTP Requests**.
5. La primera vez, Studio pedirá permiso para que el plugin use HTTP con `localhost`. Acéptalo.

## Uso

1. Abre el programa (`iniciar.bat`). Elige **Cámara** o **Pantalla compartida**, el dispositivo, la resolución y los cuadros por segundo, y pulsa **Activar**.
2. En Studio, pestaña **Plugins > Webcam Bridge**:
   - **Pantalla**: crea (o selecciona) el bloque `PantallaWebcam`. Puedes moverlo y escalarlo como quieras.
   - **Activar**: empieza a dibujar la imagen. Púlsalo otra vez para desactivar.
3. Mira el bloque por su cara frontal, en modo edición (sin pulsar Play).

Puedes cambiar de cámara, de pantalla o de resolución con el programa abierto; el plugin se ajusta solo.

## Solución de problemas

| Problema | Qué hacer |
|---|---|
| `ModuleNotFoundError: No module named 'cv2'` | Ejecuta `pip install -r requirements.txt` |
| La ventana negra se cierra sola | Abre una terminal en la carpeta y ejecuta `python bridge/app.py` para ver el error |
| Studio dice "HTTP requests are not enabled" | Activa Allow HTTP Requests (paso 4) |
| La pantalla se ve negra | Mírala por la cara frontal; comprueba que el programa diga "Activo" |
| "No se pudo abrir la cámara" | Cierra Zoom, Teams, el navegador u otra app que use la cámara |
| Puerto 8000 ocupado | Define `BRIDGE_PORT` (por ejemplo `8001`) y cambia `BASE_URL` en el plugin |
| Error de permisos con `EditableImage` | Tu cuenta puede necesitar verificación para usar esta función |

## Límites

- La resolución es baja a propósito (cada cuadro viaja por HTTP sin comprimir). Con 64x48 va fluido; con 256x144 puede ir más lento.
- Solo se ve en Studio en modo edición.
- El servidor escucha únicamente en `127.0.0.1`, así que nadie más en tu red puede ver tu cámara.
