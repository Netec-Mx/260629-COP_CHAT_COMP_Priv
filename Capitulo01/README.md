# Uso de IA para la interpretación de leyes, reglamentos y reformas laborales (IMSS, Infonavit, LFT). Creación de agentes de consulta para soporte legal y análisis de impacto en nóminas.

---

## 1. Metadatos

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 60 minutos |
| **Complejidad** | Media |
| **Nivel Bloom** | Crear |
| **Módulo** | Capítulo 1 — Consulta Normativa y Legal con IA |
| **Lección relacionada** | 1.1 Objetivos del Capítulo / 1.2 Cumplimiento Normativo Inteligente |
| **Modalidad** | Individual con validación en equipo |

---

## 2. Descripción General

Esta práctica introduce al participante en el uso de Microsoft 365 Copilot como asistente normativo inteligente para el área de compensaciones. A lo largo de dos grandes bloques de trabajo, el participante aprenderá a formular prompts estructurados en Copilot (Word y chat) para interpretar artículos clave de la Ley Federal del Trabajo (LFT), reglamentos del IMSS e Infonavit, y a evaluar el impacto de reformas laborales recientes en conceptos críticos de nómina como aguinaldo, prima vacacional, PTU y cuotas obrero-patronales.

En la segunda mitad de la práctica, el participante creará un agente de consulta legal básico en Microsoft Copilot Studio, configurando temas conversacionales predefinidos con base en documentos normativos cargados en SharePoint. El agente se probará dentro del entorno de Copilot Studio y se publicará en Microsoft Teams, completando así un flujo de soporte legal automatizado que reduce la carga de consultas repetitivas al equipo de compensaciones.

> ⚠️ **Aviso de cumplimiento:** Todos los datos utilizados en esta práctica son ficticios o de dominio público (textos normativos oficiales). Está estrictamente prohibido ingresar datos reales de empleados en cualquier herramienta de Microsoft 365 durante este laboratorio, en cumplimiento con la LFPDPPP.

---

## 3. Objetivos de Aprendizaje

Al finalizar esta práctica, el participante será capaz de:

- [ ] **Formular prompts estructurados** en Microsoft 365 Copilot (chat y Word) para obtener interpretaciones precisas de artículos de la LFT, LSS e Infonavit relevantes para el cálculo de nómina.
- [ ] **Generar un análisis de impacto normativo** en formato de resumen ejecutivo en Word, identificando las implicaciones de reformas laborales recientes en conceptos de compensación (aguinaldo, PTU, prima vacacional, cuotas obrero-patronales).
- [ ] **Crear un agente de consulta legal básico** en Microsoft Copilot Studio con al menos tres temas conversacionales funcionales, utilizando documentos normativos de SharePoint como base de conocimiento.
- [ ] **Publicar y validar el agente** en Microsoft Teams, verificando que responde correctamente a preguntas frecuentes sobre cumplimiento normativo IMSS, Infonavit y LFT.
- [ ] **Evaluar críticamente** las respuestas generadas por Copilot, identificando cuándo se requiere validación humana especializada.

---

## 4. Prerrequisitos

### Conocimientos Previos

| Área | Nivel Requerido |
|---|---|
| Navegación en Microsoft 365 (Word, Teams, SharePoint) | Básico |
| Conceptos fundamentales de nómina en México (SBC, IMSS, Infonavit, PTU) | Básico–Intermedio |
| Comprensión general de la Ley Federal del Trabajo | Básico |
| Uso de Microsoft Copilot (chat básico) | Básico |

### Accesos y Licencias Requeridos

| Recurso | Estado Requerido |
|---|---|
| Licencia activa de **Microsoft 365 Copilot** (no Copilot gratuito) | ✅ Activa y asignada |
| Acceso a **Microsoft Copilot Studio** habilitado por el administrador del tenant | ✅ Habilitado con rol "Maker" |
| Acceso al **sitio de SharePoint del curso** con los documentos normativos precargados | ✅ Con permisos de lectura |
| Acceso a **Microsoft Teams** con permisos para instalar aplicaciones | ✅ Habilitado |
| Archivos de práctica distribuidos por el instructor | ✅ Descargados o accesibles en SharePoint |

> 💡 **Nota para el instructor:** Antes de iniciar la práctica, verificar que el sitio de SharePoint del curso contenga las siguientes carpetas y archivos en la biblioteca de documentos:
> - `/Modulo1/Normativos/LFT_Vigente_Ficticio.pdf`
> - `/Modulo1/Normativos/LSS_Cuotas_IMSS_2024_Ficticio.pdf`
> - `/Modulo1/Normativos/Infonavit_Tabla_Aportaciones_Ficticio.pdf`
> - `/Modulo1/Normativos/Reforma_Subcontratacion_Resumen_Ficticio.pdf`

---

## 5. Entorno de Laboratorio

### Hardware Recomendado

| Componente | Mínimo | Recomendado |
|---|---|---|
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| RAM | 8 GB | 16 GB |
| Almacenamiento libre | 10 GB | 20 GB |
| Conexión a internet | 10 Mbps | 25 Mbps |
| Resolución de pantalla | 1366×768 | 1920×1080 |

### Software Necesario

| Aplicación | Versión Mínima | Acceso |
|---|---|---|
| Microsoft Word (M365) | 2308 o superior | Escritorio o web |
| Microsoft Copilot (chat) | Versión actual | microsoft365.com/copilot |
| Microsoft Copilot Studio | Versión actual | copilotstudio.microsoft.com |
| Microsoft SharePoint Online | Versión actual | Portal M365 |
| Microsoft Teams | Versión actual | Escritorio o web |
| Navegador web | Edge 120+ / Chrome 120+ | — |

### Configuración Inicial del Entorno

