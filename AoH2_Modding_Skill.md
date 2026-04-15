# 📖 Manual de Habilidades: Modding de Eventos para AoH2

Este documento define el protocolo completo para operar con los archivos de escenarios de Age of History 2.

---

## 0. PROTOCOLO DE INICIALIZACIÓN Y GESTIÓN DE RUTAS

**PRIORIDAD MÁXIMA:** Antes de ejecutar cualquier tarea de modding, debes verificar tu entorno de trabajo.

1.  **Verificar Configuración:** Busca un archivo llamado `project_config.json` en el directorio raíz de este proyecto.
2.  **Si `project_config.json` EXISTE Y ES VÁLIDO:** Lee las rutas `game_path` y `project_path` de este archivo. Procede a la tarea solicitada.
3.  **Si `project_config.json` NO EXISTE O ESTÁ VACÍO:**
    a.  **Activa el "Modo de Configuración Inicial"**.
    b.  **Comunícate con el usuario** en lenguaje natural y pídele la siguiente información:
        - "Para configurar el entorno por primera vez, necesito que me proporciones la ruta completa a la carpeta principal de tu juego Age of History II."
        - "Ahora, por favor, dame la ruta completa a la carpeta donde has guardado este proyecto."
    c.  **Crea el archivo `project_config.json`** en el directorio raíz del proyecto.
    d.  **Escribe las rutas** proporcionadas por el usuario en el archivo con el siguiente formato:
        ```json
        {
          "game_path": "RUTA_PROPORCIONADA_POR_EL_USUARIO_AL_JUEGO",
          "project_path": "RUTA_PROPORCIONADA_POR_EL_USUARIO_AL_PROYECTO"
        }
        ```
    e.  Informa al usuario: "¡Configuración completada! Ahora puedo proceder con tu solicitud."
    f.  Reintenta la tarea original usando las rutas recién guardadas.

> **REGLA DE SEGURIDAD:** Todas las operaciones de lectura y escritura de archivos deben estar limitadas a las rutas definidas en `project_config.json`. Está estrictamente prohibido acceder a cualquier otro directorio del sistema del usuario.

---

## 1. FLUJO DE TRABAJO ESENCIAL: RECONSTRUIR, NO MODIFICAR

Para evitar la corrupción de datos en los archivos binarios del juego, el único método seguro y aprobado es:

1.  **DECODIFICAR:** Lee el archivo de eventos (`..._E`) del escenario objetivo y conviértelo a un formato legible (JSON).
2.  **DISEÑAR:** Crea el nuevo evento en memoria, siguiendo las reglas de este manual.
3.  **CONSTRUIR:** Crea una lista completa en memoria que contenga **TODOS** los eventos originales más el nuevo que has diseñado.
4.  **RECOMPILAR:** Usa `EventInjector.java` para borrar el archivo de eventos binario antiguo y crear uno nuevo desde cero usando la lista completa del paso anterior.

---

## 2. REGLAS TÉCNICAS

### 2.1. Codificación de Caracteres
- La herramienta `EventInjector.java` soporta codificación **UTF-8**.
- **OBLIGATORIO:** Al crear textos para los eventos, utiliza siempre la gramática y ortografía correctas en español, incluyendo tildes (á, é, í, ó, ú), eñes (ñ) y signos de puntuación (¡, ¿).

### 2.2. Lógica de Probabilidades de la IA (`iAIChance`)
- Para garantizar que la IA siempre tome una decisión en un evento, una de las opciones **DEBE** tener `iAIChance: 100`.
- Las demás opciones pueden tener un valor entre `1` y `99`. La IA las evaluará en orden. La opción con `100` actúa como "fallback" si las otras fallan su tirada de probabilidad.
- **Ejemplo correcto:**
  - Decisión A: `iAIChance: 15` (15% de probabilidad).
  - Decisión B: `iAIChance: 100` (Opción por defecto si la A falla).

---

## 3. GUÍA DE IDs DE CIVILIZACIONES

