# Práctica 7 — Configuración de un Agente para Atención de Consultas de Nómina

## 1. Metadatos

| Atributo | Detalle |
|---|---|
| **Duración estimada** | 90 minutos |
| **Complejidad** | Alta |
| **Nivel Bloom** | Crear |
| **Módulo / Capítulo** | Capítulo 7 — Integración de Agentes de IA en Recursos Humanos |
| **Práctica** | 7 de 8 |

---

## 2. Descripción General

En esta práctica construirás desde cero un agente de inteligencia artificial funcional en **Microsoft Copilot Studio**, diseñado específicamente para atender consultas de nómina de empleados. El agente combinará respuestas generativas basadas en documentos de políticas almacenados en SharePoint con temas conversacionales diseñados manualmente para consultas estructuradas (fechas de pago, desglose de recibo, liquidación, vacaciones, aguinaldo). Integrarás flujos de **Power Automate** para recuperar datos personalizados del empleado desde una hoja de Excel, y finalmente publicarás y probarás el agente en **Microsoft Teams**. Esta práctica representa el primer despliegue de un agente autónomo de RH dentro del ecosistema Microsoft 365, aplicando el concepto central del Capítulo 7: la transición de un asistente puntual hacia un agente que actúa dentro de flujos de trabajo definidos.

---

## 3. Objetivos de Aprendizaje

Al finalizar esta práctica, serás capaz de:

- [ ] **Diseñar** la arquitectura completa de un agente de IA para nómina, definiendo alcance de temas, fuentes de conocimiento, flujos conversacionales y condiciones de escalamiento a un agente humano.
- [ ] **Configurar** en Copilot Studio un agente funcional con temas específicos de nómina conectado a documentos de políticas en SharePoint.
- [ ] **Implementar** flujos de Power Automate dentro del agente para recuperar datos personalizados del empleado (salario, antigüedad, días de vacaciones) desde Excel/SharePoint.
- [ ] **Publicar y probar** el agente en Microsoft Teams, validando precisión de respuestas, manejo de preguntas fuera de alcance y experiencia del usuario final.

---

## 4. Prerrequisitos

### Conocimientos Previos

| Área | Nivel requerido |
|---|---|
| Microsoft Copilot Studio (interfaz básica, creación de temas) | Intermedio — completado en Práctica 1 del curso |
| Power Automate (creación de flujos con conectores SharePoint y Excel Online) | Básico — completado en Prácticas 4 y 5 |
| SharePoint Online (subir documentos, obtener URLs de archivos) | Básico |
| Estructura de conversaciones en chatbots (intents, entidades, variables) | Básico conceptual |
| Marcos normativos mexicanos de nómina (IMSS, LFT, aguinaldo, vacaciones) | Intermedio — cubierto en Prácticas 2, 3 y 6 |

### Accesos y Licencias Requeridos

| Recurso | Estado requerido |
|---|---|
| Licencia activa de **Microsoft 365 Copilot** (Apps for Enterprise) | ✅ Activa y asignada al participante |
| Acceso a **Copilot Studio** (`copilotstudio.microsoft.com`) con rol **Maker** | ✅ Habilitado por administrador del tenant |
| Acceso a **Power Automate** (`make.powerautomate.com`) con conectores premium | ✅ Incluido en licencia M365 |
| Acceso al sitio de **SharePoint del curso** con documentos de políticas precargados | ✅ Configurado por instructor |
| Acceso a **Microsoft Teams** (desktop o web) | ✅ Activo |

### Archivos de Práctica Requeridos

Estos archivos deben estar disponibles en el sitio de SharePoint del curso antes de iniciar. Solicítalos a tu instructor si no los localizas.

| Archivo | Ubicación en SharePoint | Descripción |
|---|---|---|
| `Politica_Vacaciones.pdf` | `/Modulo7/Politicas/` | Política de vacaciones conforme a LFT |
| `Tabla_Liquidacion.pdf` | `/Modulo7/Politicas/` | Tabla de cálculo de liquidación (3 meses + 20 días + partes proporcionales) |
| `Calendario_Pagos_2025.pdf` | `/Modulo7/Politicas/` | Fechas de pago de nómina del año en curso |
| `Politica_Aguinaldo.pdf` | `/Modulo7/Politicas/` | Política de aguinaldo (mínimo 15 días según LFT Art. 87) |
| `BD_Empleados_Ficticios.xlsx` | `/Modulo7/Datos/` | Base de datos con empleados ficticios: ID, nombre, salario, antigüedad, días de vacaciones disponibles |

> ⚠️ **Aviso de cumplimiento:** Todos los archivos de práctica contienen **datos ficticios** conforme a la Ley Federal de Protección de Datos Personales en Posesión de los Particulares (LFPDPPP). Está estrictamente prohibido sustituirlos por datos reales de empleados.

---

## 5. Entorno de Laboratorio

### Requisitos de Hardware

| Componente | Mínimo | Recomendado |
|---|---|---|
| RAM | 8 GB | 16 GB (múltiples pestañas de M365 abiertas simultáneamente) |
| Procesador | Intel Core i5 8ª gen / AMD Ryzen 5 | Intel Core i7 / AMD Ryzen 7 |
| Almacenamiento libre | 2 GB | 5 GB |
| Conexión a internet | 10 Mbps | 25 Mbps |
| Resolución de pantalla | 1366×768 | 1920×1080 (recomendado para Copilot Studio) |

### Requisitos de Software

| Aplicación | Versión mínima | URL de acceso |
|---|---|---|
| Microsoft Copilot Studio | Versión actual | `https://copilotstudio.microsoft.com` |
| Microsoft Power Automate | Versión actual | `https://make.powerautomate.com` |
| Microsoft Teams | Desktop o web (versión actual) | `https://teams.microsoft.com` |
| Microsoft SharePoint Online | Versión actual | URL del tenant corporativo |
| Microsoft Excel Online | M365 versión 2308+ | Integrado en SharePoint |
| Navegador web | Edge 120+ o Chrome 120+ | — |

### Configuración Inicial del Entorno

Antes de comenzar los pasos del laboratorio, verifica que tu entorno esté listo ejecutando esta lista de comprobación:

```
LISTA DE COMPROBACIÓN PRE-LABORATORIO
======================================
[ ] 1. Abre copilotstudio.microsoft.com e inicia sesión con tu cuenta corporativa.
       Confirma que ves el botón "+ Nuevo agente" en el panel principal.

[ ] 2. Abre make.powerautomate.com e inicia sesión.
       Confirma que puedes crear un flujo nuevo (botón "+ Crear").

[ ] 3. Navega al sitio de SharePoint del curso.
       Confirma que los 5 archivos de práctica están presentes en sus carpetas.

[ ] 4. Abre BD_Empleados_Ficticios.xlsx en Excel Online.
       Confirma que la hoja contiene columnas: ID_Empleado, Nombre, Apellido,
       Departamento, Salario_Mensual, Antiguedad_Anos, Dias_Vacaciones_Disponibles.

[ ] 5. Abre Microsoft Teams.
       Confirma que tienes acceso al canal del curso o a un canal de prueba.
```

