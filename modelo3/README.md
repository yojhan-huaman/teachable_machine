# Detector de Sueño con Inteligencia Artificial  
Versión documentada y en modo oscuro

Este proyecto implementa un sistema de detección de sueño utilizando un modelo de postura (Pose Model) entrenado en Teachable Machine.  
La Inteligencia Artificial analiza la postura corporal en tiempo real utilizando la cámara del dispositivo para determinar si el usuario se encuentra:

- Despierto  
- Dormido  

Todo el procesamiento ocurre directamente en el navegador, sin enviar información a servidores externos.

---

# Descripción General

Este sistema utiliza un modelo de reconocimiento de postura basado en **PoseNet** y **Teachable Machine**, capaz de detectar si el usuario está dormido o despierto según las posiciones clave de su cuerpo.  
El sistema muestra un estado visual, reproduce audio en caso de detectar sueño y expone las probabilidades de cada clase dentro de la interfaz.

---

# Funcionamiento Interno

El flujo del sistema sigue estos pasos:

1. Carga del modelo desde `model.json` y `metadata.json`.
2. Inicialización de la cámara mediante WebRTC.
3. Render del video en un canvas de 300 × 300 píxeles.
4. Estimación de postura utilizando PoseNet.
5. Extracción de puntos clave.
6. Envío de la información al modelo de clasificación.
7. Evaluación de probabilidades de las clases:
   - Despierto  
   - Dormido  
8. Aplicación de las reglas:
   - Si la clase “Dormido” supera 0.90 → alarma sonora.
   - Si la clase “Despierto” supera 0.90 → estado estable.
9. Visualización del estado en un cuadro dinámico.
10. Dibujo de la pose y el esqueleto sobre el canvas.

Todo este proceso se ejecuta constantemente mediante `requestAnimationFrame`.

---

# Datos del Modelo

```json
{
    "tfjsVersion": "1.7.4",
    "tmVersion": "0.8.6",
    "packageVersion": "0.8.6",
    "packageName": "@teachablemachine/pose",
    "timeStamp": "2025-11-20T04:51:48.155Z",
    "userMetadata": {},
    "modelName": "my-pose-model",
    "labels": [
        "Despierto",
        "Dormido"
    ],
    "modelSettings": {
        "posenet": {
            "architecture": "MobileNetV1",
            "outputStride": 16,
            "inputResolution": 257,
            "multiplier": 0.75
        }
    }
}