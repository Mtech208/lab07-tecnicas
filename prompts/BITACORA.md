# Bitacora de tecnicas avanzadas

Laboratorio 07: Tecnicas Avanzadas de Prompting.  
Herramienta de IA usada: Gemini  

---

## Ejercicio 2: Zero-shot, one-shot y few-shot

| Tipo | Aciertos (de 5) | Formato de la respuesta | Todas con el mismo formato (Si/No) |
|------|-----------------|-------------------------|------------------------------------|
| Zero-shot | 5 | Tabla detallada con explicaciones explicativas adicionales | No |
| One-shot | 5 | Lista numerada con negrita en el texto original (`1. **Texto** -> Etiqueta`) | Si |
| Few-shot | 5 | Estructura limpia e idéntica a los ejemplos (`"Texto" -> Etiqueta`) | Si |

**Observaciones de los resultados:**
- **Zero-shot:** La IA acertó todas las clasificaciones pero devolvió una tabla completa con descripciones del sentimiento entre paréntesis (ej. *Positivo (satisfecho con el producto y la entrega)*), lo cual cambia el formato básico solicitado.
- **One-shot:** Al darle un ejemplo, adoptó el uso de flechas (`->`), pero aplicó formato de lista numerada y resaltó en negrita el comentario original.
- **Few-shot:** La IA imitó a la perfección la estructura de los ejemplos dados, devolviendo directamente cada frase entre comillas seguida de `->` y la clasificación, sin texto explicativo adicional.

---

## Ejercicio 3: Chain of Thought

| Pedido | Respuesta de la IA | Muestra los pasos (Si/No) | Correcta (Si/No) |
|--------|--------------------|---------------------------|------------------|
| Directo | Muestra pasos breves y finaliza con `318.60` | Si | Si |
| Paso a paso | Muestra desglose detallado con fórmulas, comprobación por método alternativo y concluye con `S/ 318.60` | Si | Si |

**¿Por qué es útil ver el razonamiento?**  
Aunque la respuesta directa arrojó el resultado correcto, la versión paso a paso incluyó una comprobación adicional mediante un método alternativo (calculando primero sobre el total de las 3 unidades). Esto permite verificar que no haya errores de redondeo o de precedencia de operadores, dando mayor certeza y auditabilidad al resultado final.

---

## Ejercicio 4: Role prompting

| Version | Vocabulario (sencillo/tecnico) | Usa ejemplos o codigo | A quien le sirve mas |
|---------|-------------------------------|-----------------------|----------------------|
| A. Sin rol | Intermedio / General | Explicación directa con ejemplos estándar | Público general |
| B. Rol docente | Sencillo, claro y pedagógico | Metáfora de "caja etiquetada", juego de puntaje y sintaxis básica en Python | Estudiantes que nunca han programado |
| C. Rol senior | Técnico de bajo nivel (RAM, JVM, Stack/Heap) | Bloques de código Java (`int`, `String`, `final`) y explicaciones de rendimiento | Desarrolladores Java / Compañeros de trabajo |

---

## Ejercicio 5: Descomposición

- **Paso 1:** Identificó los 5 requisitos funcionales principales del sistema de inventario (catálogo de productos, control de entradas/salidas, registro de ventas, alertas de stock mínimo y reportes).
- **Paso 2:** Diseñó la arquitectura de clases (`Producto`, `MovimientoInventario`, `Venta`, `DetalleVenta`, `AlertaStock`, `ReporteInventario`), definiendo atributos con sus tipos de datos y destacando el uso de `BigDecimal` para valores monetarios.
- **Paso 3:** Generó el código Java completo para la clase `Producto`, incluyendo atributos privados, constructor por defecto y completo, métodos getters/setters, un método de negocio `requiereReabastecimiento()` y `toString()`.
- **Paso 4:** Analizó la clase `Producto` y propuso 3 mejoras avanzadas:
  1. Validación de datos de entrada (evitar precios o stocks negativos).
  2. Encapsulamiento de la lógica de negocio (`agregarStock` y `descontarStock`).
  3. Implementación de `equals()` y `hashCode()` para el manejo correcto en colecciones (`Set`, `Map`).

**Comparación con pedido de una sola vez:**  
Al descomponer la solicitud en 4 prompts secuenciales, la IA entregó explicaciones más profundas, una arquitectura modular completa con DTOs y un código robusto con mejores prácticas de software, superando con creces la respuesta resumida y genérica que generaría un único prompt.

---

## Ejercicio 6: Prompt estructurado y autocritica

```text
<rol>Actua como analista de pruebas de software.</rol>
<contexto>Login web con correo y contrasena. La cuenta se bloquea despues de 3 intentos fallidos.</contexto>
<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>
<formato>Tabla con las columnas: ID, escenario, datos de entrada, resultado esperado.</formato>

Mensaje de autocritica:
Revisa tu tabla: faltan casos limite como campos vacios, correo sin @ o contrasena con espacios? Agrega los que falten e indica cuales agregaste.