> 💡 **Tip:** Mantén abiertas las siguientes pestañas durante toda la práctica: (1) Copilot Studio, (2) Power Automate, (3) SharePoint del curso, (4) Teams. Esto reducirá el tiempo de navegación entre herramientas.

---

## 6. Instrucciones Paso a Paso

---

### Paso 1 — Crear y Configurar el Agente Base en Copilot Studio

**Objetivo:** Crear el agente "Asistente de Nómina RH" con identidad, tono, idioma y alcance definidos. Este es el punto de partida arquitectónico del agente.

#### Instrucciones

1. Navega a `https://copilotstudio.microsoft.com` e inicia sesión con tu cuenta corporativa.

2. En el panel principal, haz clic en **"+ Nuevo agente"** (esquina superior derecha o botón central si el panel está vacío).

3. En la pantalla de creación, selecciona **"Omitir para configurar"** (skip to configure) para acceder a la configuración manual completa en lugar del asistente guiado por IA.

   > 💡 Si prefieres usar el asistente, puedes escribir en el cuadro de descripción: *"Crea un agente de atención a empleados para responder consultas de nómina en español, incluyendo fechas de pago, desglose de recibo, vacaciones, aguinaldo y liquidación. El agente debe ser formal pero accesible y escalar a RH cuando no pueda responder."*

4. En la pantalla de configuración del agente, completa los siguientes campos:

   ```
   Nombre del agente:    Asistente de Nómina RH
   Descripción:          Agente de inteligencia artificial para atender consultas
                         de nómina de empleados. Responde preguntas sobre fechas
                         de pago, desglose de recibo de sueldo, cálculo de
                         liquidación, días de vacaciones disponibles y aguinaldo.
                         Opera conforme a la Ley Federal del Trabajo (LFT) y
                         políticas internas de la empresa.
   Idioma principal:     Español (México)
   ```

5. En el campo **"Instrucciones"** (sección de configuración del agente), ingresa el siguiente texto de sistema que define la personalidad y límites del agente:

   ```
   Eres el Asistente de Nómina RH, un agente especializado en responder consultas
   de nómina para los empleados de la empresa. Tu comportamiento debe seguir estas
   reglas:

   PERSONALIDAD Y TONO:
   - Usa un tono formal pero accesible y empático.
   - Responde siempre en español (México).
   - Sé conciso: respuestas de máximo 3-4 párrafos cortos.
   - Usa el nombre del empleado cuando esté disponible para personalizar la respuesta.

   ALCANCE DE TEMAS (puedes responder):
   - Fechas de pago de nómina (quincenal/mensual)
   - Desglose de conceptos del recibo de sueldo
   - Cálculo de liquidación conforme a LFT
   - Días de vacaciones disponibles y política de vacaciones
   - Cálculo y fecha de pago de aguinaldo
   - Procedimiento para solicitar constancias de empleo y cartas de trabajo

   FUERA DE ALCANCE (NO responder, escalar a RH):
   - Negociaciones salariales
   - Conflictos laborales o quejas formales
   - Información de otros empleados
   - Datos bancarios o modificación de cuenta CLABE
   - Cualquier consulta médica o de IMSS que requiera dictamen

   ESCALAMIENTO:
   Cuando una consulta esté fuera de alcance, responde:
   "Esta consulta requiere atención personalizada de nuestro equipo de RH.
   Te recomiendo contactar a rh@empresa.com o llamar al ext. 1050.
   ¿Hay algo más en lo que pueda ayudarte?"
   ```

6. Haz clic en **"Crear"** para generar el agente base.

7. Una vez creado, verifica que el agente aparece en tu panel de Copilot Studio con el nombre "Asistente de Nómina RH".

#### Resultado Esperado

El agente "Asistente de Nómina RH" aparece en el panel de Copilot Studio con estado **"Activo"** y configuración de idioma en Español (México). Al hacer clic en él, puedes ver la pantalla de edición con las pestañas: Temas, Acciones, Conocimiento, Canales y Configuración.

#### Verificación

```
VERIFICACIÓN PASO 1
====================
[ ] El agente "Asistente de Nómina RH" aparece en el panel principal de Copilot Studio.
[ ] Al abrir el agente, el idioma configurado es "Español (México)".
[ ] Las instrucciones del sistema están guardadas (visibles en la pestaña "Configuración").
[ ] El panel de edición muestra las pestañas: Temas, Acciones, Conocimiento, Canales.
```

---

### Paso 2 — Conectar Fuentes de Conocimiento desde SharePoint

**Objetivo:** Agregar los documentos de políticas de nómina almacenados en SharePoint como fuente de conocimiento generativa del agente, permitiéndole responder preguntas basadas en el contenido documental.

#### Instrucciones

1. Dentro del agente "Asistente de Nómina RH", haz clic en la pestaña **"Conocimiento"** (Knowledge) en el menú lateral izquierdo.

2. Haz clic en **"+ Agregar conocimiento"** (Add knowledge).

3. En el panel que aparece, selecciona **"SharePoint"** como tipo de fuente.

4. En el campo de URL, ingresa la URL del sitio de SharePoint del curso donde están almacenados los documentos de políticas:

   ```
   Ejemplo de URL del sitio:
   https://[tu-tenant].sharepoint.com/sites/CursoM365Compensaciones
   ```

   > 💡 Puedes obtener esta URL navegando al sitio de SharePoint del curso en tu navegador y copiando la URL de la barra de direcciones hasta el nombre del sitio (sin incluir subcarpetas).

5. Copilot Studio escaneará el sitio y mostrará las bibliotecas de documentos disponibles. Selecciona la biblioteca **"Documentos"** o la carpeta específica `/Modulo7/Politicas/`.

6. Confirma que los siguientes archivos son detectados y márcalos todos para incluirlos como conocimiento:
   - `Politica_Vacaciones.pdf`
   - `Tabla_Liquidacion.pdf`
   - `Calendario_Pagos_2025.pdf`
   - `Politica_Aguinaldo.pdf`

7. Haz clic en **"Agregar"** para confirmar la fuente de conocimiento.

8. Espera a que el sistema procese e indexe los documentos. Este proceso puede tomar entre **2 y 5 minutos**. El estado cambiará de "Procesando" a "Listo" cuando finalice.

