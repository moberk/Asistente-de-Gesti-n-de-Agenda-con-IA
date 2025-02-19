# 🗓️ Asistente de Gestión de Agenda con IA

## 📌 Descripción General
Este repositorio contiene una automatización en **Make (Integromat)** que permite gestionar una agenda personal mediante la integración con **Google Calendar** y **OpenAI GPT**.  

El asistente es capaz de **crear, modificar, eliminar y consultar eventos** en el calendario mediante lenguaje natural, proporcionando una experiencia fluida y automatizada para los usuarios.

---

## 🚀 Características Principales
✅ **Integración con Google Calendar y OpenAI GPT**  
✅ **Gestión de eventos en lenguaje natural**  
✅ **Detección y resolución de conflictos de horario**  
✅ **Corrección automática de fechas relativas ("mañana", "próximo jueves", etc.)**  
✅ **Flujo optimizado para evitar falsos conflictos de fechas**  
✅ **Formato de respuesta en JSON para fácil integración**  

---

## 📥 Instalación

### 🔹 **1. Importar el Blueprint en Make**
1. Accede a [Make (Integromat)](https://www.make.com/).
2. Crea un nuevo escenario en Make.
3. Haz clic en **Importar un Blueprint**.
4. Selecciona el archivo JSON:  
   ```plaintext
   blueprint (10).json
   ```
5. Haz clic en **Importar**.

---

### 🔹 **2. Configurar las Cuentas de Google y OpenAI**
#### **🔹 Google Calendar**
- Accede al módulo de **Google Calendar** dentro de Make.
- Selecciona o añade una cuenta de Google con permisos para leer y escribir eventos.
- Asegúrate de que el **ID del calendario** está correctamente configurado.

#### **🔹 OpenAI (GPT-4o)**
- Accede al módulo de **OpenAI ChatGPT** dentro de Make.
- Conéctalo con una cuenta de OpenAI con acceso a la API de GPT-4.
- Configura los parámetros como:
  ```plaintext
  response_format = json_object
  ```
  para garantizar respuestas en formato JSON.

---

## 🛠️ **Configuración de la Cuenta de Google**
Si necesitas cambiar la cuenta de Google asociada:
1. Dirígete a **Google Calendar** en Make.
2. En el módulo de conexión, haz clic en **Administrar conexiones**.
3. Elimina la conexión actual y agrega una nueva cuenta con permisos de acceso al calendario.
4. Asegúrate de que el ID del calendario en la configuración del módulo coincida con el de tu cuenta.

---

## 📖 **Guía Rápida de Uso**
El asistente responde a comandos en lenguaje natural. Aquí algunos ejemplos:

### **1️⃣ Crear un Evento**
📥 **Entrada:**  
"Agendar reunión con Juan el próximo jueves a las 13 hrs."

📤 **Salida esperada:**
```json
{
   "disponibilidad": "Disponible",
   "razon": "No hay eventos en conflicto en el horario solicitado.",
   "evento": "Reunión con Juan",
   "fechaHoraInicio": "20/02/2025 13:00",
   "fechaHoraFin": "20/02/2025 14:00"
}
```

---

### **2️⃣ Modificar un Evento**
📥 **Entrada:**  
"Quiero mover la sesión de estudio de mañana para el jueves a la misma hora."

📤 **Salida esperada:**
```json
{
   "status": "evento_unico",
   "evento": {
      "summary": "Sesión de estudio",
      "fechaHoraInicio": "19/02/2025 12:00",
      "fechaHoraFin": "19/02/2025 13:00"
   }
}
```

---

### **3️⃣ Consultar Eventos**
📥 **Entrada:**  
"Dime las sesiones que tengo hoy."

📤 **Salida esperada:**
```json
{
   "status": "multiples_eventos",
   "eventos": [
      {
         "summary": "Sesión de estudio",
         "fechaHoraInicio": "19/02/2025 12:00",
         "fechaHoraFin": "19/02/2025 13:00"
      },
      {
         "summary": "Reunión de equipo",
         "fechaHoraInicio": "19/02/2025 15:00",
         "fechaHoraFin": "19/02/2025 16:00"
      }
   ]
}
```

---

### **4️⃣ Eliminar un Evento**
📥 **Entrada:**  
"Elimina mi cita con el dentista de esta semana."

📤 **Salida esperada:**
```json
{
   "status": "evento_unico",
   "evento": {
      "summary": "Cita con el dentista",
      "fechaHoraInicio": "22/02/2025 10:00",
      "fechaHoraFin": "22/02/2025 11:00"
   }
}
```

---

## 📌 **Consideraciones Finales**
✅ **Corrección de Fechas Relativas**: El sistema interpreta términos como `"mañana"`, `"este jueves"`, `"la próxima semana"` y los convierte en fechas exactas.  
✅ **Formato JSON Limpio y Compatible**: Todas las respuestas siguen un formato JSON estándar para facilitar la integración.  
✅ **Manejo de Conflictos**: Si hay un evento en conflicto, se sugiere un horario alternativo.  
✅ **Configuración Personalizable**: Puedes cambiar la cuenta de Google o modificar los parámetros de OpenAI en Make sin afectar la estructura general del flujo.  

---

## ❓ **Preguntas Frecuentes**
### 1️⃣ **¿Cómo cambio la cuenta de Google Calendar?**
Ve a **Make > Módulo de Google Calendar > Administrar conexiones**, elimina la cuenta actual y conecta la nueva.

### 2️⃣ **¿Cómo sé si un evento se programó correctamente?**
El asistente siempre responde en formato JSON con `"disponibilidad": "Disponible"` si el evento se ha programado sin conflictos.

### 3️⃣ **¿Qué pasa si hay un conflicto de horario?**
Si el asistente detecta un evento en el mismo horario, responderá con:
```json
{
   "disponibilidad": "Conflicto",
   "razon": "Conflicto con evento existente.",
   "eventoConflicto": "Sesión de estudio",
   "fechaHoraInicioConflicto": "19/02/2025 12:00",
   "fechaHoraFinConflicto": "19/02/2025 13:00"
}
```
Para resolverlo, intenta cambiar la hora o consultar primero tu agenda.

---

## 📌 **Contribuciones y Mejoras**
Si deseas mejorar el asistente, revisa la estructura del flujo en Make e implementa optimizaciones en:
- **Refinamiento de clasificación de mensajes**
- **Mejor manejo de fechas y horas en diferentes zonas horarias**
- **Automatización para sugerencias de reprogramación**

---

## 📬 **Soporte**
Si encuentras problemas con la implementación, abre un **Issue** en este repositorio o revisa la documentación oficial de **Make** y **OpenAI API**.

📌 **Repositorio en GitHub**  
Este proyecto está diseñado para optimizar la gestión de agendas con IA y Google Calendar. ¡Aporta mejoras y optimizaciones a la comunidad! 🚀

---

🔹 **Desarrollado con ❤️ y tecnología IA para facilitar la gestión de tu tiempo.** 🕒✨
