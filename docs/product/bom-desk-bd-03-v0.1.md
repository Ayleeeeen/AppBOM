# BD-03 · Menú por rol y bloqueo en servidor
**Versión / estado:** v0.1 · pendiente de aprobación
**Origen:** `docs/discovery/bom-desk-v0.1.md` v0.1 (aprobado 2026-11-27) · Roadmap BD-03 · Fase 1 · INC-1 · UAT 2
**Responsable del Producto:** Ayleen Salcedo

## Historia
Como usuario de cualquier rol, quiero ver solo los módulos de mi rol y que el sistema impida lo que no me corresponde, para operar sin errores ni accesos indebidos.

**Resultado:** existe una matriz única de permisos para todo el MVP; en la Fase 1 se aplica a las pantallas existentes y cada historia de las fases 2 a 4 la hereda.

## Alcance
- **Incluye:** la matriz de permisos del MVP; su aplicación al menú y al servidor en Inicio, Perfil, Ajustes y Usuarios; denegación por defecto.
- **Excluye:** construir los módulos BOM (fases 2 a 4); permisos por registro, sede u organización; roles adicionales.
- **Dependencias:** BD-01 (`docs/product/bom-desk-bd-01-v0.1.md`), por los roles de negocio.

## Decisiones
| ID | Decisión | Fecha |
|---|---|---|
| D-BD03-1 | BD-03 fija la matriz de permisos de todo el MVP y la aplica en la Fase 1 a las pantallas existentes. El UAT 2 completo se cierra en INC-3. | 2026-11-27 |
| D-BD03-2 | Reportes: lectura para Ingeniería, Producción, Master Data y Administrador. | 2026-11-27 |
| D-BD03-3 | Administrador consulta Catálogo y solicitudes en solo lectura. `superadmin` ve Reportes. | 2026-11-27 |

## Matriz de permisos del MVP
| Módulo / acción | Ingeniería | Producción | Master Data | Administrador | superadmin | Fase |
|---|---|---|---|---|---|---|
| Inicio, Perfil, Ajustes | Sí | Sí | Sí | Sí | Sí | 1 |
| Usuarios (invitar, rol, inactivar, activar) | No | No | No | Sí | Sí | 1 |
| Catálogo (consulta) | Sí | Sí | Sí | Lectura | No | 2 |
| Crear y corregir solicitud | Sí | No | No | No | No | 2–3 |
| Mis pendientes y detalle de solicitud | Sí | Sí | Sí | Lectura | No | 2 |
| Aprobar, devolver, rechazar | No | Sí | No | No | No | 3 |
| Aplicar, devolver | No | No | Sí | No | No | 3 |
| Reportes | Lectura | Lectura | Lectura | Lectura | Lectura | 4 |

## Reglas
- R1. Denegación por defecto: un módulo o acción que no figura en la matriz como permitido está denegado.
- R2. Ocultar una opción del menú no basta: cada acción se valida también en el servidor.
- R3. Un usuario inactivo o con un rol no reconocido no accede a ningún módulo.
- R4. Cada historia de las fases 2 a 4 incluye criterios de acceso permitido y denegado coherentes con esta matriz. Un cambio en la matriz requiere una nueva versión de esta historia.

## Criterios de aceptación (Fase 1)
- CA-01. Dado un usuario de Ingeniería, Producción o Master Data, cuando entra, entonces su menú muestra Inicio, Perfil y Ajustes, y no muestra Usuarios.
- CA-02. Dado un Administrador o `superadmin`, cuando entra, entonces su menú muestra además Usuarios.
- CA-03. Dado un usuario de rol de negocio, cuando fuerza una petición de gestión de usuarios (invitar, cambiar rol o inactivar), entonces el servidor la rechaza y los datos no cambian.
- CA-04. Dado un usuario con un rol no reconocido, cuando intenta entrar, entonces no accede a ningún módulo.
- CA-05. Dado el acceso directo por URL a Usuarios con un rol de negocio, entonces aplica BD-01 CA-05.

## Pendientes
- No bloqueante: el UAT 2 completo (módulos BOM) se verifica en INC-3 con los criterios de acceso de cada historia. Responsable: Ayleen Salcedo.
- Siguiente paso: aprobación de la Responsable del Producto y traspaso a Orchestrator.