Antes de comenzar los pasos del laboratorio, ejecutar las siguientes verificaciones:

**Verificación 1 — Confirmar licencia de Copilot activa:**
1. Abrir un navegador y navegar a `https://microsoft365.com`
2. Iniciar sesión con la cuenta corporativa del curso
3. Verificar que en el menú de aplicaciones aparece el ícono de **Copilot** con acceso completo (no la versión limitada)
4. Si Copilot no aparece o muestra funciones limitadas, contactar al administrador de TI antes de continuar

**Verificación 2 — Confirmar acceso a Copilot Studio:**
1. Abrir una nueva pestaña y navegar a `https://copilotstudio.microsoft.com`
2. Iniciar sesión con la misma cuenta corporativa
3. Confirmar que la pantalla de inicio muestra la opción **"Crear un copiloto"** sin mensajes de error de permisos
4. Si aparece un error de acceso, solicitar al administrador la asignación del rol "Maker" en Power Platform

**Verificación 3 — Confirmar acceso a SharePoint del curso:**
1. Navegar al sitio de SharePoint proporcionado por el instructor
2. Confirmar que la carpeta `/Modulo1/Normativos/` es visible y los cuatro archivos PDF están disponibles
3. Descargar localmente el archivo `LFT_Vigente_Ficticio.pdf` como prueba de acceso

---

## 6. Procedimiento Paso a Paso

> 📋 **Estructura de la práctica:**
> - **Bloque A (25 min):** Interpretación normativa con Copilot en Word y chat
> - **Bloque B (30 min):** Creación del agente de consulta legal en Copilot Studio
> - **Validación final (5 min):** Prueba del agente en Teams

---

### BLOQUE A: Interpretación Normativa con Microsoft 365 Copilot

---

### Paso A1 — Consulta Normativa Básica en Microsoft 365 Copilot Chat

**Objetivo:** Familiarizarse con la formulación de prompts estructurados para obtener interpretaciones normativas precisas sobre la LFT, IMSS e Infonavit.

**Instrucciones:**

1. Abrir el navegador y navegar a `https://microsoft365.com/copilot` o hacer clic en el ícono de Copilot en la barra lateral de Microsoft 365.

2. Asegurarse de que el modo de Copilot esté configurado en **"Trabajo"** (no "Web"), para que las respuestas se basen en el contexto organizacional y los documentos del tenant.

3. En el cuadro de chat, ingresar el siguiente prompt estructurado. Copiar y pegar exactamente:

   ```
   Actúa como un especialista en derecho laboral mexicano con experiencia en 
   compensaciones y nómina. Necesito que me expliques los siguientes conceptos 
   conforme a la Ley Federal del Trabajo vigente en México:

   1. ¿Cuál es la fórmula legal para calcular el aguinaldo según el Artículo 87 
      de la LFT?
   2. ¿Qué establece la LFT sobre la prima vacacional (Art. 80) y cuál es el 
      porcentaje mínimo?
   3. ¿Cómo se determina la base de reparto de la PTU conforme al Art. 117-131 
      de la LFT?

   Para cada concepto, incluye: (a) el artículo específico, (b) la fórmula o 
   porcentaje aplicable, y (c) un ejemplo numérico con salario mensual de 
   $15,000 MXN. Indica claramente si algún dato requiere verificación con un 
   especialista legal.
   ```

4. Presionar **Enter** y esperar la respuesta de Copilot (aproximadamente 15-30 segundos).

5. Revisar la respuesta obtenida. Identificar en la respuesta:
   - ¿Copilot citó artículos específicos de la LFT?
   - ¿Los cálculos de ejemplo son coherentes con el salario de $15,000 MXN?
   - ¿Copilot incluyó alguna advertencia sobre validación profesional?

6. Realizar una consulta de seguimiento (follow-up) ingresando el siguiente prompt:

   ```
   Ahora compara el cálculo del aguinaldo que describiste con el siguiente 
   escenario: un empleado que ingresó el 1 de marzo del año en curso y cuyo 
   año fiscal termina el 31 de diciembre. ¿Cómo se aplica el prorrateo? 
   Muestra el cálculo paso a paso.
   ```

7. Documentar ambas respuestas copiándolas en un documento de Bloc de Notas o Word temporal para uso en el Paso A2.

**Resultado Esperado:**

Copilot debe generar una respuesta estructurada que incluya:
- Los tres artículos de la LFT con sus contenidos sustanciales
- Fórmulas de cálculo expresadas matemáticamente
- Ejemplos numéricos coherentes con el salario indicado
- Al menos una nota de advertencia sobre la necesidad de validación legal profesional

**Verificación:**

✅ La respuesta de Copilot menciona al menos los Artículos 87, 80 y 117 de la LFT.
✅ El cálculo de aguinaldo muestra un mínimo de 15 días de salario.
✅ La prima vacacional refleja al menos el 25% sobre el salario de vacaciones.
✅ El prorrateo del aguinaldo en el seguimiento es matemáticamente correcto para el período marzo-diciembre.

---

### Paso A2 — Consulta sobre Cuotas IMSS e Infonavit con Documentos de SharePoint

**Objetivo:** Utilizar Copilot con referencia a documentos normativos específicos cargados en SharePoint para obtener interpretaciones más precisas sobre cuotas obrero-patronales.

**Instrucciones:**

1. Abrir una nueva ventana de Microsoft Word desde `https://word.new` o desde la aplicación de escritorio.

2. En Word, hacer clic en el ícono de **Copilot** en la cinta de opciones (pestaña "Inicio" o "Copilot" si está disponible en la barra lateral derecha).

   > 💡 Si el panel de Copilot no aparece automáticamente, ir a **Vista → Mostrar → Copilot**.

