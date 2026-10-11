# SkillSwap – TP Procesos de Desarrollo de Software

## Contexto
Consigna completa en docs/consignas.pdf. Material de clase en docs/clases/.
Es un TP académico: el código debe ser explicable por estudiantes.
Priorizar claridad sobre sofisticación. Nada de patrones "por las dudas".

## Stack (obligatorio)
- Java 21, Maven, Hibernate 6 / JPA (Jakarta), MySQL 8, Flyway
- SIN Spring. Inyección manual en Main (Composition Root)
- Tests: JUnit 5, Mockito, AssertJ, JaCoCo (>=80% dominio y aplicación)

## Arquitectura (Clean Architecture)
- domain: entidades, value objects, estados, políticas, eventos. NO importa jakarta.persistence ni nada externo.
- application: casos de uso, puertos (interfaces de repos, notificador, identidad, UnitOfWork), DTOs/commands.
- infrastructure: JPA (mapeo vía orm.xml), repositorios, adapters mock, Flyway.
- controllers: delgados, validan entrada y permisos por userId, delegan en casos de uso, manejo de errores uniforme.
- Las dependencias apuntan siempre hacia domain.

## Patrones acordados
State (Publicacion, Contratacion), Strategy (recomendación, política de cancelación),
Observer (eventos → notificaciones), Adapter (identidad, email, push, pasarela),
Decorator (promociones, nunca total negativo), Simple Factory (canal de notificación),
Facade (perfil público). Cada patrón debe tener test que lo demuestre.

## Reglas de trabajo
- Trabajar SOLO en la fase pedida. No adelantar fases.
- Antes de codear, proponer un plan y esperar aprobación.
- Cada regla de negocio con su test, incluidos casos negativos.
- Al terminar: correr `mvn test` y resumir qué se hizo, qué decisiones se tomaron y por qué (para el informe).
- Nombres de dominio en español, como en la consigna.

## Decisiones técnicas clave
- Transacciones: puerto UnitOfWork en application, implementación JPA en infra.
- Sobreventa de cupo: @Version (optimistic locking) en Publicacion + test concurrente.
- Doble cobro: validación por estado + UNIQUE(contratacion_id, tipo) en movimientos.
- Débito y crédito de SkillCoins en una única transacción; saldo insuficiente → rollback total.
- HistorialEstado inmutable (solo insert): fecha, actor, motivo.
- Baja lógica de perfiles.
- Búsqueda: JOIN FETCH o proyecciones a DTO (evitar N+1), paginación en todos los listados.
- Flyway: V1 esquema, V2 índices/constraints, V3 datos demo. Nada de hbm2ddl.
- Value objects: SkillCoins, FranjaHoraria, UserId, Motivo, Puntaje.