9. **Prueba rápida de conocimiento generativo:** En el panel de prueba (ícono de chat en la parte derecha de la pantalla), escribe:

   ```
   ¿Cuántos días de aguinaldo corresponden según la política de la empresa?
   ```

   El agente debe responder citando información del documento `Politica_Aguinaldo.pdf`. Si la respuesta incluye una referencia al documento o menciona "15 días mínimo conforme a la LFT", el conocimiento generativo está funcionando correctamente.

10. Prueba una segunda consulta relacionada con vacaciones:

    ```
    ¿Cuántos días de vacaciones tengo derecho en mi primer año de trabajo?
    ```

#### Resultado Esperado

El panel de Conocimiento muestra los 4 documentos PDF con estado **"Listo"** (verde). Las respuestas de prueba en el panel de chat muestran información coherente con el contenido de los documentos y, en algunos casos, incluyen la referencia al documento fuente.

#### Verificación

```
VERIFICACIÓN PASO 2
====================
[ ] Los 4 documentos PDF aparecen en la pestaña "Conocimiento" con estado "Listo".
[ ] La consulta de aguinaldo genera una respuesta que menciona días mínimos o
    referencia la política de aguinaldo.
[ ] La consulta de vacaciones genera una respuesta coherente con la LFT
    (6 días primer año, incremento progresivo).
[ ] Las respuestas NO mencionan temas fuera del alcance definido.
```

---

### Paso 3 — Crear Temas Conversacionales Manuales para Consultas Estructuradas

**Objetivo:** Diseñar tres temas conversacionales con árboles de decisión para las consultas más frecuentes de nómina: (1) Consulta de fecha de próximo pago, (2) Solicitud de constancia de empleo, y (3) Consulta de días de vacaciones disponibles.

#### Instrucciones

##### Tema 1: Fecha de Próximo Pago

1. En el menú lateral, haz clic en **"Temas"** (Topics) y luego en **"+ Agregar tema"** → **"Desde cero"** (From blank).

2. Configura el tema con los siguientes datos:

   ```
   Nombre del tema:  Fecha de Próximo Pago
   Descripción:      Informa al empleado cuándo recibirá su próximo pago de nómina
   ```

3. En la sección **"Frases de activación"** (Trigger phrases), agrega las siguientes frases (una por línea):

   ```
   ¿cuándo me pagan?
   fecha de pago
   próximo pago de nómina
   ¿cuándo es la quincena?
   día de pago
   ¿cuándo depositan el sueldo?
   fecha de cobro
   ```

4. En el **lienzo de conversación**, después del nodo de activación, agrega un nodo de **"Mensaje"** con el siguiente texto:

   ```
   Los pagos de nómina se realizan de forma quincenal, los días **15 y último de
   cada mes**. Si el día de pago cae en fin de semana o día festivo, el depósito
   se adelanta al último día hábil anterior.

   Para ver el calendario completo de pagos del año, puedes consultarlo en el
   portal de empleados o solicitarlo a RH.

   ¿Tienes alguna otra consulta sobre tu nómina?
   ```

5. Después del mensaje, agrega un nodo de **"Pregunta"** con el texto: *"¿Deseas que te ayude con algo más?"* y configura dos opciones de respuesta rápida:
   - `Sí, tengo otra consulta`
   - `No, gracias`

6. Para la opción **"No, gracias"**, agrega un nodo de **"Mensaje"** de despedida:

   ```
   Con gusto. Recuerda que puedes consultarme en cualquier momento.
   ¡Hasta luego!
   ```

7. Para la opción **"Sí, tengo otra consulta"**, conecta al nodo de **"Ir a otro tema"** → selecciona **"Tema de inicio de conversación"** para reiniciar el flujo principal.

8. Haz clic en **"Guardar"** (Save).

##### Tema 2: Solicitud de Constancia de Empleo

1. Crea un nuevo tema: **"+ Agregar tema"** → **"Desde cero"**.

   ```
   Nombre del tema:  Solicitud de Constancia de Empleo
   Descripción:      Guía al empleado en el proceso para solicitar una constancia
                     de empleo o carta de trabajo
   ```

2. Agrega las siguientes frases de activación:

   ```
   necesito una constancia de empleo
   quiero una carta de trabajo
   solicitar constancia
   carta laboral
   comprobante de trabajo
   necesito carta para el banco
   constancia de ingresos
   ```

3. En el lienzo de conversación, agrega un nodo de **"Pregunta"** para identificar el tipo de documento:

   ```
   Texto de la pregunta:
   "Con gusto te ayudo. ¿Qué tipo de documento necesitas?"

   Opciones de respuesta rápida:
   - Constancia de empleo simple
   - Carta de trabajo con sueldo
   - Constancia para trámite de crédito (INFONAVIT/bancario)
   - Otro tipo de carta
   ```

4. Para cada opción, agrega un nodo de **"Mensaje"** con las instrucciones específicas:

   **Para "Constancia de empleo simple":**
   ```
   Para solicitar tu constancia de empleo, envía un correo a rh@empresa.com
   con el asunto: "Solicitud de Constancia de Empleo - [Tu nombre completo]"

   Incluye en el correo:
   • Tu número de empleado
   • El uso que darás al documento
   • Si necesitas apostilla o firma digital

   El tiempo de entrega es de **2 días hábiles**.
   ```

   **Para "Carta de trabajo con sueldo":**
   ```
   Para solicitar una carta de trabajo con monto de sueldo, envía un correo
   a rh@empresa.com con el asunto:
   "Solicitud de Carta de Trabajo con Sueldo - [Tu nombre completo]"

   Por políticas de privacidad, este documento requiere tu autorización
   firmada. RH te enviará el formato de autorización junto con la carta.

   Tiempo de entrega: **3 días hábiles**.
   ```

   **Para "Constancia para trámite de crédito":**
   ```
   Para constancias de crédito INFONAVIT o bancario, el proceso es:

   1. Descarga el formato oficial de la institución financiera
   2. Envíalo a rh@empresa.com junto con tu solicitud
   3. RH lo llenará y sellará en un plazo de **3 días hábiles**

   Si es un trámite urgente, comunícate directamente al ext. 1050.
   ```

   **Para "Otro tipo de carta":**
   ```
   Para cartas no contempladas en las opciones anteriores, comunícate
   directamente con RH:
   📧 rh@empresa.com
   📞 Ext. 1050
   🕐 Horario de atención: Lunes a viernes, 9:00 - 18:00 hrs.
   ```

5. Guarda el tema.

##### Tema 3: Escalamiento a Agente Humano

1. Crea un tercer tema: **"+ Agregar tema"** → **"Desde cero"**.

   ```
   Nombre del tema:  Escalamiento a RH
   Descripción:      Maneja consultas fuera del alcance del agente y dirige
                     al empleado con el equipo de RH
   ```

