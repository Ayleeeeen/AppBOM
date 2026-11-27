# Caso de negocio — BOM-DESK · Gestión de solicitudes BOM (MVP)
**Versión / estado:** borrador v0.1 · pendiente de aprobación humana
**Responsable del Producto:** Ayleen Salcedo
**Fuentes:** `docs/discovery/inputs/` — BOM-DESK · Roadmap de implementación v1.0 (principal), CasoUso v 1.0, Plan_Piloto_BOM v0.1, Roadmap_Alcance_Tickets_GestionBOM, TO-DO.txt. No revisado: Modelo_Estructura_Consultiva_MBC_Data_IA_Mineria (sin PDF).
**Contexto:** producto real; el MVP se construye y opera con usuarios de prueba. No hay empresa adoptante todavía. El piloto también aplica la metodología de agentes, pero su evaluación no forma parte de este caso.

- **Problema (hipótesis de diseño, sin evidencia medida):** en empresas manufactureras, los cambios a las listas de materiales (BOM) se gestionan sin control, historial ni trazabilidad entre Ingeniería, Producción y Master Data. Síntomas supuestos: solicitudes por correo y Excel que se pierden o duplican; datos incompletos (cantidades, motivo, sustento) que generan errores de estructura; responsables poco claros que retrasan aprobaciones; ausencia de registro de quién cambió qué y cuándo. No hay datos de frecuencia, volumen ni impacto. Si no se actúa, la hipótesis queda sin validar y no existe un producto para ofrecer.

- **Objetivo:** centralizar las solicitudes de creación y modificación de BOM, desde que se piden hasta que se aplican en la BOM vigente, con un responsable por paso e historial completo.
  - Meta 1: 100 % de las solicitudes de prueba cerradas con trazabilidad completa durante el UAT del MVP.
  - Meta 2: 100 % de los cambios en BOM vigentes provienen de una solicitud durante el UAT.
  - El impacto real sobre el proceso se medirá con el primer adoptante.

- **Solución y alcance:** opción C, plataforma web centralizada sin integraciones (BOM-DESK). Se descartaron "no actuar" (no alcanza el objetivo) y "mejorar el proceso con formulario y lista compartida" (no garantiza que la BOM cambie solo mediante una solicitud).
  - **Incluye:** solicitudes de creación y modificación; cuatro roles (Ingeniería solicita; Producción revisa, aprueba, devuelve o rechaza; Master Data aplica o devuelve; Administrador invita, asigna rol y desactiva); validaciones automáticas de materiales al registrar; rechazo con motivo obligatorio; avisos solo dentro de la app (bandeja "Mis pendientes"); catálogo mínimo de productos y materiales de solo consulta; historial por solicitud; BOM vigente versionada; reportes con tres indicadores.
  - **Excluye (No Goals):** notificaciones por correo; exportar a Excel; dashboard ejecutivo y alertas de atraso; recuperación de contraseña propia; rol Consulta; integración con ERP/SAP; BOM multinivel; adjuntos; costeo, rutas de fabricación, multi-planta, app móvil y firma electrónica.

- **Fases a alto nivel:**
  | Fase | Objetivo | Alcance general | Beneficiario | Valor | Estado |
  |---|---|---|---|---|---|
  | 1 · Usuarios y accesos | Cada persona entra con su rol | Acceso, roles, administración de accesos, permisos en servidor | Administrador | Cada solicitud tendrá autor con rol | MVP |
  | 2 · Solicitudes BOM | Registrar solicitudes completas y recuperarlas por ID | Catálogo, creación, modificación, validación de líneas, bandeja, detalle | Ingeniería | Un solo canal con datos completos | MVP |
  | 3 · Aprobación y aplicación | Cada decisión con responsable; la BOM cambia solo al aplicar | Estados, devolver, aprobar, rechazar, aplicar con versión | Producción y Master Data | Control y registro de decisiones | MVP |
  | 4 · Reportes | Medir los indicadores | Trazabilidad, reportes por estado, tiempo de ciclo, KPI | Responsable del Producto | Metas verificables | MVP |
  | 5 · Inicio y dashboard | Vista ejecutiva | Indicadores con fecha de corte, alertas, accesos rápidos | Jefaturas | Visibilidad gerencial | Visión futura, no comprometida |

- **Beneficiarios y beneficios (esperados, no comprobados):**
  - Ingeniería (usuario principal, directo): pedir cambios sin perseguir por correo → un canal y estado visible.
  - Producción (directo): revisar la estructura antes de su vigencia → decisiones sobre solicitudes completas y registradas.
  - Master Data (directo): recibir datos completos y códigos válidos → aplica solo lo aprobado y prevalidado.
  - Administrador (directo, secundario): controlar accesos → accesos centralizados.
  - Jefaturas / Responsable del Producto (indirecto): saber si el proceso está bajo control → trazabilidad y tiempos medidos.
  - Beneficio de negocio priorizado: ningún cambio de BOM sin solicitud, responsable e historial.

