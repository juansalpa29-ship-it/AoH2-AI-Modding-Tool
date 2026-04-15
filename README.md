# Guía Rápida para Agentes: Creación de Eventos en Age of History 2

Este es un tutorial paso a paso para que cualquier agente de IA pueda utilizar el `EventInjector` y las herramientas asociadas para añadir un nuevo evento a un escenario existente. Sigue las instrucciones al pie de la letra.

**PRINCIPIO FUNDAMENTAL: Nunca modifiques un archivo de eventos existente. Siempre borra y re-crea.**

---

### **CÓMO PROCESAR UNA SOLICITUD DE CREACIÓN DE EVENTOS**

**PASO 0: VERIFICACIÓN DEL ENTORNO**
- Antes de nada, comprueba si existe el archivo `project_config.json`.
- Si no existe, debes pedírselo al usuario y crearlo tú mismo. Consulta la sección 0 del `AoH2_Modding_Skill.md` para el protocolo exacto. **No procedas hasta que las rutas estén configuradas.**

**PASO 1: LEER TODOS LOS EVENTOS EXISTENTES**
- Usa las rutas del `project_config.json` para localizar el escenario solicitado (ej. SGM).
- Utiliza la herramienta para decodificar el archivo de eventos (`..._E`) y guarda su contenido en una variable o archivo JSON temporal.

**PASO 2: DISEÑAR EL NUEVO EVENTO**
- Basado en la petición del usuario, diseña el nuevo evento en tu memoria.
- Sigue las reglas del `AoH2_Modding_Skill.md` (UTF-8, `iAIChance`, IDs de civilización, etc.).
- **Ejemplo de diseño mental:**
  - **Evento:** "La Guerra de Invierno"
  - **Receptor:** URSS (ID 6 del escenario WWII)
  - **Decisiones:** "Atacar Finlandia" (AIChance 100) vs "Esperar" (AIChance 15).

**PASO 3: PREPARAR LA COMPILACIÓN TOTAL (EL PASO CLAVE)**
- Construye una **LISTA COMPLETA** en tu memoria que contenga:
  1. Todos los eventos leídos en el PASO 1.
  2. Tu nuevo evento diseñado en el PASO 2.

**PASO 4: EJECUTAR LA COMPILACIÓN FORZADA**
- Ejecuta el `EventInjector.java` con una orden para **reconstruir desde cero** el archivo de eventos del escenario.
- Pásale la lista completa que creaste en el PASO 3.
- **Ejemplo de comando conceptual:** `java EventInjector -rebuild -scenarioPath [ruta_completa_al_escenario] -inputData [lista_completa_de_eventos_en_formato_json]`

**RESUMEN DEL FLUJO A PRUEBA DE FALLOS:**
1. **CONFIGURA** si es la primera vez.
2. **DECODIFICA** lo que ya existe.
3. **DISEÑA** lo nuevo.
4. **COMBINA** lo viejo y lo nuevo en una lista total.
5. **RECOMPILA** desde cero usando esa lista.