2. Frases de activación:

   ```
   quiero hablar con un humano
   hablar con RH
   necesito hablar con alguien
   esto no me ayuda
   quiero hablar con una persona
   necesito ayuda urgente
   escalar mi consulta
   ```

3. Nodo de mensaje:

   ```
   Entiendo que prefieres hablar directamente con nuestro equipo de RH.
   Aquí están los canales de contacto disponibles:

   📧 **Correo:** rh@empresa.com
   📞 **Teléfono:** Extensión 1050
   💬 **Teams:** Canal "Soporte RH" en el equipo de la empresa
   🕐 **Horario:** Lunes a viernes, 9:00 a 18:00 hrs.

   Un especialista de RH te atenderá a la brevedad.
   ¿Hay algo más en lo que pueda ayudarte antes de que te comuniques con ellos?
   ```

4. Guarda el tema.

#### Resultado Esperado

La pestaña "Temas" muestra al menos 3 temas personalizados creados manualmente, además de los temas del sistema que Copilot Studio incluye por defecto. Cada tema tiene frases de activación configuradas y un flujo conversacional completo con nodos de mensaje y, donde aplica, nodos de pregunta con opciones.

#### Verificación

```
VERIFICACIÓN PASO 3
====================
[ ] El tema "Fecha de Próximo Pago" aparece en la lista de temas con estado activo.
[ ] El tema "Solicitud de Constancia de Empleo" tiene 4 ramas de decisión configuradas.
[ ] El tema "Escalamiento a RH" tiene frases de activación que incluyen
    "quiero hablar con un humano".
[ ] Al probar "¿cuándo me pagan?" en el panel de chat, el agente responde con
    información sobre pagos quincenales (no con una respuesta genérica).
[ ] Al probar "necesito una constancia de empleo", el agente presenta las
    4 opciones de tipo de documento.
```

---

### Paso 4 — Crear el Flujo de Power Automate para Recuperar Datos del Empleado

**Objetivo:** Construir un flujo de Power Automate que el agente pueda invocar para recuperar datos personalizados del empleado (salario, antigüedad, días de vacaciones disponibles) desde la hoja de Excel `BD_Empleados_Ficticios.xlsx` en SharePoint.

#### Instrucciones

1. Abre una nueva pestaña del navegador y navega a `https://make.powerautomate.com`.

2. En el panel izquierdo, haz clic en **"+ Crear"** → **"Flujo de nube instantáneo"** (Instant cloud flow).

3. Configura el flujo:

   ```
   Nombre del flujo:  Obtener_Datos_Empleado_Nomina
   Desencadenador:    Al llamar a un flujo secundario de Power Virtual Agents
                      (When a flow is run from a copilot)
   ```

4. Haz clic en **"Crear"**.

5. En el desencadenador **"When a flow is run from a copilot"**, haz clic en **"+ Agregar una entrada"** y configura el parámetro de entrada:

   ```
   Tipo:    Texto
   Nombre:  ID_Empleado
   ```

6. Agrega un nuevo paso: haz clic en **"+ Nuevo paso"** y busca **"Excel Online (Business)"**. Selecciona la acción **"Obtener una fila"** (Get a row).

7. Configura la acción con los siguientes parámetros:

   ```
   Ubicación:            SharePoint
   Biblioteca de docs:   [Nombre de la biblioteca donde está BD_Empleados_Ficticios.xlsx]
   Archivo:              BD_Empleados_Ficticios.xlsx
   Tabla:                Tabla_Empleados
   Id. de fila clave:    ID_Empleado
   Valor de clave:       [Selecciona el contenido dinámico: ID_Empleado del paso anterior]
   ```

   > ⚠️ **Nota:** Para que Power Automate pueda leer la tabla de Excel, el rango de datos en `BD_Empleados_Ficticios.xlsx` debe estar formateado como **Tabla** (no solo como rango). Si no está formateado como tabla, abre el archivo en Excel Online, selecciona el rango de datos y aplica **Insertar → Tabla** con el nombre `Tabla_Empleados`.

8. Agrega otro paso: busca **"Responder a un copiloto o a un bot de Power Virtual Agents"** (Respond to a copilot or Power Virtual Agents bot). Configura las salidas:

   ```
   Haz clic en "+ Agregar una salida" para cada uno de los siguientes:

   Salida 1:
     Tipo:   Texto
     Nombre: Nombre_Completo
     Valor:  [Contenido dinámico: Nombre] & " " & [Contenido dinámico: Apellido]

   Salida 2:
     Tipo:   Número
     Nombre: Salario_Mensual
     Valor:  [Contenido dinámico: Salario_Mensual]

   Salida 3:
     Tipo:   Número
     Nombre: Antiguedad_Anos
     Valor:  [Contenido dinámico: Antiguedad_Anos]

   Salida 4:
     Tipo:   Número
     Nombre: Dias_Vacaciones_Disponibles
     Valor:  [Contenido dinámico: Dias_Vacaciones_Disponibles]

   Salida 5:
     Tipo:   Texto
     Nombre: Departamento
     Valor:  [Contenido dinámico: Departamento]
   ```

9. Haz clic en **"Guardar"** (Save). Espera a que el flujo se guarde correctamente (aparecerá una palomita verde o el mensaje "El flujo se guardó correctamente").

10. **Prueba del flujo:** Haz clic en **"Probar"** (Test) → **"Manualmente"** → **"Probar"**. Ingresa un ID de empleado ficticio de tu dataset (por ejemplo: `EMP001`) y verifica que el flujo devuelve los datos correctos.

#### Resultado Esperado

El flujo `Obtener_Datos_Empleado_Nomina` aparece en Power Automate con estado **"Activo"**. Al probarlo manualmente con un ID de empleado válido del dataset, devuelve los 5 valores configurados (Nombre_Completo, Salario_Mensual, Antiguedad_Anos, Dias_Vacaciones_Disponibles, Departamento) sin errores.

#### Verificación

```
VERIFICACIÓN PASO 4
====================
[ ] El flujo "Obtener_Datos_Empleado_Nomina" aparece en Power Automate
    con estado "Activo" (no "Desactivado" ni "Error").
[ ] La prueba manual con ID "EMP001" (u otro ID válido del dataset) devuelve
    datos sin errores de ejecución.
[ ] Los 5 parámetros de salida están configurados correctamente.
[ ] El historial de ejecución del flujo muestra al menos 1 ejecución exitosa
    (ícono verde).
```

---

### Paso 5 — Conectar el Flujo al Agente y Crear el Tema de Consulta Personalizada

**Objetivo:** Integrar el flujo de Power Automate dentro del agente de Copilot Studio y crear el tema "Consulta de Días de Vacaciones Disponibles" que recupera datos personalizados del empleado usando el flujo.

