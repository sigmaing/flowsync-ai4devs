## Purpose

Esta capability permite que una persona cree su cuenta, entre al espacio compartido y conserve o cierre su sesión. Sin una sesión válida, el sistema no muestra ni modifica ninguna cuenta.

## Requirements

### Requirement: Registro con ingreso automático

El sistema SHALL crear una cuenta con email y contraseña, aceptar el nombre como dato opcional, e iniciar la sesión en el mismo paso, sin invitación ni alta en un equipo.

#### Scenario: Alta con los datos válidos

- **WHEN** una persona sin sesión envía un email no registrado, una contraseña de entre 8 y 32 caracteres y la misma contraseña como confirmación
- **THEN** el sistema crea la cuenta, inicia la sesión y muestra el espacio



#### Scenario: Alta sin nombre

- **WHEN** una persona sin sesión envía un email no registrado y una contraseña válida con su confirmación, y omite el nombre
- **THEN** el sistema crea la cuenta, inicia la sesión y trata la ausencia de nombre como un dato normal



#### Scenario: Email ya registrado

- **WHEN** una persona sin sesión envía un email que ya pertenece a una cuenta
- **THEN** el sistema no crea otra cuenta y explica, junto al email, que ese email ya está registrado



#### Scenario: Confirmación distinta

- **WHEN** una persona sin sesión envía una contraseña y una confirmación que no coincide con ella
- **THEN** el sistema no crea la cuenta y explica que las contraseñas no coinciden



#### Scenario: Contraseña fuera de longitud

- **WHEN** una persona sin sesión envía una contraseña de menos de 8 caracteres o de más de 32
- **THEN** el sistema no crea la cuenta y explica, junto a la contraseña, el límite incumplido



#### Scenario: Email inválido

- **WHEN** una persona sin sesión envía un email que no tiene forma de dirección
- **THEN** el sistema no crea la cuenta y explica, junto al email, que la dirección no es válida



### Requirement: Inicio de sesión

El sistema SHALL iniciar sesión cuando el email y la contraseña corresponden a una cuenta, y SHALL rechazar el acceso cuando no corresponden, con un mensaje comprensible y sin revelar cuál de los dos falló.

#### Scenario: Credenciales correctas

- **WHEN** una persona sin sesión envía el email y la contraseña de una cuenta existente
- **THEN** el sistema inicia la sesión y muestra el espacio



#### Scenario: Credenciales incorrectas

- **WHEN** una persona sin sesión envía un email o una contraseña que no corresponden a una cuenta
- **THEN** el sistema no inicia sesión y muestra que el email o la contraseña no son correctos



### Requirement: Consulta de la cuenta

El sistema SHALL mostrar a la persona con sesión su nombre, su email, sus iniciales y la fecha de alta, y SHALL omitir la contraseña en cualquier respuesta.

#### Scenario: Perfil con nombre

- **WHEN** una persona con sesión y con nombre abre su perfil
- **THEN** el sistema muestra ese nombre, el email, las iniciales derivadas del nombre y la fecha de alta



#### Scenario: Perfil sin nombre

- **WHEN** una persona con sesión y sin nombre abre su perfil
- **THEN** el sistema muestra el email, unas iniciales derivadas del email y la fecha de alta, e indica que no hay nombre



### Requirement: Cierre de sesión

El sistema SHALL cerrar la sesión de forma explícita, dejar de mostrar el espacio y invalidar el acceso usado en esa sesión. Volver a la vista del espacio después de cerrar SHALL llevar de nuevo al inicio de sesión.

#### Scenario: Cierre explícito

- **WHEN** una persona con sesión pide cerrar sesión
- **THEN** el sistema cierra la sesión, invalida ese acceso y muestra el inicio de sesión



#### Scenario: Vuelta a la vista protegida

- **WHEN** una persona acaba de cerrar sesión y abre de nuevo la vista del espacio
- **THEN** el sistema no muestra la cuenta y la lleva al inicio de sesión



### Requirement: Persistencia de la sesión

El sistema SHALL restaurar una sesión guardada cuyo acceso sigue siendo válido, sin pedir de nuevo las credenciales. Si el servidor rechaza ese acceso, el sistema SHALL descartarlo. Si el servidor no puede responder, el sistema SHALL conservar el acceso guardado y SHALL tratar esa visita como sin sesión.

#### Scenario: Recarga con acceso válido

- **WHEN** una persona con sesión guardada y todavía válida recarga la página o vuelve a abrir la aplicación
- **THEN** el sistema restaura la sesión y muestra el espacio sin pedir las credenciales



#### Scenario: Acceso rechazado al restaurar

- **WHEN** una persona vuelve con un acceso que el servidor ya no reconoce
- **THEN** el sistema descarta la sesión guardada y muestra el inicio de sesión indicando que la sesión ha caducado



#### Scenario: Servidor no disponible al restaurar