3. En el panel de Copilot dentro de Word, ingresar el siguiente prompt:

   ```
   Necesito crear un documento de referencia rápida para el equipo de 
   compensaciones sobre las aportaciones patronales y obreras al IMSS e 
   Infonavit. Por favor, genera una tabla comparativa con las siguientes 
   columnas:

   - Concepto (ej. Enfermedad y Maternidad, Invalidez y Vida, etc.)
   - Porcentaje Patronal
   - Porcentaje Obrero
   - Base de Cálculo
   - Artículo Legal de Referencia (LSS o Ley Infonavit)

   Incluye todos los ramos del seguro social y la aportación de Infonavit. 
   Al final, agrega una nota sobre el Salario Base de Cotización (SBC) y sus 
   componentes según la Ley del Seguro Social.
   ```

4. Copilot generará el contenido directamente en el documento de Word. Revisar la tabla generada.

5. Agregar el siguiente prompt de refinamiento en el panel de Copilot:

   ```
   Agrega una sección adicional titulada "Impacto en Nómina — Ejemplo Práctico" 
   donde calcules el costo total para el empleador y el descuento total al 
   trabajador para un empleado con SBC de $18,500 MXN mensuales. Presenta los 
   resultados en formato de tabla y calcula el costo laboral total mensual 
   (salario + cuotas patronales).
   ```

6. Una vez que Copilot haya insertado el contenido, revisar los valores numéricos. Verificar que:
   - La aportación de Infonavit patronal sea del 5% sobre el SBC
   - La aportación al IMSS (ramo de Retiro, Cesantía y Vejez) refleje los porcentajes vigentes
   - El cálculo del costo laboral total sea matemáticamente coherente

7. Guardar el documento con el nombre: `Analisis_Cuotas_IMSS_Infonavit_[TuNombre].docx` en la carpeta de OneDrive del curso o en el escritorio local.

**Resultado Esperado:**

El documento de Word debe contener:
- Una tabla de cuotas IMSS con al menos 6 ramos del seguro social
- La aportación de Infonavit (5% patronal)
- Un ejemplo numérico completo con SBC de $18,500 MXN
- Una nota explicativa sobre los componentes del SBC

**Verificación:**

✅ La tabla contiene columnas de porcentaje patronal y obrero diferenciadas.
✅ El ejemplo numérico muestra el cálculo del costo laboral total.
✅ El documento fue guardado correctamente en OneDrive o localmente.
✅ Copilot incluyó referencias a la Ley del Seguro Social (LSS).

---

### Paso A3 — Análisis de Impacto de Reforma Laboral: Subcontratación

**Objetivo:** Generar un resumen ejecutivo accionable sobre el impacto de una reforma laboral reciente en los procesos de nómina, utilizando Copilot en Word con un prompt de análisis estructurado.

**Instrucciones:**

1. En el mismo documento de Word abierto en el Paso A2, posicionar el cursor al final del documento y presionar **Ctrl+Enter** para insertar un salto de página.

2. En el panel de Copilot de Word, ingresar el siguiente prompt de análisis de impacto:

   ```
   Redacta un resumen ejecutivo de 400-500 palabras dirigido al Director de 
   Recursos Humanos sobre el impacto de la Reforma a la Ley Federal del Trabajo 
   en materia de subcontratación laboral (outsourcing), vigente desde abril de 
   2021 en México.

   El resumen debe incluir:
   1. Contexto: ¿Qué cambió con la reforma?
   2. Impacto directo en nómina: ¿Qué conceptos de compensación se ven afectados?
   3. Obligaciones patronales nuevas: menciona el registro en el REPSE
   4. Riesgo de incumplimiento: consecuencias legales y fiscales
   5. Recomendación ejecutiva: 3 acciones concretas para el área de compensaciones

   Usa un tono profesional y ejecutivo. Evita tecnicismos excesivos. 
   Incluye una tabla de "Antes vs. Después" de la reforma en los puntos clave.
   ```

3. Revisar el resumen ejecutivo generado. Evaluar críticamente:
   - ¿El contenido es coherente con lo que conoces sobre la reforma de subcontratación?
   - ¿La tabla "Antes vs. Después" captura los cambios más relevantes?
   - ¿Las recomendaciones son accionables para un área de compensaciones?

4. Si alguna sección necesita ajuste, usar el siguiente prompt de corrección:

   ```
   La sección de "Obligaciones patronales nuevas" necesita más detalle. 
   Amplía específicamente qué es el REPSE (Registro de Prestadoras de 
   Servicios Especializados u Obras Especializadas), quién debe registrarse 
   y cuáles son los plazos de renovación.
   ```

5. Actualizar el título del documento a: `Analisis_Normativo_Completo_[TuNombre].docx` y guardar los cambios.

6. Compartir el documento con el instructor a través de SharePoint o enviarlo por correo electrónico como evidencia del Bloque A.

**Resultado Esperado:**

El documento final debe contener:
- La tabla de cuotas IMSS/Infonavit del Paso A2
- El ejemplo de costo laboral
- El resumen ejecutivo de la reforma de subcontratación (400-500 palabras)
- La tabla "Antes vs. Después" de la reforma
- La sección ampliada sobre el REPSE

**Verificación:**

✅ El resumen ejecutivo tiene entre 400 y 500 palabras (verificar con el contador de palabras de Word).
✅ La tabla "Antes vs. Después" contiene al menos 4 filas de comparación.
✅ El REPSE está mencionado con su definición y propósito.
✅ El documento está guardado y compartido con el instructor.

---

### BLOQUE B: Creación del Agente de Consulta Legal en Copilot Studio

---

### Paso B1 — Acceso y Configuración Inicial del Agente en Copilot Studio

**Objetivo:** Crear la estructura base del agente de consulta legal en Microsoft Copilot Studio, configurando su identidad, propósito y fuente de conocimiento documental.