### WWI - 1914 (1773099385339vorscbyt) (Escenario no vanilla)
| ID | Tag | Civilización |
|----|-----|-----------------------------|
| 1 | fra_r | Francia |
| 2 | spa_m | España |
| 3 | por_r | Portugal |
| 4 | uni_m | Reino Unido |
| 5 | ita_m | Italia |
| 6 | auhu_m | Imperio Austrohúngaro |
| 7 | ger_m | Imperio Alemán |
| 8 | net_m | Países Bajos |
| 9 | bel_m | Bélgica |
| 10 | lux_m | Luxemburgo |
| 11 | gre_m | Grecia |
| 12 | bul_m | Segundo Imperio Búlgaro |
| 13 | ser_m | Serbia |
| 14 | alb2_m | Albania |
| 15 | rom_m | Rumania |
| 16 | rus2_m | Imperio Ruso |
| 17 | nor_m | Noruega |
| 18 | den_m | Dinamarca |
| 19 | swe_m | Suecia |
| 20 | tur_m | Imperio Otomano |
| 21 | swi_r | Suiza |
| 22 | mot_m | Montenegro |
| 23 | and_m | Andorra |
| 24 | moc_m | Mónaco |
| 25 | jsh_t | Emirato de Yabal Shammar |
| 26 | nejd_t | Emirato de Nechd |
| 28 | afg_m | Afganistán |
| 29 | lii_r | Liberia |
| 30 | eth_m | Imperio Etíope |
| 31 | soa_m | Unión Sudafricana |
| 32 | nep_m | Nepal |
| 33 | bhu_m | Bután |
| 34 | jap_m | Imperio del Japón |
| 35 | tha2_m | Tailandia |
| 36 | tann_h | República de Tuvá |
| 37 | mon_h | Mongolia |
| 38 | tib_r | Tíbet |
| 39 | chi_r | República de China |
| 40 | aus_m | Australia |
| 41 | usa_r | Estados Unidos |
| 42 | mex_r | México |
| 43 | gua_r | Guatemala |
| 44 | els_r | El Salvador |
| 45 | nic_r | Nicaragua |
| 46 | cor_r | Costa Rica |
| 47 | hou_r | Honduras |
| 48 | pan_r | Panamá |
| 49 | cub_r | Cuba |
| 50 | hai_r | Haití |
| 51 | dom_r | República Dominicana |
| 52 | col_r | Colombia |
| 53 | ecu_r | Ecuador |
| 54 | per_r | Perú |
| 55 | ven_r | Venezuela |
| 56 | bra_r | Brasil |
| 57 | uru_r | Uruguay |
| 58 | arg_r | Argentina |
| 59 | chl_r | Chile |
| 60 | bol_r | Bolivia |
| 61 | par_r | Paraguay |
| 62 | dox_m | Canadá |
| 63 | nez_m | Nueva Zelanda |
| 176 | qaja_m | Dinastía Kayar |

### WWII - 1936 (worldwar2) (escenario vanilla)
| ID | Tag | Civilización |
|----|-----|---------------|
| 2 | ger_f | Alemania Nazi |
| 7 | pol | Polonia |
| 6 | rus_c | Unión Soviética |
| 1 | ita_f | Italia |
| 23 | fra | Francia |
| 3 | uni_m | Reino Unido |
| 4 | spa | Segunda República Española |
| 12 | atr | Austria |
| 13 | hun | Hungría |
| 11 | czsl | Checoslovaquia |
| 18 | rom_m | Rumania |
| 17 | bul_m | Segundo Imperio Búlgaro |
| 14 | alb | Albania |
| 15 | gre_m | Grecia |
| 16 | tur | Turquía |
| 9 | yugo_m | Yugoslavia |
| 10 | swi | Suiza |
| 22 | den_m | Dinamarca |
| 20 | net_m | Países Bajos |
| 21 | bel_m | Bélgica |
| 19 | lux | Luxemburgo |
| 26 | nor_m | Noruega |
| 25 | swe_m | Suecia |
| 24 | fin | Finlandia |
| 28 | est | Estonia |
| 27 | lat | Letonia |
| 29 | lit | Lituania |
| 37 | fcd | Ciudad libre de Danzig |
| 5 | por | Portugal |
| 8 | ire | Irlanda |
| 45 | jap_f | Japón |
| 49 | man_f | Manchukuo |
| 48 | mon_c | Mongolia |
| 47 | tann_c | República Popular de Tannu Tuvá |
| 77 | qin_f | República de China |
| 83 | chi_c | República Popular China |
| 82 | sqy | Shanxi |
| 79 | guag | Guangxi |
| 78 | yucl | Camarilla de Yunnan |
| 50 | meng_f | Mengjiang |
| 80 | xij | Sinkiang |
| 81 | xib | Xibei San Ma |
| 55 | tib | Tíbet |
| 52 | tha2 | Tailandia |
| 53 | bhu_m | Bután |
| 54 | nep_m | Nepal |
| 38 | brra_m | Raj británico |
| 85 | max_m | Malasia Británica |
| 57 | duin | Indias Orientales Neerlandesas |
| 51 | phi | Filipinas |
| 44 | soa_m | Unión Sudafricana |
| 35 | eth_m | Imperio Etíope |
| 34 | oma2 | Omán |
| 32 | sau_m | Arabia Saudita |
| 36 | lii | Liberia |
| 46 | afg | Afganistán |
| 30 | ira | Irak |
| 31 | irq_m | Irak (régimen) |
| 33 | egy | Egipto |
| 39 | usa_r | Estados Unidos |
| 84 | dox_m | Canadá |
| 42 | aus_m | Australia |
| 56 | nez_m | Nueva Zelanda |
| 43 | mex | México |
| 59 | cub | Cuba |
| 58 | gua | Guatemala |
| 60 | hai | Haiti |
| 61 | dom | República Dominicana |
| 64 | els | El Salvador |
| 65 | hou | Honduras |
| 66 | nic | Nicaragua |
| 67 | cor | Costa Rica |
| 68 | pan | Panamá |
| 62 | col | Colombia |
| 63 | ecu | Ecuador |
| 69 | ven | Venezuela |
| 70 | per | Perú |
| 71 | bol | Bolivia |
| 72 | chl | Chile |
| 73 | arg | Argentina |
| 74 | uru | Uruguay |
| 75 | par | Paraguay |
| 76 | bra | Brasil |

---

*Documento actualizado: 15 de abril, 2026*
*Juego: Age of Civilizations 2 (AoC2) / Age of History 2*
