# TranscribeAI Pro - Aplicación para Transcripción de Audio

Aplicación web Flask para transcribir archivos de audio a texto con identificación de hablantes (diarización) usando OpenAI Whisper y pyannote.audio.

## 🚀 Características

- **Transcripción de alta calidad** usando modelos Whisper de OpenAI
- **Identificación de hablantes** (diarización) con pyannote.audio
- **Soporte multiidioma** (18+ idiomas)
- **Interfaz web moderna** con Tailwind CSS
- **Procesamiento optimizado** para archivos largos (chunking automático)
- **Exportación** en formatos TXT y DOCX
- **Segmentación temporal** opcional (franjas de 10 minutos)

## 📋 Requisitos Previos

- Python 3.8-3.11
- FFmpeg instalado en el sistema
- 8GB RAM mínimo (16GB+ recomendado)
- Token de HuggingFace (para diarización)

## 🔧 Instalación

1. Clona el repositorio:
```bash
git clone https://github.com/wilsonA2000/APLICACION-PARA-AUDIOS-A-TEXTO.git
cd APLICACION-PARA-AUDIOS-A-TEXTO
```

2. Crea un entorno virtual:
```bash
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate
```

3. Instala las dependencias:
```bash
pip install -r requirements.txt
```

4. Configura las variables de entorno:
```bash
# Crea un archivo .env en la raíz del proyecto
echo "HUGGINGFACE_TOKEN=tu_token_aqui" > .env
```

Para obtener un token de HuggingFace:
- Ve a https://huggingface.co/settings/tokens
- Crea una cuenta si no tienes una
- Genera un nuevo token con permisos de lectura

5. Instala FFmpeg:
- **Windows**: Descarga desde https://ffmpeg.org/download.html
- **Linux**: `sudo apt-get install ffmpeg`
- **Mac**: `brew install ffmpeg`

## 🎯 Uso

1. Inicia la aplicación:
```bash
python app.py
```

2. Abre tu navegador en http://127.0.0.1:5000

3. Sube un archivo de audio (formatos soportados: MP3, WAV, M4A, OGG, FLAC)

4. Selecciona las opciones:
   - **Idioma**: Elige el idioma del audio o deja en automático
   - **Número de hablantes**: Especifica cuántos hablantes hay en el audio
   - **Marcas de tiempo**: Incluir timestamps en la transcripción

5. Haz clic en "Transcribir con IA" y espera el procesamiento

6. Descarga el resultado en formato TXT o DOCX

## ⚡ Optimización para Archivos Grandes

La aplicación incluye optimizaciones automáticas:
- Archivos >30 minutos: Se procesan en chunks de 5 minutos
- Archivos >60 minutos: Se omite la diarización para ahorrar memoria
- Monitoreo de memoria con limpieza automática

Para mejores resultados con archivos muy largos, consulta [SYSTEM_REQUIREMENTS.md](SYSTEM_REQUIREMENTS.md)

## 🛠️ Configuración Avanzada

### Cambiar el modelo de Whisper

En `app.py`, línea 29:
```python
# Modelos disponibles: tiny, base, small, medium, large, large-v2, large-v3
model = whisper.load_model('base', device=device)
```

### Habilitar GPU (NVIDIA)

Si tienes una GPU NVIDIA con CUDA:
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

## 📁 Estructura del Proyecto

```
APLICACION-PARA-AUDIOS-A-TEXTO/
├── app.py                    # Aplicación Flask principal
├── requirements.txt          # Dependencias de Python
├── .env                     # Variables de entorno (no incluido en git)
├── .gitignore              # Archivos ignorados por git
├── README.md               # Este archivo
├── CLAUDE.md               # Instrucciones para Claude AI
├── SYSTEM_REQUIREMENTS.md  # Requerimientos detallados del sistema
└── templates/
    ├── index.html          # Interfaz principal (deprecada)
    └── dashboard.html      # Nueva interfaz mejorada
```

## 🐛 Solución de Problemas

### Error: "Killed" durante el procesamiento
- **Causa**: Memoria insuficiente
- **Solución**: Cierra otras aplicaciones o usa un modelo más pequeño

### Error: "No se encontró HUGGINGFACE_TOKEN"
- **Causa**: Falta configurar el token
- **Solución**: Crea el archivo .env con tu token de HuggingFace

### El audio no se procesa correctamente
- **Causa**: Formato no soportado o archivo corrupto
- **Solución**: Verifica que FFmpeg esté instalado correctamente

## 🤝 Contribuciones

Las contribuciones son bienvenidas. Por favor:
1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Ver el archivo [LICENSE](LICENSE) para más detalles.

## 👤 Autor

**Wilson A**
- GitHub: [@wilsonA2000](https://github.com/wilsonA2000)

## 🙏 Agradecimientos

- [OpenAI Whisper](https://github.com/openai/whisper) por el modelo de transcripción
- [pyannote.audio](https://github.com/pyannote/pyannote-audio) por la diarización
- [Flask](https://flask.palletsprojects.com/) por el framework web
- [Tailwind CSS](https://tailwindcss.com/) por los estilos