#### Instrucciones

1. Regresa a Copilot Studio y abre el agente "Asistente de Nómina RH".

2. En el menú lateral, haz clic en **"Temas"** → **"+ Agregar tema"** → **"Desde cero"**.

3. Configura el tema:

   ```
   Nombre del tema:  Consulta de Vacaciones Disponibles
   Descripción:      Recupera y muestra los días de vacaciones disponibles
                     del empleado consultando la base de datos via Power Automate
   ```

4. Agrega las siguientes frases de activación:

   ```
   ¿cuántos días de vacaciones me quedan?
   días de vacaciones disponibles
   saldo de vacaciones
   ¿cuántas vacaciones tengo?
   mis días de vacaciones
   vacaciones pendientes
   ¿cuántos días puedo tomar de vacaciones?
   ```

5. En el lienzo de conversación, después del nodo de activación, agrega un nodo de **"Pregunta"** para solicitar el ID del empleado:

   ```
   Texto de la pregunta:
   "Para consultar tu saldo de vacaciones, necesito verificar tu información.
   Por favor, ingresa tu número de empleado (ejemplo: EMP001):"

   Tipo de respuesta:  Texto completo del usuario
   Guardar en variable: Var_ID_Empleado
   ```

6. Después del nodo de pregunta, agrega un nodo de **"Acción"** → **"Llamar a una acción"** → **"Crear un flujo"** → selecciona el flujo **"Obtener_Datos_Empleado_Nomina"** que creaste en el Paso 4.

   > 💡 Si el flujo no aparece en la lista, haz clic en "Ver más" o busca por nombre. Puede tardar 1-2 minutos en sincronizarse entre Power Automate y Copilot Studio.

7. En la configuración de la acción del flujo, mapea el parámetro de entrada:

   ```
   Parámetro del flujo:  ID_Empleado
   Valor:                [Selecciona la variable: Var_ID_Empleado]
   ```

8. Configura las variables de salida del flujo (Copilot Studio las crea automáticamente). Verifica que se generaron las siguientes variables:

   ```
   Topic.Nombre_Completo
   Topic.Salario_Mensual
   Topic.Antiguedad_Anos
   Topic.Dias_Vacaciones_Disponibles
   Topic.Departamento
   ```

9. Agrega un nodo de **"Condición"** (Condition) para manejar el caso en que no se encuentre el empleado:

   ```
   Condición:  Topic.Nombre_Completo es igual a "" (vacío)
   
   Rama "Sí" (empleado no encontrado):
     Agrega un nodo de Mensaje:
     "No encontré un empleado con el número [Var_ID_Empleado]. 
     Por favor verifica tu número de empleado e intenta nuevamente,
     o comunícate con RH al ext. 1050."
   
   Rama "No" (empleado encontrado):
     Continúa al siguiente nodo
   ```

10. En la rama **"No"** (empleado encontrado), agrega un nodo de **"Mensaje"** con la respuesta personalizada usando las variables:

    ```
    Hola, **{Topic.Nombre_Completo}** 👋

    Aquí está tu información de vacaciones:

    📅 **Días de vacaciones disponibles:** {Topic.Dias_Vacaciones_Disponibles} días
    🏢 **Departamento:** {Topic.Departamento}
    ⏳ **Antigüedad:** {Topic.Antiguedad_Anos} año(s)

    Conforme a la Ley Federal del Trabajo, los días de vacaciones se incrementan
    progresivamente con base en tu antigüedad. Para programar tus vacaciones,
    comunícate con tu supervisor directo y notifica a RH con al menos 5 días de
    anticipación.

    ¿Puedo ayudarte con algo más?
    ```

    > 💡 Para insertar variables en el mensaje, usa el botón **"Insertar variable"** (ícono `{x}`) que aparece en el editor de mensajes y selecciona cada variable de la lista.

11. Guarda el tema.

#### Resultado Esperado

El tema "Consulta de Vacaciones Disponibles" está completo con: nodo de pregunta para ID, llamada al flujo de Power Automate, condición para manejo de errores y mensaje personalizado con datos del empleado. Al probarlo en el panel de chat con un ID válido, el agente devuelve datos reales del dataset ficticio.

#### Verificación

```
VERIFICACIÓN PASO 5
====================
[ ] El flujo "Obtener_Datos_Empleado_Nomina" aparece como acción disponible
    dentro del tema en Copilot Studio.
[ ] Las variables de salida del flujo (Topic.Nombre_Completo, etc.) están
    correctamente mapeadas en el nodo de mensaje.
[ ] Al probar el tema con ID "EMP001", el agente responde con el nombre
    y días de vacaciones del empleado ficticio correspondiente.
[ ] Al probar con un ID inválido (ej. "XYZ999"), el agente muestra el
    mensaje de error configurado en la rama de condición.
```

---

### Paso 6 — Configurar el Tema de Inicio y Personalizar la Experiencia de Bienvenida

**Objetivo:** Personalizar el tema de inicio de conversación del agente para establecer el contexto, recopilar el ID del empleado al inicio y configurar variables globales de sesión.

#### Instrucciones

1. En la pestaña **"Temas"**, localiza el tema del sistema llamado **"Conversación - Saludo"** o **"Greeting"** (tema de inicio predeterminado). Haz clic en él para editarlo.

2. Reemplaza el mensaje de bienvenida predeterminado con el siguiente:

   ```
   ¡Hola! Soy el **Asistente de Nómina RH** 🤖

   Estoy aquí para ayudarte con tus consultas sobre:
   • 📅 Fechas de pago de nómina
   • 📄 Desglose de tu recibo de sueldo
   • 🏖️ Días de vacaciones disponibles
   • 💰 Cálculo de aguinaldo
   • 📋 Solicitud de constancias y cartas de trabajo
   • 💼 Información sobre liquidación

   ¿En qué puedo ayudarte hoy?
   ```

3. Después del mensaje de bienvenida, agrega opciones de respuesta rápida para facilitar la navegación:

   ```
   Opciones de respuesta rápida:
   - "Fechas de pago"
   - "Mis vacaciones disponibles"
   - "Solicitar constancia"
   - "Calcular aguinaldo"
   - "Hablar con RH"
   ```

4. Guarda el tema de inicio.

5. Ahora configura el tema **"Conversación - Sin coincidencia"** (Fallback / No match): este tema se activa cuando el agente no entiende la consulta del usuario.

6. Edita el mensaje de fallback:

   ```
   No estoy seguro de haber entendido tu consulta. 🤔

   Puedo ayudarte con temas de nómina como fechas de pago, vacaciones,
   aguinaldo, constancias de empleo y liquidación.

   ¿Podrías reformular tu pregunta? O si prefieres, puedo conectarte
   con el equipo de RH.

   Opciones rápidas:
   ```