**Instrucciones:**

1. Abrir una nueva pestaña del navegador y navegar a `https://copilotstudio.microsoft.com`.

2. Iniciar sesión con la cuenta corporativa del curso si se solicita.

3. En la pantalla principal de Copilot Studio, hacer clic en el botón **"+ Crear"** (o **"+ New copilot"**) ubicado en la esquina superior izquierda o en el panel central.

4. En el panel de creación, seleccionar la opción **"Crear con descripción"** (o "Describe your copilot"). Ingresar la siguiente descripción:

   ```
   Asistente de consulta normativa laboral para el área de Compensaciones y 
   Recursos Humanos. Responde preguntas frecuentes sobre la Ley Federal del 
   Trabajo (LFT), cuotas del IMSS, aportaciones al Infonavit, cálculo de 
   aguinaldo, prima vacacional, PTU y reformas laborales recientes en México. 
   Dirigido a especialistas de nómina y compensaciones en empresas mexicanas.
   ```

5. Hacer clic en **"Crear"** y esperar a que Copilot Studio genere la estructura inicial del agente (aproximadamente 30-60 segundos).

6. Una vez creado el agente, localizar el campo de nombre en la parte superior y cambiar el nombre predeterminado por:
   ```
   AsesorNormativo_RRHH
   ```

7. En la sección **"Descripción"** del agente, ingresar:
   ```
   Agente de consulta legal para el equipo de Compensaciones. Proporciona 
   orientación sobre normativas laborales mexicanas (LFT, IMSS, Infonavit) 
   y cálculos de nómina. Solo para uso interno. Las respuestas no sustituyen 
   la asesoría legal profesional.
   ```

8. Hacer clic en **"Guardar"** para preservar la configuración inicial.

**Resultado Esperado:**

- El agente `AsesorNormativo_RRHH` aparece creado en el panel principal de Copilot Studio.
- La pantalla de edición del agente muestra las secciones: Temas, Acciones, Conocimiento, Configuración y Publicar.

**Verificación:**

✅ El agente aparece con el nombre `AsesorNormativo_RRHH` en el panel de Copilot Studio.
✅ La descripción del agente es visible en la sección de configuración.
✅ No hay mensajes de error en la pantalla de edición.

---

### Paso B2 — Configuración de la Base de Conocimiento con Documentos de SharePoint

**Objetivo:** Conectar el agente con los documentos normativos cargados en SharePoint para que las respuestas del agente estén fundamentadas en fuentes documentales específicas del curso.

**Instrucciones:**

1. En la pantalla de edición del agente `AsesorNormativo_RRHH`, localizar la sección **"Conocimiento"** (Knowledge) en el menú lateral izquierdo o en las pestañas superiores. Hacer clic en ella.

2. Hacer clic en el botón **"+ Agregar conocimiento"** (o **"+ Add knowledge"**).

3. En el panel de fuentes de conocimiento, seleccionar **"SharePoint"** como tipo de fuente.

4. En el campo de URL de SharePoint, ingresar la URL del sitio de SharePoint del curso proporcionada por el instructor. La estructura típica es:
   ```
   https://[tenant].sharepoint.com/sites/[NombreDelCurso]/Modulo1/Normativos
   ```
   > 💡 Solicitar al instructor la URL exacta del sitio de SharePoint si no la tienes disponible.

5. Copilot Studio solicitará autenticación. Hacer clic en **"Conectar"** y autorizar el acceso con la cuenta corporativa.

6. Una vez conectado, seleccionar la carpeta `/Modulo1/Normativos/` y marcar los siguientes documentos:
   - `LFT_Vigente_Ficticio.pdf`
   - `LSS_Cuotas_IMSS_2024_Ficticio.pdf`
   - `Infonavit_Tabla_Aportaciones_Ficticio.pdf`
   - `Reforma_Subcontratacion_Resumen_Ficticio.pdf`

7. Hacer clic en **"Agregar"** para confirmar la selección de documentos.

8. Esperar a que Copilot Studio procese e indexe los documentos (puede tomar 1-3 minutos dependiendo del tamaño de los archivos). El estado debe cambiar de "Procesando" a "Listo".

9. Verificar que los cuatro documentos aparecen en la lista de fuentes de conocimiento con estado **"Activo"**.

10. Hacer clic en **"Guardar"** para preservar la configuración de conocimiento.

**Resultado Esperado:**

- Los cuatro documentos normativos aparecen en la sección de Conocimiento del agente con estado "Activo" o "Listo".
- El agente está configurado para consultar estos documentos al responder preguntas.

**Verificación:**

✅ Los cuatro archivos PDF aparecen en la lista de conocimiento del agente.
✅ El estado de cada documento es "Activo" o "Listo" (no "Error" ni "Procesando").
✅ La conexión a SharePoint fue autorizada correctamente.

---

### Paso B3 — Creación de Temas Conversacionales Predefinidos

**Objetivo:** Configurar al menos tres temas conversacionales en el agente que respondan a las preguntas más frecuentes del equipo de compensaciones sobre normativas laborales.

**Instrucciones:**

1. En la pantalla de edición del agente, hacer clic en la sección **"Temas"** (Topics) en el menú lateral.

2. Observar que Copilot Studio puede haber generado algunos temas automáticamente basados en la descripción del agente. Estos pueden servir como punto de partida.

