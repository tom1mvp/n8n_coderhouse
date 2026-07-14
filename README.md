# Agent AI para Automatización Dinámica de Gastos en Google Sheets con n8n

Este repositorio contiene la estructura completa de un flujo avanzado de automatización implementado en **n8n**, diseñado para operar como un Agente de Inteligencia Artificial (AI Agent) autónomo. El sistema procesa peticiones en lenguaje natural desde un canal de chat, extrayendo dinámicamente variables e insertando registros estructurados directamente en Google Sheets.

## Arquitectura y Componentes del Flujo

El flujo está compuesto por los siguientes nodos principales interconectados:
1. **Chat Trigger ("When chat message received"):** Punto de entrada del webhook que captura el mensaje del usuario (`chatInput`) y maneja el estado de la sesión (`sessionId`).
2. **AI Agent (Advanced AI):** Nodo central que gestiona el lazo de razonamiento (Reasoning Loop) del modelo.
3. **OpenAI Chat Model (GPT-4o):** El cerebro cognitivo encargado de la interpretación semántica y toma de decisiones.
4. **Google Sheets Tool ("Create spreadsheet"):** Herramienta otorgada al agente para crear nuevos libros y pestañas personalizadas en tiempo real de forma dinámica.
5. **Google Sheets Tool ("Append row"):** Herramienta utilizada para el parseo y persistencia de filas de datos limpios.

## Capacidades Dinámicas Clave

A diferencia de los flujos deterministas rígidos, este Agente de IA cuenta con:
* **Mapeo Automatizado por Parámetros (From AI):** Los campos `Title` del documento y la pestaña destino están configurados en modo dinámico (`Defined automatically by the model`). Esto le permite al Agente de IA leer el chat, aislar las entidades solicitadas por el usuario (ej: *"archivo: gastos, hoja: gastos junio 2026"*) y setearlas dinámicamente en las propiedades de la API de Google sin intervención de variables cableadas (*hardcoded*).
* **Protocolo de Limpieza de Payload:** El prompt del sistema bloquea activamente la inyección de metadatos del flujo (`sessionId`, `action`, etc.) en las celdas de datos finales, asegurando matrices de información completamente normalizadas.

## Contenido del Repositorio

* `checkpoint1_thomas_bratik.json`: Archivo con la exportación del workflow listo para ser importado.
* `README.md`: Documentación técnica del proyecto.

## Instrucciones de Despliegue e Importación

1. Descarga el archivo `.json` de este repositorio.
2. Abre tu instancia de **n8n**.
3. En el lienzo de trabajo, ve al menú superior derecho (`...`) y selecciona **Import from file...**.
4. Selecciona el archivo `.json` descargado.
5. Configura las credenciales requeridas para tus nodos conectados:
   * **OpenAI account** (API Key con acceso a `gpt-4o`).
   * **Google Sheets OAuth2 API** (Cuenta de Google con permisos de lectura/escritura en Drive).
6. Presiona **Publish** en la esquina superior derecha para activar el Webhook del chat.