7. Agrega opciones de respuesta rápida al fallback:

   ```
   - "Reformular mi pregunta"
   - "Hablar con RH"
   ```

8. Guarda todos los cambios.

#### Resultado Esperado

El agente presenta un mensaje de bienvenida personalizado con opciones claras al iniciar cualquier conversación. Las consultas no reconocidas activan el mensaje de fallback con opciones de redirección, evitando que el usuario quede sin respuesta.

#### Verificación

```
VERIFICACIÓN PASO 6
====================
[ ] Al iniciar una nueva conversación en el panel de prueba, aparece el
    mensaje de bienvenida personalizado con el menú de opciones.
[ ] Al escribir una consulta sin sentido (ej. "asdfgh"), el agente responde
    con el mensaje de fallback configurado.
[ ] Las opciones de respuesta rápida del saludo son funcionales (al hacer
    clic en "Mis vacaciones disponibles", activa el tema correspondiente).
```

---

### Paso 7 — Publicar el Agente en Microsoft Teams

**Objetivo:** Publicar el agente "Asistente de Nómina RH" en Microsoft Teams para que los empleados puedan interactuar con él directamente desde la plataforma de colaboración.

#### Instrucciones

1. En Copilot Studio, con el agente "Asistente de Nómina RH" abierto, haz clic en el botón **"Publicar"** (Publish) ubicado en la barra superior derecha.

2. En el panel de publicación, revisa el resumen del agente:
   - Número de temas configurados
   - Fuentes de conocimiento conectadas
   - Acciones/flujos integrados

3. Haz clic en **"Publicar"** para confirmar. El proceso de publicación tarda aproximadamente **2-3 minutos**.

4. Una vez publicado, navega a la pestaña **"Canales"** (Channels) en el menú lateral del agente.

5. En la lista de canales disponibles, localiza **"Microsoft Teams"** y haz clic en **"Agregar canal"** o **"Activar"**.

6. En el panel de configuración de Teams, completa:

   ```
   Disponibilidad:     Mostrar en Teams para mis compañeros de trabajo
   Icono del agente:   (Opcional) Sube un ícono personalizado de 30x30 px
   Descripción corta:  Asistente de IA para consultas de nómina y RH
   ```

7. Haz clic en **"Agregar a Teams"** (Add to Teams).

8. Se abrirá una ventana emergente de Teams. Haz clic en **"Agregar"** para instalar el agente como aplicación en tu Teams.

9. Una vez instalado, Teams abrirá automáticamente una conversación directa con el agente "Asistente de Nómina RH".

10. **Prueba de publicación:** Inicia una conversación en Teams escribiendo:

    ```
    Hola
    ```

    Verifica que el agente responde con el mensaje de bienvenida personalizado configurado en el Paso 6.

#### Resultado Esperado

El agente "Asistente de Nómina RH" aparece como una aplicación instalada en Microsoft Teams y responde correctamente al mensaje de saludo con el menú de opciones configurado. La conversación se realiza dentro del entorno de Teams sin necesidad de abrir Copilot Studio.

#### Verificación

```
VERIFICACIÓN PASO 7
====================
[ ] El estado del agente en Copilot Studio muestra "Publicado" (no "Borrador").
[ ] El canal "Microsoft Teams" aparece como activo en la pestaña "Canales".
[ ] El agente aparece en la lista de aplicaciones de Teams del participante.
[ ] Al escribir "Hola" en Teams, el agente responde con el mensaje de
    bienvenida personalizado.
[ ] Las opciones de respuesta rápida son visibles y funcionales en Teams.
```

---

### Paso 8 — Pruebas Exhaustivas del Agente con Escenarios de Nómina

**Objetivo:** Ejecutar un conjunto de escenarios de prueba que validen la precisión de respuestas, el manejo de consultas fuera de alcance y la experiencia completa del usuario final.

#### Instrucciones

Ejecuta cada uno de los siguientes escenarios de prueba en el panel de chat de Teams (o en el panel de prueba de Copilot Studio). Registra los resultados en la tabla de validación al final de este paso.

##### Escenario A — Consulta de Conocimiento Generativo (Aguinaldo)

```
CONSULTA DE PRUEBA A:
"¿Cuántos días de aguinaldo me corresponden si llevo 8 meses trabajando?"

RESULTADO ESPERADO:
El agente debe responder mencionando que el aguinaldo mínimo es de 15 días
conforme al Art. 87 de la LFT, y que si se tiene menos de un año, corresponde
la parte proporcional. Debe citar o referenciar la política de aguinaldo.
```

##### Escenario B — Consulta de Conocimiento Generativo (Liquidación)

```
CONSULTA DE PRUEBA B:
"¿Qué me corresponde si me despiden sin causa justificada?"

RESULTADO ESPERADO:
El agente debe mencionar los tres conceptos principales de liquidación:
3 meses de salario, 20 días por año trabajado y partes proporcionales
(aguinaldo, vacaciones, prima vacacional). Debe basar la respuesta en
la Tabla_Liquidacion.pdf.
```

##### Escenario C — Tema Manual (Fecha de Pago)

```
CONSULTA DE PRUEBA C:
"¿El viernes me depositan o el lunes?"

RESULTADO ESPERADO:
El agente debe activar el tema "Fecha de Próximo Pago" y responder
sobre los pagos quincenales los días 15 y último de mes, con mención
del adelanto cuando cae en fin de semana.
```

##### Escenario D — Tema con Flujo (Vacaciones Personalizadas)

```
CONSULTA DE PRUEBA D:
"¿Cuántos días de vacaciones tengo disponibles?"

FLUJO ESPERADO:
1. Agente solicita número de empleado
2. Usuario ingresa: EMP003 (o cualquier ID válido del dataset)
3. Agente llama al flujo de Power Automate
4. Agente responde con nombre del empleado, días disponibles,
   departamento y antigüedad

RESULTADO ESPERADO:
Respuesta personalizada con datos reales del empleado EMP003 del dataset.
```

##### Escenario E — Solicitud de Constancia

```
CONSULTA DE PRUEBA E:
"Necesito una carta para el banco"

RESULTADO ESPERADO:
El agente debe activar el tema "Solicitud de Constancia de Empleo" y
presentar las 4 opciones de tipo de documento. Al seleccionar
"Constancia para trámite de crédito", debe mostrar el proceso
de 3 pasos con el tiempo de entrega.
```

##### Escenario F — Consulta Fuera de Alcance

```
CONSULTA DE PRUEBA F:
"Quiero negociar un aumento de sueldo"

RESULTADO ESPERADO:
El agente debe reconocer que esto está fuera de su alcance y responder
con el mensaje de escalamiento configurado, proporcionando el correo
rh@empresa.com y extensión 1050.
```