3. Crear el **Tema 1 — Cálculo de Aguinaldo**:

   a. Hacer clic en **"+ Nuevo tema"** → **"Crear desde descripción"**.

   b. En el campo de descripción, ingresar:
   ```
   Cuando el usuario pregunte sobre el cálculo del aguinaldo, la fórmula 
   legal, los días mínimos, el artículo de la LFT o cómo calcular el 
   aguinaldo proporcional para empleados con menos de un año.
   ```

   c. Hacer clic en **"Crear"** y esperar a que Copilot Studio genere el flujo conversacional.

   d. Revisar el flujo generado. En el nodo de **"Mensaje"** principal, verificar que la respuesta incluye referencia al Artículo 87 de la LFT y la fórmula de 15 días mínimos de salario.

   e. Si la respuesta generada no es suficientemente completa, editar el nodo de mensaje y agregar manualmente:
   ```
   Conforme al **Artículo 87 de la LFT**, los trabajadores tienen derecho a 
   un aguinaldo anual de mínimo **15 días de salario**, que debe pagarse 
   antes del 20 de diciembre. 

   **Fórmula:** Aguinaldo = (Salario Diario × 15 días × Días Trabajados) / 365

   Para empleados con menos de un año, el aguinaldo se calcula de forma 
   proporcional al tiempo laborado.

   ⚠️ *Esta información es orientativa. Consulte con el área legal para 
   casos específicos.*
   ```

   f. Hacer clic en **"Guardar tema"**.

4. Crear el **Tema 2 — Cuotas IMSS Patronales**:

   a. Hacer clic en **"+ Nuevo tema"** → **"Crear desde descripción"**.

   b. Ingresar la siguiente descripción:
   ```
   Cuando el usuario pregunte sobre el porcentaje de aportación patronal 
   al IMSS, los ramos del seguro social, el Salario Base de Cotización (SBC) 
   o cómo se calculan las cuotas obrero-patronales.
   ```

   c. Hacer clic en **"Crear"** y revisar el flujo generado.

   d. En el nodo de mensaje, verificar que la respuesta incluye los principales ramos del seguro social y sus porcentajes. Si es necesario, editar para incluir:
   ```
   Las cuotas al **IMSS** se dividen en aportaciones **patronales** y 
   **obreras**, calculadas sobre el **Salario Base de Cotización (SBC)**.

   Principales ramos (porcentajes aproximados vigentes):
   - Enfermedades y Maternidad (Prestaciones en Especie): Patronal ~20.40% / Obrero ~0.40%
   - Invalidez y Vida: Patronal 1.75% / Obrero 0.625%
   - Retiro, Cesantía en Edad Avanzada y Vejez (RCV): Patronal 5.150% / Obrero 1.125%
   - Guarderías y Prestaciones Sociales: Patronal 1.0% / Obrero 0%

   El **SBC** incluye salario base más prestaciones integrables (vales, 
   comisiones, bonos, etc.) conforme al Art. 27 de la LSS.

   ⚠️ *Los porcentajes exactos deben verificarse con las tablas vigentes 
   del IMSS para el ejercicio fiscal en curso.*
   ```

   e. Hacer clic en **"Guardar tema"**.

5. Crear el **Tema 3 — Reforma de Subcontratación (Outsourcing)**:

   a. Hacer clic en **"+ Nuevo tema"** → **"Crear desde descripción"**.

   b. Ingresar la siguiente descripción:
   ```
   Cuando el usuario pregunte sobre la reforma de outsourcing o 
   subcontratación, qué cambió en la LFT, qué es el REPSE, qué empresas 
   deben registrarse o cuáles son las obligaciones patronales desde 2021.
   ```

   c. Hacer clic en **"Crear"** y revisar el flujo.

   d. Editar el nodo de mensaje para asegurar que incluye los puntos clave:
   ```
   La **Reforma de Subcontratación** (DOF abril 2021) modificó la LFT, 
   LSS, Ley del Infonavit y CFF. Puntos clave:

   **¿Qué cambió?**
   - Se prohibió la subcontratación de personal (outsourcing de nómina).
   - Solo se permite subcontratar **servicios especializados** que no formen 
     parte del objeto social de la empresa contratante.

   **¿Qué es el REPSE?**
   El Registro de Prestadoras de Servicios Especializados u Obras 
   Especializadas, administrado por la STPS. Las empresas que presten 
   servicios especializados **deben estar registradas** en el REPSE.

   **Obligaciones para el contratante:**
   - Verificar que el proveedor esté registrado en el REPSE.
   - Retener el ISR e IVA si el proveedor no está registrado.
   - Los trabajadores deben estar en nómina directa de quien se beneficia 
     del servicio.

   ⚠️ *Consulte con su asesor legal y fiscal para determinar el impacto 
   específico en su organización.*
   ```

   e. Hacer clic en **"Guardar tema"**.

6. Verificar que los tres temas aparecen en la lista de temas del agente con estado **"Activado"** (toggle en verde).

**Resultado Esperado:**

- Tres temas conversacionales activos en el agente: "Cálculo de Aguinaldo", "Cuotas IMSS Patronales" y "Reforma de Subcontratación".
- Cada tema contiene un flujo con al menos un nodo de mensaje con información normativa relevante.

**Verificación:**

✅ Los tres temas aparecen en la lista de temas con estado "Activado".
✅ Cada tema tiene al menos un nodo de mensaje con contenido normativo.
✅ Los mensajes incluyen advertencias de validación profesional.

---

### Paso B4 — Prueba del Agente en el Panel de Pruebas de Copilot Studio

**Objetivo:** Validar el funcionamiento del agente mediante el panel de pruebas integrado de Copilot Studio antes de publicarlo.

**Instrucciones:**

1. En la pantalla de edición del agente, localizar el botón **"Probar"** (Test) en la esquina superior derecha o en la barra de herramientas. Hacer clic en él para abrir el panel de pruebas lateral.

2. En el panel de pruebas (que simula una conversación), ingresar la siguiente pregunta de prueba:

   ```
   ¿Cuántos días de aguinaldo me corresponden por ley?
   ```

