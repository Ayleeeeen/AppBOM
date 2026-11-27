# BD-02 · Inactivar usuario
**Versión / estado:** v0.1 · pendiente de aprobación
**Origen:** `docs/discovery/bom-desk-v0.1.md` v0.1 (aprobado 2026-11-27) · Roadmap BD-02 · Fase 1 · INC-1
**Responsable del Producto:** Ayleen Salcedo

## Historia
Como Administrador, quiero inactivar a un usuario, para que deje de entrar sin perder su registro.

**Resultado:** un usuario inactivado no puede entrar; su registro se conserva y puede reactivarse.

## Alcance
- **Incluye:** inactivar un usuario activo; revocar una invitación pendiente; reactivar un usuario inactivado; impedir que el Administrador elimine usuarios.
- **Excluye:** reasignación de solicitudes de un usuario inactivado (decisión antes de INC-2); recuperación de contraseña; que un Administrador gestione Administradores.
- **Dependencias:** BD-01 (`docs/product/bom-desk-bd-01-v0.1.md`), por los roles de negocio. Reutiliza la gestión de usuarios existente (inactivar, activar, eliminar); Orchestrator verifica la reutilización.

## Decisiones
| ID | Decisión | Fecha |
|---|---|---|
| D-BD02-1 | El Administrador no elimina usuarios; la única baja es inactivar. `superadmin` conserva "Eliminar definitivamente" como herramienta técnica. Antes de INC-2 se revisa la eliminación de usuarios con solicitudes. | 2026-11-27 |
| D-BD02-2 | Se conserva "Activar": un usuario inactivado puede reactivarse con el mismo rol. | 2026-11-27 |

## Reglas
- R1. El Administrador inactiva y reactiva solo usuarios con rol de negocio. `superadmin` además inactiva y reactiva Administradores.
- R2. Ningún usuario se inactiva a sí mismo. Siempre queda al menos un `superadmin` activo.
- R3. Un correo inactivado no puede invitarse de nuevo; se recupera con "Activar".
- R4. Solo `superadmin` elimina definitivamente.

## Criterios de aceptación
- CA-01. Dado un usuario activo de Producción, cuando el Administrador lo inactiva, entonces su estado se muestra inactivo y ese usuario no puede entrar.
- CA-02. Dado un usuario con la sesión abierta, cuando es inactivado, entonces pierde el acceso en su siguiente navegación.
- CA-03. Dada una invitación pendiente, cuando el Administrador la revoca, entonces el enlace de la invitación deja de servir.
- CA-04. Dado un Administrador, cuando intenta inactivarse a sí mismo, o inactivar a otro Administrador o a `superadmin`, incluso forzando la petición, entonces el servidor lo rechaza y los datos no cambian.
- CA-05. Dado un Administrador, cuando abre el menú de un usuario, entonces no ve "Eliminar definitivamente"; si fuerza la petición, el servidor la rechaza y los datos no cambian.
- CA-06. Dado `superadmin`, cuando elimina definitivamente a un usuario de prueba, entonces el usuario desaparece de la lista.
- CA-07. Dado un usuario inactivado de Ingeniería, cuando el Administrador lo reactiva, entonces el usuario vuelve a entrar con el rol Ingeniería.

## Pendientes
- No bloqueante: qué ocurre con las solicitudes de un usuario inactivado o eliminado. Responsable: Ayleen Salcedo. Resolver antes de INC-2.
- Siguiente paso: aprobación de la Responsable del Producto y traspaso a Orchestrator.