- **Entrega de valor:**
  - **Entregable mínimo:** MVP de las fases 1 a 4, operando con tres usuarios de prueba (uno por rol de negocio) más el Administrador.
  - **Criterios de aceptación UAT:**
    1. El Administrador invita, asigna rol y desactiva a un usuario; un usuario desactivado no entra.
    2. Cada rol ve solo su menú; una acción no permitida forzada se bloquea en el servidor sin cambiar datos.
    3. Ingeniería registra una creación y una modificación; se rechazan materiales inactivos y cantidades en 0; ambas se recuperan por ID tras recargar.
    4. Una solicitud recorre devolución → corrección → aprobación (Producción) → aplicación (Master Data); la BOM pasa a vN+1 y vN queda en el historial, enlazada.
    5. El rechazo exige motivo y cierra la solicitud.
    6. El historial muestra cada evento con usuario, rol, fecha y hora, estado de origen y destino, sin saltos.
    7. Los reportes cuadran con la bandeja y con un conteo manual; el KPI distingue un periodo sin datos de uno con 0 %.
  - **Indicadores** (responsable de medición: Ayleen Salcedo; periodo: UAT del MVP):
    | Indicador | Qué mide | Línea base | Meta | Método / fuente |
    |---|---|---|---|---|
    | % de solicitudes con trazabilidad completa | Solicitudes cerradas (aplicada, rechazada, cancelada) que cumplen las 4 condiciones del Plan Piloto §4.6 | No existe; se medirá con el primer adoptante, mismas 4 condiciones | 100 % (datos de prueba) | Reporte del KPI contrastado con conteo manual |
    | % de cambios en BOM vigentes que provienen de una solicitud | Versiones de BOM con solicitud de origen | No existe | 100 % (datos de prueba) | Comparación de versiones con solicitudes aplicadas |
    | Tiempo de ciclo | Días de envío → aprobación → aplicación | No existe | Sin meta; solo se mide | Reporte de tiempos |
  - La aceptación UAT prueba el funcionamiento; no demuestra impacto en el negocio.

- **Estimación para PMO:**
  - **Plazo (estimación del Excel, ajustada):** 17 días hábiles desde el 30/11/2026 (F1: 4, F2: 5, F3: 4, F4: 4); cierre aproximado el 22/12/2026, sin descontar feriados. Las fechas de fin del Excel tienen fórmulas rotas (`#¡REF!`). Los 31 tickets / 96 puntos incluyen la Fase 5 y deben reajustarse.
  - **Costo:** por precisar. Componentes declarados: suscripción Claude Pro (recurrente), laptops y otros no detallados. Posibles costos recurrentes de servicios de autenticación y base de datos, por verificar.
  - **Restricciones:** no se construye sin definición aprobada; un módulo a la vez; permisos en el servidor; sin dependencias nuevas sin decisión.
  - **Dependencias:** catálogo y BOM de prueba preparados por la Responsable (D-08); tres usuarios de prueba; proveedor de autenticación (el repositorio ya contiene uno; su reutilización la verifica Roadmap / Orchestrator).
  - **Supuestos:** BOM de un nivel; una solicitud abierta por producto (D-10); un rol por usuario (D-14); Producción no crea solicitudes.
  - **Riesgos:**
    | Riesgo | Consecuencia | Prob. | Impacto | Mitigación |
    |---|---|---|---|---|
    | El problema es una hipótesis | El producto no responde a una necesidad real | Por evaluar | Alto | Validar con el primer adoptante y medir la línea base allí |
    | Decisiones abiertas (D-08, D-10, D-14, IDs inconsistentes entre documentos) | Retrabajo | Media | Medio | Cerrarlas antes de la fase que las necesita; Roadmap unifica los IDs |
    | Capacidad: una responsable más agentes, con límites de uso de la suscripción | Atraso del plazo | Media | Medio | Roadmap verifica capacidad; una fase a la vez |
    | Entorno de trabajo (PATH, Node, permisos; ya ocurrió) | Días perdidos | Media | Bajo | Checklist de arranque y prueba inicial |
    | Desvío de alcance por los agentes | Funciones no pedidas | Media | Medio | Este caso es la única fuente; Review controla contra la spec |
    | Datos de prueba poco representativos | Metas del 100 % triviales | Media | Bajo | Incluir casos negativos y devoluciones en el UAT |
  - **Compatibilidad preliminar:** alcance y plazo son coherentes con la estimación del Excel. El costo no está cuantificado, así que no se declara factibilidad ni se comprometen recursos.

- **Dictamen Discovery: LISTO PARA REVISIÓN.** Problema registrado como hipótesis aceptada por la Responsable del Producto; objetivo evaluable; alternativa justificada; alcance, exclusiones y fases confirmados; criterios UAT e indicadores con método, periodo y responsable.
  - Condiciones: la línea base queda diferida al primer adoptante; el costo está por precisar (no crítico para planificar).
  - Este dictamen no valida el valor de negocio ni constituye aprobación.
