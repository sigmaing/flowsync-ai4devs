# Prompts

Aquí van **todos los prompts que lanzaste** para hacer el ejercicio, en el orden en que los
lanzaste, con el modelo y la herramienta de cada uno.

Esto no es papeleo. Lo que se revisa es **cómo pediste las cosas**, no solo lo que salió: un
resultado flojo con un prompt bueno y un resultado flojo con un prompt vago necesitan feedback
distinto, y sin este archivo no se distinguen.

## Cómo rellenarlo

- Un apartado `## Prompt N` por cada prompt.
- **Pega el prompt tal cual lo lanzaste**, dentro del bloque de código, aunque ocupe diez líneas
  y aunque tenga faltas. No lo reescribas para que quede bien: el que arreglaste mentalmente
  después no es el que lanzaste.
- Incluye también los que **no funcionaron**. Suelen ser los más útiles de leer.
- `Modelo` y `Herramienta` en todos. Si cambiaste de una a otra a mitad, se nota aquí.

---

## Prompt 1

**Modelo:** Auto
**Herramienta:** Cursor

```
Vamos  a estudiar el alcance y el backlog de Flowsync los archivos estan en  docs
```

**Qué salió:** funcionó a la primera.

## Prompt 2

**Modelo:** Auto
**Herramienta:** Cursor

```
Muy bien ahora vamos a estudiar el codigo las capas de frontend y backend solo el módulo de cuentas y acceso, no amplies este alcance de estudio
```

**Qué salió:** funcionó a la primera; se quedó en cuentas y acceso.

## Prompt 3

**Modelo:** Auto
**Herramienta:** Cursor

```
Perfecto ahora documentemos en el archivo @docs/spec-viva/cag.md, las especificaciones deben quedar en este formato obligatorio:

## Purpose: una o dos frases que expliquen para qué existe esta capability.

## Requirements: sección que contiene los requisitos, cada uno encabezado por ### Requirement: y redactado con SHALL para indicar lo que debe hacer el sistema.

#### Scenario:: al menos uno por requisito, con dos viñetas: **WHEN***. Incluye las precondiciones dentro de WHEN, sin utilizar GIVEN.

Idioma: español, excepto las palabras clave de la RFC.
```

**Qué salió:** funcionó a la primera. La segunda viñeta no venía nombrada; se escribió WHEN y THEN.

## Prompt 4

**Modelo:** Auto
**Herramienta:** Cursor

```
Vamos a poner un checklist de verificación para los requisitos, indicando cuales han sido comprobados en código, el checklist es manual, no lo diligencies
```

**Qué salió:** pasó a plan y no escribió el checklist hasta confirmarlo.

## Prompt 5

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** funcionó. Checklist vacío, una casilla por escenario.

## Prompt 6

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** el mismo plan del checklist, reenviado. Ya estaba hecho.

## Prompt 7

**Modelo:** Auto
**Herramienta:** Cursor

```
Muy bien a hora vamos a validar Requirement: Registro con ingreso automático, cada uno de sus excenarios incluye la evidencia citando el codigo e indicando su completiud, no  modifiques el requemiento, adicina esta validación en la seccion del checklist
```

**Qué salió:** pasó a plan. No escribió la evidencia hasta confirmarlo.

## Prompt 8

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** funcionó. Seis escenarios de registro con evidencia y completitud, casillas sin marcar.

## Prompt 9

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** el mismo plan de registro, reenviado. Ya estaba hecho.

## Prompt 10

**Modelo:** Auto
**Herramienta:** Cursor

```
Perfecto ahora hagamoslo para rel requerimiento de Inicio de sesión
```

**Qué salió:** funcionó a la primera, sin volver a pasar por un plan.

## Prompt 11

**Modelo:** Auto
**Herramienta:** Cursor

```
Ahora con el requisito Consulta de la cuenta
```

**Qué salió:** funcionó a la primera.

## Prompt 12

**Modelo:** Auto
**Herramienta:** Cursor

```
Ahora con el requisito Cierre de sesión
```

**Qué salió:** funcionó a la primera.

## Prompt 13

**Modelo:** Auto
**Herramienta:** Cursor

```
Muy bien ahora vamos a cerrar el ejercicio en @docs/spec-viva/cag.md , al final vamos a poner esto: 1. Requisitos generados y comprobados. Indica cuántos requisitos escribió el agente y cuántos verificaste tú consultando el código. Escribe ambos números, sin redondearlos ni justificarlos. Comprobar significa revisar el código para confirmar el comportamiento, no limitarse a leer un requisito que parece correcto.
```

**Qué salió:** pasó a plan. Propuso 7 escritos y 4 comprobados.

## Prompt 14

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** funcionó. Se añadió el cierre con 7 y 4, sin justificar la diferencia.

## Prompt 15

**Modelo:** Auto
**Herramienta:** Cursor

```
Implement the plan as specified, it is attached for your reference. Do NOT edit the plan file itself.

To-do's from the plan have already been created. Do not create them again. Mark them as in_progress as you work, starting with the first one. Don't stop until you have completed all the to-dos.
```

**Qué salió:** el mismo plan del cierre, reenviado. Ya estaba hecho.

## Prompt 16

**Modelo:** Auto
**Herramienta:** Cursor

```
ahora respondamos esto 2. Incoherencias detectadas. Anota cada inconsistencia en una línea e indica dónde aparece. No necesitas buscarlas expresamente: pueden surgir al intentar describir como regla general un comportamiento que no se cumple en todas las partes del sistema.
hallazgo: en @backend/app/validators/user.ts  el correo no indica el maxlengt del correo y se tiene esto const email = () => vine.string().email().maxLength(254)
```

**Qué salió:** funcionó. Se añadió una línea en el cierre. El hallazgo señala el validador; en la interfaz el máximo no se muestra.

## Prompt 17

**Modelo:** Auto
**Herramienta:** Cursor

```
Las contraseñas se guardan en texto plano
```

**Qué salió:** se respondió en el chat y no se escribió en el cierre. La afirmación no se sostiene: el modelo hashea con scrypt antes de guardar.

## Prompt 18

**Modelo:** Auto
**Herramienta:** Cursor

```
3. Comportamientos que no supiste clasificar como bug o contrato. Incluye al menos un caso en el que hayas encontrado un comportamiento y no tengas claro si es un error o si el sistema está diseñado para funcionar así. Explica brevemente las dos posibilidades y por qué el código no permite saber cuál es la correcta.

Hallazgo: en este @frontend/src/pages/login-page.tsx , la funcion login @login-page.tsx (25-28)  envia la contraseña en texto plano, y en el payload de la peticion, no en las cabeceras para este fin, esto puede ser un riesgo de seguridad si no se transmite por https
```

**Qué salió:** funcionó. Se añadió el punto 3 con las dos lecturas. Iba adjunto el fragmento de `handleSubmit` (líneas 25-28).
