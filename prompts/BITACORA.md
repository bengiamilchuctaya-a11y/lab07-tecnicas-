# Bitacora de tecnicas avanzadas

Laboratorio 07: Tecnicas Avanzadas de Prompting.
Herramienta de IA usada: (escribe aqui cual usaste)

## Ejercicio 2: Zero-shot, one-shot y few-shot

| Tipo      | Aciertos (de 5) | Formato de la respuesta                           | Todas con el mismo formato (Si/No) |
| --------- | --------------- | ------------------------------------------------- | ---------------------------------- |
| Zero-shot | 5               | Tabla estructurada con íconos y resumen final     | Sí                                 |
| One-shot  | 5               | Lista numerada con flecha (`1. Texto → Etiqueta`) | Sí                                 |
| Few-shot  | 5               | Formato estricto `"Texto" -> Etiqueta`            | Sí                                 |

## Ejercicio 3: Chain of Thought

| Pedido      | Respuesta de la IA                   | Muestra los pasos (Si/No) | Correcta (Si/No) |
| ----------- | ------------------------------------ | ------------------------- | ---------------- |
| Directo     | 318.60                               | No                        | Sí               |
| Paso a paso | S/ 318.60 (con desglose del cálculo) | Sí                        | Sí               |

Se puede ver la lógica empleada por la IA y confirmar que el resultado final sea producto de un procedimiento correcto y no de una casualidad.
Tambien, facilita la identificación y corrección exacta del punto donde pudo haber un fallo en operaciones más complejas.

## Ejercicio 4: Role prompting

| Version        | Vocabulario (sencillo/tecnico) | Usa ejemplos o codigo | A quien le sirve mas                                             |
| -------------- | ------------------------------ | --------------------- | ---------------------------------------------------------------- |
| A. Sin rol     | Sencillo                       | Sí                    | Público usuarios que buscan una respuesta rápida y estándar.     |
| B. Rol docente | Sencillo                       | Sí                    | estudiantes sin experiencia previa en programación.              |
| C. Rol senior  | Técnico                        | Sí                    | Desarrolladores, programadores o profesionales del área técnica. |

## Ejercicio 5: Descomposicion

- **Paso 1:** La IA listó los 5 requisitos principales del sistema (Registrar, Consultar, Actualizar, Eliminar y Controlar stock con alertas).
- **Paso 2:** La IA diseñó la arquitectura proponiendo 5 clases (`Producto`, `Inventario`, `MovimientoStock`, `SistemaInventario` y `Main`) indicando sus atributos y tipos de datos.
- **Paso 3:** La IA generó el código Java encapsulado de la clase `Producto` con su constructor y métodos getters/setters.
- **Paso 4:** La IA analizó la clase `Producto` y sugirió 3 mejoras concretas: validación de datos (precios/stock negativos), autogeneración de ID y sobreescritura del método `toString()`.

**Comparación con el pedido de una sola vez:**
Mientras que el pedido directo entregó una solución completa de golpe pero limitada a solo 3 clases genéricas, el pedido por pasos permitió construir una arquitectura más robusta (incluyendo control de movimientos) y refinar el código de cada clase con un control de calidad detallado en cada etapa.

## Ejercicio 6: Prompt estructurado y autocritica

### Evaluacion del resultado

| Qué revisar                                      | Cumple (Sí / No) |
| ------------------------------------------------ | ---------------- |
| ¿Tiene las 4 columnas pedidas?                   | Sí               |
| ¿Incluye el bloqueo después de 3 intentos?       | Sí               |
| ¿Incluye casos con campos vacíos?                | Sí               |
| ¿Indica qué casos agregó en la autocrítica?      | Sí               |
| ¿Hay algún caso repetido o que no tenga sentido? | No               |

### Prompts utilizados

```text
[Prompt Estructurado]
<rol>Actua como analista de pruebas de software.</rol>

<contexto>Login web con correo y contrasena. La cuenta se bloquea despues de 3 intentos fallidos.</contexto>

<tarea>Piensa paso a paso que puede fallar y escribe 6 casos de prueba.</tarea>

<formato>Tabla con las columnas: ID, escenario, datos de entrada, resultado esperado.</formato>

[Promt de Autocritica]
Revisa tu tabla: faltan casos limite como campos vacios, correo sin @ o contrasena con espacios? Agrega los que falten e indica cuales agregaste
```