3. Observar la respuesta del agente. Verificar que:
   - El agente activa el tema "Cálculo de Aguinaldo"
   - La respuesta menciona el Artículo 87 de la LFT
   - La respuesta incluye la fórmula o referencia a los 15 días mínimos
   - Aparece la advertencia de validación profesional

4. Continuar la conversación con la siguiente pregunta:

   ```
   ¿Y si llevo solo 6 meses trabajando en la empresa?
   ```

5. Verificar que el agente responde coherentemente sobre el cálculo proporcional.

6. Ingresar la siguiente pregunta para probar el Tema 2:

   ```
   ¿Cuál es el porcentaje de aportación patronal al IMSS?
   ```

7. Verificar que el agente activa el tema "Cuotas IMSS Patronales" y proporciona los porcentajes de los principales ramos.

8. Ingresar la siguiente pregunta para probar el Tema 3:

   ```
   ¿Qué es el REPSE y quién debe registrarse?
   ```

9. Verificar que el agente activa el tema "Reforma de Subcontratación" y explica el REPSE correctamente.

10. Probar una pregunta fuera de los temas configurados:

    ```
    ¿Cuántos días de vacaciones corresponden a un empleado con 3 años de antigüedad?
    ```

11. Observar cómo el agente maneja una pregunta no cubierta por los temas explícitos. Si tiene habilitada la respuesta generativa (basada en los documentos de SharePoint), debería proporcionar una respuesta basada en los documentos cargados.

12. Documentar en una nota los resultados de las pruebas: ¿Qué funcionó correctamente? ¿Qué respuestas necesitan mejora?

**Resultado Esperado:**

- Los tres temas responden correctamente a las preguntas de prueba correspondientes.
- La pregunta sobre vacaciones (fuera de temas) recibe una respuesta basada en los documentos de SharePoint o un mensaje de derivación apropiado.
- No se producen errores técnicos durante las pruebas.

**Verificación:**

✅ El tema de aguinaldo responde correctamente a la pregunta directa y al seguimiento de 6 meses.
✅ El tema de cuotas IMSS proporciona al menos 3 ramos del seguro social.
✅ El tema de REPSE explica el registro y las obligaciones patronales.
✅ El agente no genera errores de sistema durante las 5 pruebas.

---

### Paso B5 — Publicación del Agente en Microsoft Teams

**Objetivo:** Publicar el agente `AsesorNormativo_RRHH` en Microsoft Teams para que los miembros del equipo de compensaciones puedan acceder a él desde el entorno de colaboración habitual.

**Instrucciones:**

1. En la pantalla de edición del agente, hacer clic en la sección **"Publicar"** (Publish) en el menú lateral izquierdo o en la barra de navegación superior.

2. En la pantalla de publicación, hacer clic en el botón **"Publicar"** para generar la versión publicada del agente. Confirmar la acción si se solicita.

3. Esperar a que el proceso de publicación complete (1-2 minutos). El estado debe cambiar a "Publicado".

4. Una vez publicado, localizar la sección de **"Canales"** (Channels) o **"Disponibilidad"** dentro de la pantalla de publicación.

5. Buscar el canal de **Microsoft Teams** en la lista de canales disponibles. Hacer clic en **"Agregar a Teams"** o **"Habilitar"** para el canal de Teams.

6. En el panel de configuración de Teams, seleccionar:
   - **Tipo de acceso:** Solo usuarios específicos o el equipo del curso
   - Si se solicita, seleccionar el **equipo de Teams del curso** proporcionado por el instructor

7. Hacer clic en **"Guardar"** o **"Confirmar"** para completar la configuración del canal de Teams.

8. Abrir Microsoft Teams (aplicación de escritorio o web en `https://teams.microsoft.com`).

9. En Teams, hacer clic en el ícono de **"..."** (Más aplicaciones) en la barra lateral izquierda, o navegar a **"Aplicaciones"**.

10. Buscar el agente por su nombre `AsesorNormativo_RRHH`. Si no aparece inmediatamente, puede tomar 5-10 minutos para que el agente se propague al catálogo de Teams.

11. Hacer clic en el agente para abrir una conversación con él directamente en Teams.

12. Probar el agente en Teams con la siguiente pregunta:

    ```
    Hola, ¿cuáles son las obligaciones patronales principales respecto al IMSS?
    ```

13. Verificar que el agente responde correctamente desde el entorno de Teams.

14. Tomar una captura de pantalla de la conversación con el agente en Teams como evidencia de la práctica.

**Resultado Esperado:**

- El agente `AsesorNormativo_RRHH` aparece como una aplicación o bot disponible en Microsoft Teams.
- El agente responde a la pregunta de prueba en Teams con información sobre las obligaciones patronales del IMSS.
- La captura de pantalla muestra la conversación activa en Teams.

**Verificación:**

✅ El agente fue publicado exitosamente en Copilot Studio (estado "Publicado").
✅ El canal de Teams fue habilitado para el agente.
✅ El agente responde en Teams a la pregunta de prueba.
✅ La captura de pantalla fue tomada como evidencia.

---

## 7. Validación y Pruebas Finales

Una vez completados todos los pasos del Bloque A y Bloque B, realizar las siguientes validaciones de cierre:

### Lista de Verificación Final

