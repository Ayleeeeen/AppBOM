# Roadmap — BOM-DESK v0.1
**Fuente:** `docs/discovery/bom-desk-v0.1.md` v0.1 (aprobado por Ayleen Salcedo, 2026-11-27)
**Responsable del Producto:** Ayleen Salcedo
**Actualizado:** 2026-11-27

## Objetivo y límites
- **Objetivo:** centralizar las solicitudes de creación y modificación de BOM, desde que se piden hasta que se aplican en la BOM vigente, con un responsable por paso e historial completo.
- **Metas (UAT del MVP):** 100 % de solicitudes cerradas con trazabilidad completa; 100 % de cambios en BOM vigentes provienen de una solicitud; tiempo de ciclo solo se mide.
- **Fuera de alcance:** correo, Excel, dashboard y alertas (Fase 5), recuperación de contraseña, rol Consulta, ERP/SAP, BOM multinivel, adjuntos, costeo, multi-planta, móvil, firma electrónica.

## Fases e incrementos
| Fase | Incremento | Objetivo | Plazo estimado (no comprometido) | Estado |
|---|---|---|---|---|
| 1 · Usuarios y accesos | INC-1 | Cada persona entra con su rol | 30/11 – 03/12/2026 (4 días) | EN DEFINICIÓN |
| 2 · Solicitudes BOM | INC-2 | Registrar solicitudes completas y recuperarlas por ID | 04/12 – 10/12/2026 (5 días) | BRUTO |
| 3 · Aprobación y aplicación | INC-3 | Cada decisión con responsable; la BOM cambia solo al aplicar | 11/12 – 16/12/2026 (4 días) | BRUTO |
| 4 · Reportes | INC-4 | Medir los indicadores | 17/12 – 22/12/2026 (4 días) | BRUTO |
| 5 · Inicio y dashboard | — | Vista ejecutiva | — | DIFERIDO (visión futura) |

Fechas sin descontar feriados. Capacidad: una responsable más agentes, por verificar.

## Backlog
| ID | Fase / módulo | Historia | Prioridad | Depende de | Incremento | Estado / referencia |
|---|---|---|---|---|---|---|
| BD-01 | F1 · Accesos | Como Administrador, invito a un usuario y le asigno un rol de negocio, para que cada solicitud tenga autor con rol. | 1 | — | INC-1 | PENDIENTE DE APROBACIÓN · `docs/product/bom-desk-bd-01-v0.1.md` v0.1 |
| BD-02 | F1 · Accesos | Como Administrador, desactivo a un usuario, para que deje de entrar. | 2 | BD-01 | INC-1 | PENDIENTE DE APROBACIÓN · `docs/product/bom-desk-bd-02-v0.1.md` v0.1 · UAT 1 |
| BD-03 | F1 · Permisos | Como usuario, veo solo el menú de mi rol y una acción no permitida se bloquea en el servidor sin cambiar datos. | 3 | BD-01 | INC-1 | PENDIENTE DE APROBACIÓN · `docs/product/bom-desk-bd-03-v0.1.md` v0.1 · UAT 2 |
| BD-10 | F2 · Catálogo | Como Ingeniería, consulto productos y materiales (solo lectura), para elegir códigos válidos. | — | INC-1, D-08 | INC-2 | BRUTO |
| BD-11 | F2 · Solicitudes | Como Ingeniería, registro una solicitud de creación de BOM; se rechazan materiales inactivos y cantidades en 0. | — | BD-10 | INC-2 | BRUTO · UAT 3 |
| BD-12 | F2 · Solicitudes | Como Ingeniería, registro una solicitud de modificación de una BOM vigente, con las mismas validaciones. | — | BD-10, D-10 | INC-2 | BRUTO · UAT 3 |
| BD-13 | F2 · Bandeja | Como usuario de negocio, veo "Mis pendientes", para saber qué me toca. | — | BD-11 | INC-2 | BRUTO |
| BD-14 | F2 · Detalle | Como usuario, abro una solicitud por su ID y la recupero tras recargar. | — | BD-11 | INC-2 | BRUTO · UAT 3 |
| BD-20 | F3 · Flujo | Como Producción, apruebo o devuelvo una solicitud; Ingeniería corrige y reenvía. | — | INC-2 | INC-3 | BRUTO · UAT 4 |
| BD-21 | F3 · Flujo | Como Producción, rechazo una solicitud con motivo obligatorio y queda cerrada. | — | BD-20 | INC-3 | BRUTO · UAT 5 |
| BD-22 | F3 · Aplicación | Como Master Data, aplico una solicitud aprobada (la BOM pasa a vN+1 y vN queda en el historial, enlazada) o la devuelvo. | — | BD-20 | INC-3 | BRUTO · UAT 4 |
| BD-23 | F3 · Historial | Como usuario, veo cada evento de la solicitud con usuario, rol, fecha y hora, estado de origen y destino. | — | BD-20 | INC-3 | BRUTO · UAT 6 |
| BD-30 | F4 · Reportes | Como Responsable del Producto, veo solicitudes por estado y cuadran con la bandeja. | — | INC-3 | INC-4 | BRUTO · UAT 7 |
| BD-31 | F4 · Reportes | Como Responsable del Producto, veo el tiempo de ciclo envío → aprobación → aplicación. | — | INC-3 | INC-4 | BRUTO |
| BD-32 | F4 · KPI | Como Responsable del Producto, veo el % de trazabilidad completa y el % de cambios con solicitud; un periodo sin datos se distingue de 0 %. | — | INC-3 | INC-4 | BRUTO · UAT 7 |
| BD-40 | F5 · Dashboard | Vista ejecutiva con indicadores, alertas y accesos rápidos. | — | — | — | DIFERIDO, no comprometido |

## Decisiones
| ID | Tema | Necesaria para | Estado |
|---|---|---|---|
| D-14 | Un rol por usuario | INC-1 | CERRADA · ver BD-01 |
| D-08 | Catálogo y BOM de prueba (prepara la Responsable) | INC-2 | ABIERTA |
| D-10 | Una solicitud abierta por producto | INC-2 | ABIERTA |
| D-IDs | Los IDs BD-xx sustituyen los IDs inconsistentes de los documentos de entrada | Todo | CERRADA en este Roadmap |
| D-CAN | El indicador cuenta solicitudes "canceladas", pero el caso no define quién cancela ni cuándo | INC-3 | ABIERTA · resolver en `/story BD-20` |

## Cambios, deuda y releases
Sin registros.

## Indicadores
| Indicador | Resultado |
|---|---|
| % de solicitudes con trazabilidad completa | POR MEDIR |
| % de cambios en BOM con solicitud | POR MEDIR |
| Tiempo de ciclo | POR MEDIR |