##### Escenario G — Solicitud de Hablar con Humano

```
CONSULTA DE PRUEBA G:
"Quiero hablar con una persona de RH"

RESULTADO ESPERADO:
El agente activa el tema "Escalamiento a RH" y proporciona todos
los canales de contacto disponibles.
```

##### Tabla de Registro de Resultados de Prueba

Completa esta tabla durante las pruebas:

| Escenario | Consulta enviada | Tema activado | Respuesta correcta | Observaciones |
|---|---|---|---|---|
| A | Aguinaldo proporcional | Generativo (SharePoint) | ☐ Sí ☐ No | |
| B | Liquidación sin causa | Generativo (SharePoint) | ☐ Sí ☐ No | |
| C | Día de depósito | Fecha de Próximo Pago | ☐ Sí ☐ No | |
| D | Vacaciones disponibles | Consulta Vacaciones + Flujo | ☐ Sí ☐ No | |
| E | Carta para banco | Solicitud de Constancia | ☐ Sí ☐ No | |
| F | Negociar aumento | Escalamiento (fuera de alcance) | ☐ Sí ☐ No | |
| G | Hablar con humano | Escalamiento a RH | ☐ Sí ☐ No | |

#### Resultado Esperado

Al menos **6 de los 7 escenarios** deben producir el resultado esperado. Los escenarios D (flujo personalizado) y F (fuera de alcance) son los más críticos para validar la arquitectura completa del agente.

#### Verificación

```
VERIFICACIÓN PASO 8
====================
[ ] Se completaron los 7 escenarios de prueba y se registraron los resultados.
[ ] El Escenario D (vacaciones con flujo) devuelve datos personalizados del empleado.
[ ] El Escenario F (fuera de alcance) activa el mensaje de escalamiento correcto.
[ ] No se presentaron errores de flujo (500, timeout) durante las pruebas.
[ ] La experiencia en Teams es fluida (sin demoras mayores a 5 segundos por respuesta).
```

---

## 7. Validación y Pruebas Finales

### Lista de Verificación de Entregables

Al concluir la práctica, verifica que tienes todos los componentes del agente correctamente configurados:

```
ENTREGABLES FINALES — PRÁCTICA 7
===================================

AGENTE EN COPILOT STUDIO:
[ ] Agente "Asistente de Nómina RH" publicado (no en borrador)
[ ] 4 fuentes de conocimiento de SharePoint indexadas y con estado "Listo"
[ ] 5 temas configurados:
    [ ] Fecha de Próximo Pago (manual)
    [ ] Solicitud de Constancia de Empleo (manual, 4 ramas)
    [ ] Escalamiento a RH (manual)
    [ ] Consulta de Vacaciones Disponibles (con flujo de Power Automate)
    [ ] Tema de inicio personalizado
[ ] Tema de fallback personalizado configurado
[ ] Instrucciones del sistema (personalidad y límites) guardadas

FLUJO DE POWER AUTOMATE:
[ ] Flujo "Obtener_Datos_Empleado_Nomina" activo y sin errores
[ ] Parámetro de entrada: ID_Empleado
[ ] 5 parámetros de salida configurados
[ ] Al menos 1 ejecución exitosa en el historial

PUBLICACIÓN EN TEAMS:
[ ] Canal de Microsoft Teams activado en Copilot Studio
[ ] Agente instalado y funcional en Teams del participante
[ ] Prueba de saludo exitosa en Teams

PRUEBAS:
[ ] Los 7 escenarios de prueba ejecutados y documentados
[ ] Mínimo 6 de 7 escenarios con resultado correcto
```

### Criterios de Éxito

| Criterio | Peso | Estado |
|---|---|---|
| Agente publicado y accesible en Teams | 20% | ☐ |
| Conocimiento generativo de SharePoint funcional | 15% | ☐ |
| Temas manuales con flujos de decisión correctos | 20% | ☐ |
| Flujo de Power Automate integrado y funcional | 25% | ☐ |
| Manejo correcto de consultas fuera de alcance | 10% | ☐ |
| Experiencia de usuario coherente y personalizada | 10% | ☐ |

---

## 8. Solución de Problemas

### Problema 1 — El Flujo de Power Automate No Aparece como Acción en Copilot Studio

**Síntomas:**
- Al intentar agregar una acción de flujo en el tema "Consulta de Vacaciones Disponibles" (Paso 5), el flujo `Obtener_Datos_Empleado_Nomina` no aparece en la lista de flujos disponibles.
- El mensaje puede indicar "No se encontraron flujos" o la lista aparece vacía.

**Causa:**
El flujo de Power Automate no tiene configurado el desencadenador correcto para integrarse con Copilot Studio. Solo los flujos con el desencadenador **"When a flow is run from a copilot"** (anteriormente "When a flow is run from Power Virtual Agents") son visibles desde Copilot Studio. Además, el flujo debe estar en el **mismo entorno de Power Platform** que el agente de Copilot Studio.

**Solución:**

1. Regresa a Power Automate (`make.powerautomate.com`).
2. Abre el flujo `Obtener_Datos_Empleado_Nomina` y verifica que el primer paso (desencadenador) sea exactamente: **"When a flow is run from a copilot"**.
3. Si el desencadenador es diferente (por ejemplo, "HTTP request" o "Manual"), debes crear el flujo nuevamente desde cero con el desencadenador correcto.
4. Verifica que el flujo y el agente están en el **mismo entorno de Power Platform**: en Power Automate, el entorno aparece en la esquina superior derecha. En Copilot Studio, el entorno se muestra en la misma ubicación. Ambos deben coincidir.
5. Una vez corregido, regresa a Copilot Studio, cierra y vuelve a abrir el tema. Espera 2-3 minutos para que la sincronización se complete.
6. Si el flujo aún no aparece, haz clic en **"Actualizar"** (ícono de recarga) en el selector de flujos dentro del tema.

---

### Problema 2 — El Agente Responde con Información Incorrecta o No Relacionada con los Documentos de SharePoint

**Síntomas:**
- Al preguntar sobre aguinaldo o vacaciones, el agente responde con información genérica de internet en lugar de basarse en los documentos de políticas de la empresa.
- Las respuestas no mencionan las políticas específicas de la empresa ni referencian los documentos PDF.
- El agente puede responder con información contradictoria o desactualizada.

**Causa:**
Existen dos causas posibles: (a) los documentos de SharePoint no fueron indexados correctamente (estado "Error" o "Procesando" en lugar de "Listo"), o (b) la configuración de **"Búsqueda generativa"** (Generative answers) del agente está desactivada o configurada para ignorar las fuentes de conocimiento personalizadas y usar únicamente el modelo de lenguaje base.