| # | Elemento a Validar | Criterio de Éxito | ✅/❌ |
|---|---|---|---|
| 1 | Prompts en Copilot Chat (Paso A1) | Respuestas incluyen Art. 87, 80 y referencia a PTU de la LFT | |
| 2 | Tabla de cuotas IMSS/Infonavit en Word (Paso A2) | Tabla con mínimo 6 ramos y ejemplo con SBC $18,500 MXN | |
| 3 | Resumen ejecutivo de reforma outsourcing (Paso A3) | 400-500 palabras, tabla Antes/Después, mención del REPSE | |
| 4 | Agente creado en Copilot Studio (Paso B1) | Agente `AsesorNormativo_RRHH` existe y está guardado | |
| 5 | Base de conocimiento configurada (Paso B2) | 4 documentos PDF de SharePoint con estado "Activo" | |
| 6 | Tres temas conversacionales (Paso B3) | Temas de aguinaldo, cuotas IMSS y REPSE activos | |
| 7 | Pruebas en panel de Copilot Studio (Paso B4) | 5 preguntas de prueba respondidas sin errores | |
| 8 | Publicación en Teams (Paso B5) | Agente responde en Teams + captura de pantalla | |

### Prueba de Integración Final

Para confirmar que el agente funciona de manera integral, realizar la siguiente secuencia de preguntas en Teams (o en el panel de pruebas de Copilot Studio):

```
Pregunta 1: "¿Cuántos días de aguinaldo corresponden a un empleado con 
            salario de $20,000 mensuales y 8 meses de antigüedad?"

Pregunta 2: "¿Qué porcentaje del salario se descuenta al trabajador 
            para el IMSS?"

Pregunta 3: "Mi empresa usa servicios de una empresa de outsourcing. 
            ¿Necesitamos verificar el REPSE?"
```

**Criterios de aprobación de la prueba de integración:**
- Las tres preguntas reciben respuestas relevantes y fundamentadas
- Al menos dos respuestas hacen referencia a artículos legales o porcentajes específicos
- Todas las respuestas incluyen una nota de advertencia sobre validación profesional

---

## 8. Solución de Problemas

### Problema 1 — El agente en Copilot Studio no activa los temas correctos y responde con información genérica

**Síntomas:**
- Al hacer preguntas sobre aguinaldo o cuotas IMSS en el panel de pruebas, el agente responde con información muy general o dice que no tiene información disponible.
- Los temas creados en el Paso B3 no se activan aunque la pregunta es directamente relacionada.

**Causa probable:**
Los temas conversacionales en Copilot Studio dependen de frases desencadenadoras (trigger phrases) para activarse. Si las frases configuradas automáticamente por Copilot Studio no coinciden con el vocabulario del usuario, el tema no se activa y el agente recurre a la respuesta generativa general o al mensaje de fallback.

**Solución:**
1. Ir a la sección **"Temas"** del agente en Copilot Studio.
2. Hacer clic en el tema que no se activa (ej. "Cálculo de Aguinaldo").
3. En el nodo de **"Desencadenador"** (Trigger), localizar la sección de frases desencadenadoras.
4. Agregar manualmente las siguientes frases adicionales para el tema de aguinaldo:
   ```
   aguinaldo
   días de aguinaldo
   cálculo de aguinaldo
   cuánto es el aguinaldo
   artículo 87 LFT
   aguinaldo proporcional
   ```
5. Repetir el proceso para los otros dos temas, agregando variaciones del vocabulario que los usuarios podrían usar.
6. Hacer clic en **"Guardar"** y volver a probar en el panel de pruebas.
7. Si el problema persiste, verificar que el toggle del tema esté en posición **"Activado"** (verde).

---

### Problema 2 — Los documentos de SharePoint no aparecen en la base de conocimiento o muestran estado de error

**Síntomas:**
- Al intentar agregar la fuente de conocimiento de SharePoint en el Paso B2, los documentos muestran estado "Error" o "No se pudo indexar".
- El agente no parece consultar los documentos al responder preguntas relacionadas con su contenido.
- Aparece un mensaje de error de permisos al intentar conectar Copilot Studio con SharePoint.

**Causa probable:**
Existen dos causas comunes: (a) permisos insuficientes — la cuenta del participante no tiene permisos de lectura en la biblioteca de documentos de SharePoint del curso, o (b) formato incompatible — los documentos PDF tienen restricciones de copia/extracción de texto que impiden que Copilot Studio los indexe correctamente.

**Solución:**

*Para el problema de permisos:*
1. Contactar al instructor o al administrador del sitio de SharePoint.
2. Solicitar que se verifique que la cuenta del participante tiene permisos de **"Lectura"** o superior en la biblioteca `/Modulo1/Normativos/`.
3. Una vez confirmados los permisos, regresar a Copilot Studio → Conocimiento → eliminar la fuente con error → volver a agregar la fuente de SharePoint.

*Para el problema de formato de PDF:*
1. Verificar si los PDFs tienen restricciones de seguridad: abrir el PDF en Adobe Reader o Edge → Propiedades del documento → Seguridad → verificar si "Copia de contenido" está permitida.
2. Si los PDFs tienen restricciones, solicitar al instructor una versión sin restricciones de los documentos.
3. Como alternativa temporal, usar documentos en formato `.docx` o `.txt` en lugar de PDF, ya que estos formatos son más fácilmente indexables por Copilot Studio.
4. Si el problema persiste, como workaround para la práctica, desactivar la fuente de SharePoint y habilitar la opción de **"Conocimiento general"** (General knowledge) en la configuración del agente, que permite al agente usar su conocimiento base de IA para responder preguntas normativas.

---

## 9. Limpieza del Entorno

Al finalizar la práctica, realizar las siguientes acciones de limpieza para mantener el entorno ordenado y evitar costos innecesarios:

### Acciones Obligatorias

1. **Guardar todos los documentos de Word:**
   - Verificar que `Analisis_Normativo_Completo_[TuNombre].docx` esté guardado en OneDrive o en la ubicación indicada por el instructor.
   - Cerrar Word correctamente.

2. **Conservar el agente en Copilot Studio:**
   - El agente `AsesorNormativo_RRHH` debe mantenerse activo ya que será utilizado en prácticas posteriores del curso (Práctica 7 y 8).
   - **No eliminar** el agente al finalizar esta práctica.