- **WHEN** una persona vuelve con una sesión guardada y el servidor no responde
- **THEN** el sistema no da la sesión por iniciada en esa visita, conserva el acceso guardado y explica que no ha podido restaurarla



### Requirement: Protección del espacio

El sistema SHALL impedir ver y modificar cualquier cuenta a quien no presenta un acceso válido, y SHALL llevar esas visitas de la interfaz al inicio de sesión.

#### Scenario: Vista del espacio sin sesión

- **WHEN** una persona sin sesión abre una vista del espacio
- **THEN** el sistema no muestra ninguna cuenta y la redirige al inicio de sesión



#### Scenario: Perfil sin acceso válido

- **WHEN** se solicita el perfil sin un acceso válido
- **THEN** el sistema rechaza la petición y no devuelve datos de ninguna cuenta



### Requirement: Mensajes de error comprensibles

El sistema SHALL mostrar los fallos de validación en castellano y junto al campo que falló, y SHALL explicar los fallos de conexión indicando qué hacer. El sistema SHALL evitar que un error técnico crudo llegue a la persona.

#### Scenario: Validación rechazada en un campo visible

- **WHEN** una persona envía el formulario de registro o de inicio de sesión y el servidor rechaza un campo que el formulario muestra
- **THEN** el sistema explica el problema en castellano, junto a ese campo



#### Scenario: Servidor inalcanzable durante un envío

- **WHEN** una persona envía el formulario de registro o de inicio de sesión y no hay conexión con el servidor
- **THEN** el sistema no cambia la sesión y explica que no ha podido conectar y que hay que comprobar que el servidor está en marcha



## Verificación

Lista manual. Marca un escenario solo después de comprobarlo en el código.

### Registro con ingreso automático

- [x] Alta con los datos válidos
  - **Completitud:** completa
  - **Evidencia:** `backend/app/validators/user.ts` (líneas 6-16) exige email, contraseña de 8 a 32 caracteres y confirmación igual. `backend/app/controllers/new_account_controller.ts` (líneas 8-16) crea la cuenta y el token. `frontend/src/auth/auth-provider.tsx` (líneas 91-95) inicia la sesión. `frontend/src/routes/public-only-route.tsx` (línea 13) muestra `/profile` sin invitación. La ruta de alta no lleva `middleware.auth()` (`backend/start/routes.ts`, líneas 20-26).
- [x] Alta sin nombre
  - **Completitud:** completa
  - **Evidencia:** `backend/app/validators/user.ts` (línea 13) declara `fullName` nullable. `frontend/src/pages/register-page.tsx` (línea 42) envía `null` si el nombre va en blanco, y el rótulo lo marca opcional (líneas 64-68). No hay rechazo por nombre ausente.
- [x] Email ya registrado
  - **Completitud:** completa
  - **Evidencia:** `email().unique({ table: 'users', column: 'email' })` en `backend/app/validators/user.ts` (línea 14). `frontend/src/lib/api.ts` (líneas 50-52) traduce `database.unique` del email a «Ese email ya está registrado…». `frontend/src/auth/use-auth-form.ts` (líneas 35-49) lo deja en el campo, y `frontend/src/pages/register-page.tsx` (líneas 98-99) lo pinta bajo el email.
- [x] Confirmación distinta
  - **Completitud:** completa
  - **Evidencia:** `frontend/src/pages/register-page.tsx` (líneas 34-36) corta el envío y muestra «Las contraseñas no coinciden.». El servidor repite la regla con `sameAs('password')` en `backend/app/validators/user.ts` (línea 16), y `frontend/src/lib/api.ts` (líneas 54-55) traduce esa regla a la misma frase.
- [x] Contraseña fuera de longitud
  - **Completitud:** completa
  - **Evidencia:** `minLength(8).maxLength(32)` en `backend/app/validators/user.ts` (línea 7), aplicada a contraseña y confirmación. `frontend/src/lib/api.ts` (líneas 60-63) explica el mínimo o el máximo junto al campo, y `frontend/src/pages/register-page.tsx` (líneas 118-119) lo muestra bajo la contraseña. El `minLength={8}` del input no es la barrera: el formulario usa `noValidate`.
- [x] Email inválido
  - **Completitud:** completa
  - **Evidencia:** `vine.string().email()` en `backend/app/validators/user.ts` (línea 6). `frontend/src/lib/api.ts` (líneas 56-57) traduce la regla `email` a «Introduce una dirección de email válida.», pintada bajo el campo.



### Inicio de sesión

- [x] Credenciales correctas
  - **Completitud:** completa
  - **Evidencia:** `backend/app/validators/user.ts` (líneas 23-26) exige email y contraseña. `backend/app/controllers/access_tokens_controller.ts` (líneas 8-16) comprueba las credenciales con `User.verifyCredentials`, crea el token y devuelve la cuenta. `frontend/src/lib/api.ts` (líneas 149-153) llama a `POST /api/v1/auth/login`. `frontend/src/auth/auth-provider.tsx` (líneas 84-88) inicia la sesión. `frontend/src/routes/public-only-route.tsx` (línea 13) muestra `/profile`. La ruta de login no lleva `middleware.auth()` (`backend/start/routes.ts`, líneas 20-26).
