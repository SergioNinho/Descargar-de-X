# Descargar-de-X
Proyecto X Video Downloader Este proyecto permite descargar videos desde URLs de X (anteriormente conocido como Twitter) utilizando yt-dlp.
## Requisitos
Python 3.7+

## Bibliotecas:

yt_dlp

os

pathlib

## Instalación
Clona este repositorio.

Instala las bibliotecas necesarias utilizando pip:
```
pip install yt_dlp
```
## Uso
Para descargar videos de X (antes Twitter), puedes utilizar la función bajar_x.

## Ejemplo de uso
```
import yt_dlp
import os
from pathlib import Path

def bajar_x(url):
    """
    Descarga un video desde una URL de X (antes Twitter) usando yt-dlp con un nombre de archivo específico.

    Args:
        url (str): URL del video o tweet que contiene el video.

    Returns:
        str: Ruta completa del archivo descargado.
    """
    
    path_x = 'Videos'
    folder_x = '@surgir.mp4'
    url_descargas_x = str(Path.home() / path_x)
    
    os.makedirs(url_descargas_x +'/'+folder_x, exist_ok=True)
    
    ydl_opts = {
        'format': 'best',  # Descargar la mejor calidad disponible
        'quiet': True,     # Desactiva mensajes en la consola
    }

    with yt_dlp.YoutubeDL(ydl_opts) as ydl:
        # Extraer información del video (sin descargar)
        info = ydl.extract_info(url, download=False)

        # Obtener título
        titulo = info.get("title", "video_sin_titulo")
        extension = info.get("ext", "mp4")  # Extensión predeterminada (mp4)

        # Determinar el nombre del archivo
        nombre_archivo = f"{titulo}.{extension}"
        print(nombre_archivo)
        if len(nombre_archivo) > 40:
            # Actualizar la plantilla de salida
            ydl_opts['outtmpl'] = f'{os.path.join(url_descargas_x, folder_x)}/Asurgir-{nombre_archivo[0:20]}....mp4'
            try:
                with yt_dlp.YoutubeDL(ydl_opts) as ydl:
                    # Descargar el video
                    ydl.download([url])
            except Exception as e:
                raise RuntimeError(f"Error al descargar el video: {e}")
        elif len(nombre_archivo) <= 40:
            ydl_opts['outtmpl'] = f'{os.path.join(url_descargas_x, folder_x)}/Asurgir-{nombre_archivo}'
            try:
                with yt_dlp.YoutubeDL(ydl_opts) as ydl:
                    # Descargar el video
                    ydl.download([url])
            except Exception as e:
                raise RuntimeError(f"Error al descargar el video: {e}")

# Ejemplo de llamada a la función
# bajar_x("https://x.com/MariaFdaCabal/status/1859920721650069714")
```
## Contribución
Si deseas contribuir a este proyecto, por favor crea un fork del repositorio y abre un Pull Request con tus cambios.

## Licencia
Este proyecto está bajo la licencia MIT.