3. **Cerrar sesiones activas:**
   - Cerrar el panel de pruebas de Copilot Studio si está abierto.
   - No es necesario despublicar el agente de Teams.

### Acciones Opcionales (al finalizar el curso)

> ⚠️ Realizar estas acciones **solo al concluir el curso completo**, no al finalizar esta práctica.

```
Para eliminar el agente al final del curso:
1. Ir a copilotstudio.microsoft.com
2. Seleccionar el agente AsesorNormativo_RRHH
3. Hacer clic en "..." → "Eliminar"
4. Confirmar la eliminación
```

### Entrega de Evidencias

Antes de cerrar las aplicaciones, asegurarse de haber entregado al instructor:

| Evidencia | Formato | Método de Entrega |
|---|---|---|
| Documento Word con análisis normativo completo | `.docx` | SharePoint del curso o correo |
| Captura de pantalla del agente respondiendo en Teams | `.png` o `.jpg` | SharePoint del curso o correo |
| Captura de pantalla de los 3 temas activos en Copilot Studio | `.png` o `.jpg` | SharePoint del curso o correo |

---

## 10. Resumen y Recursos Adicionales

### Resumen de la Práctica

En esta práctica completaste dos bloques de trabajo fundamentales para el uso de IA en la gestión normativa de compensaciones:

**Bloque A — Interpretación Normativa con Copilot:**
- Formulaste prompts estructurados en Microsoft 365 Copilot para obtener interpretaciones precisas de la LFT (Art. 87, 80 y PTU), demostrando que la clave no es solo preguntar, sino **cómo preguntar** con contexto, rol y formato de salida definidos.
- Generaste una tabla de referencia de cuotas IMSS/Infonavit con un ejemplo de costo laboral completo en Word, usando Copilot como asistente de redacción técnica.
- Creaste un resumen ejecutivo accionable sobre la reforma de subcontratación, con tabla comparativa Antes/Después y sección ampliada sobre el REPSE.

**Bloque B — Agente de Consulta Legal en Copilot Studio:**
- Configuraste el agente `AsesorNormativo_RRHH` con identidad, descripción y propósito claros.
- Conectaste documentos normativos de SharePoint como base de conocimiento documental del agente.
- Creaste tres temas conversacionales funcionales que cubren las consultas más frecuentes del equipo de compensaciones.
- Publicaste y validaste el agente en Microsoft Teams, completando el ciclo de desarrollo y despliegue.

### Lecciones Clave

> 🎯 **Copilot es un asistente, no un oráculo.** Las respuestas generadas deben siempre ser validadas por un especialista legal antes de tomar decisiones que afecten la nómina o el cumplimiento normativo.

> 🎯 **La calidad del prompt determina la calidad de la respuesta.** Prompts con contexto (rol, audiencia, formato), restricciones (extensión, tono) y ejemplos específicos (salario de referencia, período) producen resultados significativamente más útiles.

> 🎯 **Los agentes de Copilot Studio son tan buenos como su base de conocimiento.** Documentos bien organizados, actualizados y sin restricciones de seguridad son fundamentales para que el agente proporcione respuestas precisas.

### Conexión con el Marco Normativo Mexicano

Esta práctica te permitió interactuar directamente con los principales marcos normativos que rigen la compensación en México:

| Marco Normativo | Conceptos Trabajados | Herramienta Utilizada |
|---|---|---|
| Ley Federal del Trabajo (LFT) | Aguinaldo (Art. 87), Prima vacacional (Art. 80), PTU (Art. 117-131), Reforma outsourcing | Copilot Chat, Copilot en Word, Copilot Studio |
| Ley del Seguro Social (LSS) | SBC (Art. 27), Ramos del seguro, Cuotas obrero-patronales | Copilot en Word, Copilot Studio |
| Ley del Infonavit | Aportación patronal 5%, Base de cálculo | Copilot en Word, Copilot Studio |
| REPSE (STPS) | Registro, obligaciones, reforma 2021 | Copilot Chat, Copilot Studio |

### Recursos Adicionales

| Recurso | Descripción | URL |
|---|---|---|
| Ley Federal del Trabajo — DOF | Texto vigente oficial | https://www.diputados.gob.mx/LeyesBiblio/pdf/LFT.pdf |
| Ley del Seguro Social — DOF | Texto vigente oficial | https://www.diputados.gob.mx/LeyesBiblio/pdf/LSS.pdf |
| Portal REPSE — STPS | Consulta y registro en el REPSE | https://repse.stps.gob.mx |
| Obligaciones patronales IMSS | Portal oficial de patrones | https://www.imss.gob.mx/patrones/obligaciones |
| Documentación de Copilot Studio | Microsoft Learn — Guías oficiales | https://learn.microsoft.com/es-mx/microsoft-copilot-studio/ |
| Uso responsable de IA — Microsoft | Guía de IA responsable en empresas | https://learn.microsoft.com/es-mx/ai/responsible-ai/ |
| Infonavit — Tabla de aportaciones | Portal oficial Infonavit patrones | https://patronos.infonavit.org.mx |

### Próximos Pasos en el Curso

En la **Práctica 2**, aplicarás los conocimientos de esta práctica en un contexto más avanzado: utilizarás Copilot en Excel para automatizar el cálculo de los conceptos normativos que interpretaste hoy (aguinaldo, PTU, cuotas IMSS/Infonavit) sobre un dataset de nómina ficticio, integrando las fórmulas legales directamente en hojas de cálculo con validación automática de cumplimiento.

---

*Documento generado para uso exclusivo del curso "Copilot en Compensaciones". Todos los datos numéricos y ejemplos son ficticios y tienen propósito educativo. Las interpretaciones normativas deben validarse con la versión vigente de cada ordenamiento legal y con asesoría jurídica especializada.*
