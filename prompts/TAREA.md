# Tarea: Mi prompt avanzado

## Tarea elegida

Crear casos de prueba para el formulario de registro de usuarios en una página web.

## Version 1: prompt basico

```text
Dame casos de prueba para un registro de usuarios.
```

- **Técnica agregada:** Ninguna, es un prompt básico.
- **Por qué:** Para ver qué responde la IA por defecto sin darle muchos detalles.
- **Qué mejoró / Limitaciones:** Respondió de forma muy general, sin un formato claro y se saltó validaciones importantes como el correo o la contraseña.

## Version 2

```text
<rol>Actúa como un tester de software (QA).</rol>

<contexto>
Registro de usuarios en una web. Reglas:
- Correo único y válido.
- Contraseña de mínimo 8 caracteres, con 1 número y 1 mayúscula.
- Aceptar términos y condiciones.
</contexto>

<tarea>Escribe 5 casos de prueba para este registro.</tarea>

<formato>Tabla con las columnas: ID, Escenario, Datos de entrada, Resultado esperado.</formato>
```

- **Técnica agregada:** Role Prompting y Prompt Estructurado (etiquetas XML).
- **Por qué:** Para que la IA tome el rol de un probador de software y las etiquetas le dejen claro qué parte es contexto y qué es tarea.
- **Qué mejoró:** Ahora la respuesta viene ordenada en una tabla de 5 casos y respeta las reglas que le puse.

## Version 3: prompt final

```text
<rol>Actúa como un tester de software (QA).</rol>

<contexto>
Registro de usuarios en una web.
Reglas:
- Correo único y válido.
- Contraseña de mínimo 8 caracteres, con 1 número y 1 mayúscula.
- Aceptar términos y condiciones.
</contexto>

<ejemplo_few_shot>
ID: CP-01
Escenario: Registro exitoso
Datos de entrada: Correo: "juan@test.com", Clave: "Hola1234", Términos: Marcado
Resultado esperado: Cuenta creada y mensaje de confirmación.
</ejemplo_few_shot>

<tarea>
Piensa paso a paso qué cosas pueden fallar y genera 6 casos de prueba (3 casos donde todo salga bien y 3 casos de error).
</tarea>

<formato>
Entrega una tabla Markdown con las columnas: ID, Escenario, Datos de entrada, Resultado esperado.
</formato>
```

- **Técnicas agregadas:** Few-Shot (ejemplo) y Chain of Thought (pensar paso a paso).
- **Por qué:** Le di un ejemplo para asegurarme de que me devuelva el formato exacto y le pedí pensar paso a paso para que incluya errores comunes.
- **Qué mejoró:** La lista quedó bien balanceada entre casos correctos y fallos, siguiendo exactamente la estructura del ejemplo.

## Tecnicas usadas en el prompt final

| Parte del Prompt                                | Técnica Aplicada    |
| :---------------------------------------------- | :------------------ |
| `<rol>Actúa como un tester...</rol>`            | Role Prompting      |
| Uso de etiquetas `<contexto>`, `<tarea>`, etc.  | Prompt Estructurado |
| Bloque `<ejemplo_few_shot>`                     | Few-Shot Prompting  |
| "Piensa paso a paso qué cosas pueden fallar..." | Chain of Thought    |

## Evaluacion del resultado

| Qué revisar                                            | Cumple (Sí / No) |
| :----------------------------------------------------- | :--------------: |
| ¿Tiene las 4 columnas pedidas?                         |        Sí        |
| ¿Asigna un rol claro y un formato definido?            |        Sí        |
| ¿Combina al menos 3 técnicas de prompting?             |        Sí        |
| ¿Incluye ejemplo (Few-Shot) y pide pensar paso a paso? |        Sí        |
| ¿Cubre tanto casos de éxito como errores?              |        Sí        |

## Por que elegi estas tecnicas

Elegí estas técnicas porque cuando le pides algo a la IA de forma muy simple, suele dar respuestas incompletas. Ponerle un rol y usar etiquetas le da orden a la instrucción. El ejemplo (Few-Shot) le enseña a la IA exactamente cómo quiero los datos, y pedirle que piense paso a paso ayuda a que no olvide probar los errores típicos que un usuario comete al registrarse.
