# Requerimientos del Sistema - TranscribeAI Pro

## Configuraciones Recomendadas

### 🔥 Configuración Óptima (Máxima Calidad)
**Para archivos largos (>2 horas) con múltiples hablantes**

#### Hardware:
- **CPU**: Intel Core i9 o AMD Ryzen 9 (8+ cores, 16+ threads)
- **GPU**: NVIDIA RTX 4090 o RTX 4080 (24GB VRAM)
- **RAM**: 64GB DDR5
- **Almacenamiento**: 1TB NVMe SSD
- **Sistema Operativo**: Ubuntu 22.04 LTS o Windows 11 Pro

#### Modelos a usar:
- **Whisper**: `large-v3` (1550MB) - Máxima precisión
- **Pyannote**: `speaker-diarization-3.1` con GPU

#### Rendimiento esperado:
- Archivos de 3+ horas: 20-30 minutos de procesamiento
- Precisión: 95-98% en condiciones óptimas
- Identificación de hasta 20 hablantes simultáneos

---

### 💪 Configuración Profesional (Balance Calidad/Velocidad)
**Para uso empresarial regular**

#### Hardware:
- **CPU**: Intel Core i7 o AMD Ryzen 7 (6+ cores)
- **GPU**: NVIDIA RTX 3070 o superior (8GB VRAM)
- **RAM**: 32GB DDR4/DDR5
- **Almacenamiento**: 500GB NVMe SSD
- **Sistema Operativo**: Windows 10/11 o Ubuntu 20.04+

#### Modelos a usar:
- **Whisper**: `medium` (769MB) - Excelente balance
- **Pyannote**: Habilitado con GPU

#### Rendimiento esperado:
- Archivos de 2 horas: 30-45 minutos de procesamiento
- Precisión: 92-95%
- Identificación de hasta 10 hablantes

---

### 💻 Configuración Estándar (Uso Personal)
**Para archivos medianos con buena calidad**

#### Hardware:
- **CPU**: Intel Core i5 o AMD Ryzen 5 (4+ cores)
- **GPU**: NVIDIA GTX 1660 o superior (6GB VRAM) - Opcional
- **RAM**: 16GB DDR4
- **Almacenamiento**: 256GB SSD
- **Sistema Operativo**: Windows 10 o Ubuntu 20.04

#### Modelos a usar:
- **Whisper**: `small` (244MB) o `base` (74MB)
- **Pyannote**: Habilitado si hay GPU

#### Rendimiento esperado:
- Archivos de 1 hora: 20-30 minutos de procesamiento
- Precisión: 85-92%
- Identificación de hasta 5 hablantes

---

### 📱 Configuración Mínima (Funcional)
**Para archivos cortos y uso ocasional**

#### Hardware:
- **CPU**: Intel Core i3 o AMD Ryzen 3 (2+ cores)
- **GPU**: No requerida (usa CPU)
- **RAM**: 8GB DDR4
- **Almacenamiento**: 128GB SSD
- **Sistema Operativo**: Windows 10 o Ubuntu 18.04

#### Modelos a usar:
- **Whisper**: `tiny` (39MB) o `base` (74MB)
- **Pyannote**: Deshabilitado para archivos largos

#### Rendimiento esperado:
- Archivos de 30 minutos: 15-20 minutos de procesamiento
- Precisión: 75-85%
- Sin identificación de hablantes en archivos largos

---

## Comparación de Modelos Whisper

| Modelo | Tamaño | VRAM Requerida | Velocidad Relativa | Precisión | Uso Recomendado |
|--------|--------|----------------|-------------------|-----------|-----------------|
| tiny | 39 MB | ~1 GB | 32x | 75-80% | Subtítulos rápidos |
| base | 74 MB | ~1 GB | 16x | 80-85% | Transcripción básica |
| small | 244 MB | ~2 GB | 6x | 85-90% | Uso general |
| medium | 769 MB | ~5 GB | 2x | 90-93% | Profesional |
| large-v2 | 1550 MB | ~10 GB | 1x | 93-95% | Máxima calidad |
| large-v3 | 1550 MB | ~10 GB | 1x | 95-97% | Estado del arte |

---

## Optimizaciones de Rendimiento

### Con GPU NVIDIA:
```python
# En app.py, cambiar:
device = "cuda" if torch.cuda.is_available() else "cpu"
model = whisper.load_model('large-v3', device=device)
```

### Procesamiento por lotes:
```python
# Para múltiples archivos
batch_size = 4  # Ajustar según RAM disponible
```

### Configuración de Docker (Recomendado para producción):
```dockerfile
FROM nvidia/cuda:11.8.0-cudnn8-runtime-ubuntu22.04
# Instalación optimizada con soporte GPU
```

---

## Requisitos de Software

### Dependencias del Sistema:
- Python 3.8-3.11
- FFmpeg 4.4+
- CUDA Toolkit 11.8+ (para GPU)
- cuDNN 8.6+ (para GPU)

### Librerías Python principales:
- torch>=2.0.1 (con CUDA si hay GPU)
- openai-whisper==20231117
- pyannote.audio==3.1.1
- transformers>=4.35.0
- accelerate>=0.24.0

---

## Estimación de Tiempos de Procesamiento

### Archivo de 2 horas (120 minutos):

| Configuración | Modelo Whisper | Con GPU | Tiempo Estimado |
|---------------|----------------|---------|-----------------|
| Óptima | large-v3 | Sí | 15-20 min |
| Profesional | medium | Sí | 25-35 min |
| Estándar | small | Opcional | 40-60 min |
| Mínima | base | No | 90-120 min |

### Factores que afectan el rendimiento:
1. **Calidad del audio**: Audio limpio procesa más rápido
2. **Número de hablantes**: Más hablantes = más tiempo de diarización
3. **Idioma**: Algunos idiomas son más complejos de procesar
4. **Ruido de fondo**: Aumenta el tiempo de procesamiento

---

## Recomendaciones Específicas

### Para Podcasts/Entrevistas:
- Usar configuración **Profesional** con `medium` model
- Habilitar diarización (2-4 hablantes)
- RAM mínima: 32GB

### Para Conferencias/Webinars:
- Usar configuración **Óptima** con `large-v3`
- Diarización para múltiples hablantes
- GPU dedicada recomendada

### Para Notas de Voz Personales:
- Configuración **Estándar** suficiente
- Modelo `small` o `base`
- 16GB RAM suficiente

### Para Transcripción Masiva:
- Configuración **Óptima** con múltiples GPUs
- Considerar solución en la nube (AWS/GCP)
- Implementar cola de procesamiento

---

## Servicios en la Nube Alternativos

Si no tienes el hardware necesario:

1. **Google Colab Pro+**: $49.99/mes
   - GPU T4/V100
   - 52GB RAM
   - Ideal para pruebas

2. **AWS EC2 p3.2xlarge**: ~$3/hora
   - GPU V100
   - 61GB RAM
   - Para procesamiento intensivo

3. **Paperspace Gradient**: Desde $8/mes
   - Varias opciones de GPU
   - Bueno para desarrollo

4. **RunPod**: Desde $0.2/hora
   - RTX 3090/4090
   - Económico para uso ocasional