# BD-01 · Invitar y asignar rol de negocio
**Versión / estado:** v0.1 · pendiente de aprobación
**Origen:** `docs/discovery/bom-desk-v0.1.md` v0.1 (aprobado 2026-11-27) · Roadmap BD-01 · Fase 1 · INC-1
**Responsable del Producto:** Ayleen Salcedo

## Historia
Como Administrador, quiero invitar a un usuario con un rol de negocio y cambiarlo cuando haga falta, para que cada solicitud tenga autor con rol.

**Resultado:** cada persona de prueba entra con uno de los roles Ingeniería, Producción o Master Data.

## Alcance
- **Incluye:** invitar con correo y rol de negocio; cambiar el rol entre los tres roles de negocio; nombres de rol en español en la interfaz; reasignación de los usuarios existentes con rol `user`.
- **Excluye:** desactivar usuarios (BD-02); menú por rol en los módulos BOM (BD-03); recuperación de contraseña; rol Consulta; múltiples roles por usuario; que un Administrador cree Administradores.
- **Dependencias:** ninguna funcional. Reutiliza la gestión de usuarios existente (invitar, cambiar rol); Orchestrator verifica la reutilización.

## Decisiones
| ID | Decisión | Fecha |
|---|---|---|
| D-14 / D-BD01-1 | Un rol por usuario. `user` se reemplaza por Ingeniería, Producción y Master Data; `admin` se muestra como Administrador; `superadmin` se conserva como rol técnico, no asignable desde el panel y sin operar solicitudes. | 2026-11-27 |
| D-BD01-2 | Solo `superadmin` crea o asigna Administradores. El Administrador asigna únicamente roles de negocio. | 2026-11-27 |
| D-BD01-3 | Los usuarios existentes con rol `user` pasan automáticamente a Ingeniería. Riesgo aceptado por la Responsable: reciben permisos de Ingeniería sin revisión individual. | 2026-11-27 |

## Reglas
- R1. Cada usuario tiene exactamente un rol: Ingeniería, Producción, Master Data, Administrador o `superadmin`.
- R2. El Administrador solo asigna Ingeniería, Producción o Master Data. `superadmin` asigna además Administrador. Ningún usuario asigna `superadmin` desde el panel.
- R3. `superadmin` no opera solicitudes BOM.
- R4. Se mantiene el comportamiento vigente ante correo inválido o ya registrado: se muestra un mensaje y no se crea un duplicado.
- R5. Ningún usuario queda con rol `user` después del cambio.

## Criterios de aceptación
- CA-01. Dado un Administrador, cuando invita un correo con rol Producción, entonces la persona se registra, entra y ve su rol "Producción".
- CA-02. Dado un Administrador, cuando abre el selector de rol, entonces solo ve Ingeniería, Producción y Master Data.
- CA-03. Dado un usuario de Ingeniería, cuando el Administrador cambia su rol a Master Data, entonces el nuevo rol persiste tras recargar.
- CA-04. Dado un Administrador, cuando fuerza una petición para asignar Administrador o `superadmin`, entonces el servidor la rechaza y los datos no cambian.
- CA-05. Dado un usuario con rol de negocio, cuando abre directamente la URL de Usuarios, entonces se le deniega el acceso.
- CA-06. Dado `superadmin`, cuando invita a una persona con rol Administrador, entonces esa persona entra como Administrador.
- CA-07. Dado un usuario existente con rol `user`, cuando se aplica el cambio, entonces su rol aparece como Ingeniería y ningún usuario conserva el rol `user`.

## Pendientes
Ninguno material. Siguiente paso: aprobación de la Responsable del Producto y traspaso a Orchestrator.
