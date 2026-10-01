# Tarea: Mi prompt avanzado

## Tarea elegida
Diseñar la arquitectura de clases Java, endpoints REST y casos de prueba para el módulo de **Gestión de Notas y Calificaciones Estudiantiles** en escala vigesimal (0 a 20).

---

## Version 1: prompt basico

`Crea un sistema para gestionar las notas de los estudiantes de un colegio en Java.`

**Análisis de la Version 1:**
- **Técnica usada:** Ninguna (Prompt Básico / Zero-shot).
- **Por qué:** Sirve como punto de comparación inicial para evaluar la respuesta por defecto de la IA.
- **Resultado:** Entregó un código Java genérico dentro de un solo archivo, sin manejo de arquitectura, sin validaciones de rango y sin endpoints REST.

---

## Version 2

`<rol>Actúa como Arquitecto de Software Backend Java Senior especialista en sistemas educativos.</rol>`  
`<contexto>Estamos desarrollando el módulo de calificaciones para un colegio. Se requiere registrar asignaturas, estudiantes, notas por periodo (bimestres) e historial de promedios.</contexto>`  
`<tarea>`  
`Paso 1: Lista las clases principales con sus atributos y tipos de datos.`  
`Paso 2: Escribe el código Java de la clase principal Nota.`  
`Paso 3: Muestra la estructura de endpoints REST necesarios.`  
`</tarea>`  

**Análisis de la Version 2:**
- **Técnicas agregadas:** Role Prompting + Descomposición + Prompt Estructurado (etiquetas XML).
- **Por qué:** Definir un rol especializado mejora el estándar técnico del código y descomponer la tarea obliga a estructurar la respuesta por etapas.
- **Qué mejoró:** Se incluyeron buenas prácticas de diseño orientado a objetos y tipos adecuados, pero las rutas REST carecían de un patrón unificado y faltaban validaciones de negocio.

---

## Version 3: prompt final

`<rol>Actúa como Arquitecto de Software Backend Senior en Java y especialista en QA.</rol>`  

`<contexto>`  
`Estamos construyendo la API REST del módulo de Gestión de Notas para un colegio en Perú (escala vigesimal 0-20).`  
`</contexto>`  

`<tarea>`  
`Analiza paso a paso la arquitectura del sistema y genera la documentación técnica del módulo de calificaciones siguiendo el flujo establecido en los ejemplos.`  
`</tarea>`  

`<ejemplos>`  
`Ejemplo de endpoint REST:`  
`"POST /api/v1/notas" -> Registra una nota | Body: {estudianteId, cursoId, valor} | Retorna: 201 Created`  

`Ejemplo de endpoint REST:`  
`"GET /api/v1/estudiantes/{id}/promedio" -> Obtiene el promedio ponderado del estudiante | Retorna: 200 OK`  
`</ejemplos>`  

`<formato>`  
`1. Lista de Entidades (Nombre y Atributos con tipo Java).`  
`2. Código Java limpio de la entidad Nota con validaciones de rango (0-20).`  
`3. Tabla de Endpoints REST (Método, Ruta, Descripción).`  
`4. Casos de prueba límite para el registro de notas.`  
`</formato>`  

`Mensaje de autocrítica:`  
`Revisa tu respuesta antes de entregarla: ¿El código valida que la nota no sea menor a 0 ni mayor a 20? ¿Los endpoints siguen el estándar REST? Agrega o corrige las validaciones que falten e indica explícitamente qué ajustaste.`  

**Análisis de la Version 3:**
- **Técnicas agregadas:** Few-shot + Chain of Thought + Autocrítica (sumadas a Role Prompting y Prompt Estructurado).
- **Por qué:** *Few-shot* fija la estructura estandarizada de la API REST, *Chain of Thought* asegura un análisis lógico del diseño, y la *Autocrítica* garantiza la inclusión de reglas de negocio críticas (escala 0-20).
- **Qué mejoró:** Generó una propuesta robusta con validaciones explícitas de excepciones (`@DecimalMin`, `@DecimalMax`), endpoints consistentes y casos de prueba QA.

---

## Tecnicas usadas en el prompt final

| Técnica aplicada | Parte del prompt final donde se ubica | Propósito de la técnica |
|------------------|---------------------------------------|-------------------------|
| **Role Prompting** | `<rol>Actúa como Arquitecto de Software...</rol>` | Asigna la perspectiva y el estándar de calidad de un especialista senior. |
| **Prompt Estructurado** | Uso de etiquetas `<rol>`, `<contexto>`, `<tarea>`, `<ejemplos>`, `<formato>` | Delimita con claridad las instrucciones para evitar malinterpretaciones del modelo. |
| **Chain of Thought** | `<tarea>Analiza paso a paso la arquitectura...</tarea>` | Guía el razonamiento lógico del modelo antes de emitir el código. |
| **Few-shot** | Sección `<ejemplos>` con mapeos de rutas REST | Define el formato visual y estructural que deben seguir los controladores de la API. |
| **Autocrítica** | Bloque `Mensaje de autocrítica:` | Obliga a la IA a auto-evaluar su resultado y añadir reglas de validación faltantes. |

---

## Evaluacion del resultado

| Criterio a revisar | Cumple (Sí / No) |
|--------------------|------------------|
| ¿Se adoptó el rol de Arquitecto Senior en el lenguaje y código? | Sí |
| ¿El código Java incluye validación para la escala vigesimal (0 a 20)? | Sí |
| ¿Los endpoints REST siguen la estructura exacta demostrada en los ejemplos? | Sí |
| ¿La autocrítica identificó y corrigió las reglas de validación en la respuesta? | Sí |

---

## Por que elegi estas tecnicas

Elegí **Role Prompting, Few-Shot, Prompt Estructurado y Autocrítica** debido a que la arquitectura de software exige precisión formal. El *Prompt Estructurado* y el *Few-Shot* imponen un patrón limpio e idéntico para la documentación de la API. Por último, la *Autocrítica* actúa como un filtro de calidad esencial en el desarrollo backend, garantizando que reglas clave como el rango permitido de calificaciones no queden omitidas.

---