- [x] Credenciales incorrectas
  - **Completitud:** completa
  - **Evidencia:** `User.verifyCredentials` (`backend/app/controllers/access_tokens_controller.ts`, línea 10) rechaza email o contraseña que no corresponden, con un 400 sin campo. `frontend/src/lib/api.ts` (líneas 82-85) lo traduce a «El email o la contraseña no son correctos.», sin decir cuál falló. `frontend/src/pages/login-page.tsx` (líneas 23 y 36-39) muestra ese aviso y no inicia sesión.



### Consulta de la cuenta

- [x] Perfil con nombre
  - **Completitud:** completa
  - **Evidencia:** `GET /api/v1/account/profile` exige sesión (`backend/start/routes.ts`, líneas 28-35). `backend/app/controllers/profile_controller.ts` (líneas 5-6) devuelve el usuario autenticado a través de `UserTransformer`. Ese transformer (`backend/app/transformers/user_transformer.ts`, líneas 5-13) incluye `fullName`, `email`, `createdAt` e `initials`, y no incluye `password`; la columna además tiene `serializeAs: null` (`backend/database/schema.ts`, líneas 46-47). Las iniciales salen del nombre (`backend/app/models/user.ts`, líneas 11-14). `frontend/src/routes/app-routes.tsx` (líneas 16-17) abre `/profile` solo con sesión, y `frontend/src/pages/profile-page.tsx` (líneas 36-55) muestra las iniciales, el nombre, el email y la fecha de alta.
- [x] Perfil sin nombre
  - **Completitud:** completa
  - **Evidencia:** sin `fullName`, `backend/app/models/user.ts` (líneas 12-16) calcula las iniciales a partir del email. `frontend/src/pages/profile-page.tsx` (líneas 39-44 y 51-55) muestra «Sin nombre», el email y la fecha de alta. La respuesta sigue sin contraseña: `UserTransformer` no la selecciona (`backend/app/transformers/user_transformer.ts`, líneas 6-12).



### Cierre de sesión

- [x] Cierre explícito
  - **Completitud:** completa
  - **Evidencia:** `frontend/src/pages/profile-page.tsx` (líneas 24-27 y 60-67) pide el cierre desde el perfil. `frontend/src/auth/auth-provider.tsx` (líneas 23-28 y 98-106) borra la sesión local y después llama a `POST /api/v1/account/logout` (`frontend/src/lib/api.ts`, líneas 162-165). `backend/app/controllers/access_tokens_controller.ts` (líneas 19-23) elimina el token de esa sesión. La ruta exige sesión (`backend/start/routes.ts`, líneas 28-35). Al quedar el estado en `anonymous`, `frontend/src/routes/protected-route.tsx` (línea 13) muestra el inicio de sesión. Si esa llamada falla, la sesión local ya está cerrada y el token del servidor no se borra.
- [x] Vuelta a la vista protegida
  - **Completitud:** completa
  - **Evidencia:** tras el cierre, el estado queda en `anonymous` (`frontend/src/auth/auth-provider.tsx`, líneas 23-27). `frontend/src/routes/app-routes.tsx` (líneas 16-17) deja `/profile` detrás de `ProtectedRoute`, y `frontend/src/routes/protected-route.tsx` (línea 13) redirige a `/login` sin pintar la cuenta.



### Persistencia de la sesión

- [ ] Recarga con acceso válido
- [ ] Acceso rechazado al restaurar
- [ ] Servidor no disponible al restaurar



### Protección del espacio

- [ ] Vista del espacio sin sesión
- [ ] Perfil sin acceso válido



### Mensajes de error comprensibles

- [ ] Validación rechazada en un campo visible
- [ ] Servidor inalcanzable durante un envío



## Cierre

1. Requisitos generados y comprobados. El agente escribió 7 requisitos. Se comprobaron 4 consultando el código.
2. Incoherencias detectadas. El email se limita a 254 caracteres en `backend/app/validators/user.ts` (línea 6) y ese máximo no se indica en el registro (`frontend/src/pages/register-page.tsx`, líneas 86-99) .
3. Comportamientos que no supiste clasificar como bug o contrato. En `frontend/src/pages/login-page.tsx` (líneas 25-28) el inicio de sesión envía la contraseña en claro dentro del cuerpo JSON; `frontend/src/lib/api.ts` (líneas 116 y 149-153) reserva `Authorization` para el token y no fuerza HTTPS (el ejemplo es `http://localhost:3333`). Puede ser el contrato: el servidor espera email y contraseña en el cuerpo y el cifrado corresponde al transporte. Puede ser un fallo: sin TLS, quien vea la petición lee la contraseña, y el código no dice si HTTP es solo para desarrollo o si la contraseña no debería viajar así. Nada en el cliente ni en el validador de login distingue esas dos lecturas.