**Solución:**

1. **Verifica el estado de indexación:** En Copilot Studio, ve a la pestaña **"Conocimiento"** y confirma que todos los documentos muestran estado **"Listo"** (verde). Si alguno muestra "Error", elimínalo y vuelve a agregarlo. Asegúrate de que los PDFs no están protegidos con contraseña y que el agente tiene permisos de lectura en la biblioteca de SharePoint.

2. **Verifica los permisos de SharePoint:** El agente accede a SharePoint usando la identidad del creador. Confirma que tu cuenta tiene al menos permisos de **"Lector"** en la biblioteca donde están los documentos.

3. **Activa la prioridad de fuentes personalizadas:** En Copilot Studio, ve a **"Configuración"** → **"IA generativa"** (Generative AI). Verifica que la opción **"Buscar solo en fuentes de conocimiento configuradas"** (o equivalente) esté activada. Esto evita que el agente use conocimiento general de internet cuando tiene documentos específicos disponibles.

4. **Prueba el conocimiento directamente:** En la pestaña "Conocimiento", algunos entornos ofrecen un botón de prueba por documento. Úsalo para verificar que el contenido del PDF fue correctamente extraído e indexado.

5. Si los PDFs son escaneados (imágenes sin texto seleccionable), el sistema no puede extraer el contenido. En ese caso, convierte los documentos a PDF con texto seleccionable usando Adobe Acrobat o Microsoft Word antes de subirlos a SharePoint.

---

## 9. Limpieza del Entorno

> ⚠️ **Importante:** Sigue estas instrucciones de limpieza únicamente si tu instructor así lo indica, o al finalizar completamente el curso. El agente creado en esta práctica es necesario para la **Práctica 8** (auditorías de pago y decisiones ejecutivas). **No elimines el agente si aún no has completado la Práctica 8.**

### Si debes limpiar el entorno al terminar el curso:

```
PASOS DE LIMPIEZA
==================

1. EN COPILOT STUDIO:
   - Abre el agente "Asistente de Nómina RH"
   - Ve a "Configuración" → "Avanzado"
   - Selecciona "Eliminar agente"
   - Confirma la eliminación

2. EN POWER AUTOMATE:
   - Localiza el flujo "Obtener_Datos_Empleado_Nomina"
   - Haz clic en los tres puntos (⋯) → "Eliminar"
   - Confirma la eliminación

3. EN MICROSOFT TEAMS:
   - Ve a "Aplicaciones" en la barra lateral de Teams
   - Localiza "Asistente de Nómina RH"
   - Haz clic derecho → "Desinstalar"

4. EN SHAREPOINT (solo si los archivos fueron subidos por el participante):
   - No elimines los archivos del sitio del curso si fueron proporcionados
     por el instructor; son compartidos con otros participantes.
   - Solo elimina archivos que hayas subido tú personalmente para pruebas.
```

### Si continúas a la Práctica 8:

```
PREPARACIÓN PARA PRÁCTICA 8
==============================
[ ] Mantén el agente "Asistente de Nómina RH" publicado en Copilot Studio.
[ ] Mantén el flujo "Obtener_Datos_Empleado_Nomina" activo en Power Automate.
[ ] Anota la URL del agente en Teams para referencia rápida.
[ ] El instructor proporcionará el dataset adicional necesario para la Práctica 8
    (reportes de auditoría y datos de decisiones ejecutivas).
```

---

## 10. Resumen

### Lo Que Construiste en Esta Práctica

En esta práctica de 90 minutos, construiste un **agente de IA funcional para atención de consultas de nómina** siguiendo la arquitectura completa de un agente autónomo descrita en el Capítulo 7. Específicamente:

| Componente | Tecnología | Resultado |
|---|---|---|
| Agente base con identidad y límites | Copilot Studio | Agente "Asistente de Nómina RH" con instrucciones de sistema |
| Conocimiento generativo documental | SharePoint + Copilot Studio | 4 documentos de políticas indexados y consultables |
| Temas conversacionales manuales | Copilot Studio (lienzo de diseño) | 3 temas con árboles de decisión y flujos estructurados |
| Recuperación de datos personalizados | Power Automate + Excel Online | Flujo que devuelve datos del empleado por ID |
| Respuestas personalizadas con variables | Copilot Studio (variables de tema) | Respuestas que incluyen nombre, saldo de vacaciones, etc. |
| Manejo de consultas fuera de alcance | Copilot Studio (fallback + escalamiento) | Redirección a RH con información de contacto |
| Publicación en canal corporativo | Microsoft Teams | Agente accesible para empleados desde Teams |

### Conceptos Clave Aplicados

- **Agente vs. Asistente:** Implementaste un agente que actúa autónomamente dentro de flujos definidos (recupera datos, toma decisiones según condiciones, escala cuando es necesario), no solo responde cuando se le pregunta.
- **Arquitectura de conocimiento híbrida:** Combinaste conocimiento generativo (basado en documentos) con temas diseñados manualmente, aprovechando las fortalezas de cada enfoque.
- **Orquestación multi-herramienta:** Integraste Copilot Studio, Power Automate, SharePoint y Excel en un flujo de trabajo cohesivo, tal como se describe en la Lección 7.3.
- **Cumplimiento y gobernanza:** Configuraste límites de alcance y mensajes de escalamiento, aplicando principios de gobernanza de agentes de IA en RH.

### Recursos Adicionales

| Recurso | URL |
|---|---|
| Documentación oficial de Copilot Studio | `https://learn.microsoft.com/es-es/microsoft-copilot-studio/` |
| Crear flujos para Copilot Studio en Power Automate | `https://learn.microsoft.com/es-es/microsoft-copilot-studio/advanced-flow-create` |
| Configurar fuentes de conocimiento en Copilot Studio | `https://learn.microsoft.com/es-es/microsoft-copilot-studio/knowledge-sources-overview` |
| Publicar agentes en Microsoft Teams | `https://learn.microsoft.com/es-es/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams` |
| Ley Federal del Trabajo — Texto vigente (DOF) | `https://www.diputados.gob.mx/LeyesBiblio/pdf/LFT.pdf` |

> 🚀 **Próximo paso:** La **Práctica 8** extenderá este agente con capacidades de auditoría de pagos y soporte a decisiones ejecutivas, integrando reportes dinámicos y análisis de datos de compensaciones en tiempo real.

---

*Práctica 7 — Módulo 7: Integración de Agentes de IA en Recursos Humanos*
*Curso: Gestión de Compensaciones con Microsoft 365 Copilot y Herramientas de IA*
*Todos los datos utilizados en esta práctica son ficticios y fueron creados exclusivamente con fines educativos, en cumplimiento con la LFPDPPP.*
