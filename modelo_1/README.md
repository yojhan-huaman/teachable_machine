# Panel de Control IA – Reconocimiento de Usuario  
Versión ampliada y documentada

Este proyecto implementa un panel de control para reconocimiento de usuarios mediante un modelo de Teachable Machine (Image Model) utilizando TensorFlow.js.  
El sistema procesa video en tiempo real desde la cámara del dispositivo, calcula las probabilidades de clasificación y reproduce mensajes de voz basados en la detección.

---

# Descripción General

Este panel permite reconocer usuarios previamente entrenados en un modelo de Teachable Machine.  
Si el sistema identifica correctamente a un usuario, anuncia por voz “Bienvenido [nombre]”.  
Si ninguna clase alcanza el umbral mínimo de probabilidad, se activa la clasificación “Usuario No Identificado” y el sistema reproduce “Usuario no identificado”.

El proyecto incluye herramientas adicionales como canvas de vista previa, control de cámara, inversión de video, fotografía instantánea y visualización de probabilidades.

---

# Funcionamiento Interno

El sistema sigue este flujo:

1. Carga el modelo Teachable Machine (JSON, Metadata y Pesos).
2. Inicializa la cámara mediante WebRTC.
3. Toma fotogramas en tiempo real.
4. Envía el cuadro actual al modelo para obtener predicciones.
5. Ordena las predicciones de mayor a menor probabilidad.
6. Selecciona la clase con mayor probabilidad.
7. Compara la probabilidad con un umbral:
   - Si es mayor o igual a 0.85 → Usuario identificado.
   - Si es menor a 0.85 → Usuario No Identificado.
8. Reproduce el mensaje correspondiente usando SpeechSynthesis.
9. Actualiza la interfaz:
   - Nombre detectado
   - Probabilidad
   - Lista completa de predicciones
   - Estado visual por colores
   - Vista previa sobre canvas
10. Repite el ciclo en animación continua.

El procesamiento ocurre en el navegador, sin enviar datos a servidores externos.

---

# Datos del Modelo

```json
{
    "tfjsVersion": "1.7.4",
    "tmVersion": "2.4.10",
    "packageVersion": "0.8.4-alpha2",
    "packageName": "@teachablemachine/image",
    "timeStamp": "2025-11-20T05:27:06.107Z",
    "userMetadata": {},
    "modelName": "tm-my-image-model",
    "labels": [
        "Yojhan Deyvis Huaman Huaman",
        "Vacio"
    ],
    "imageSize": 224
}