Plan por hitos

Hito 1 · Diseño

Leer la consigna juntos y armar un glosario: oferta vs desafío, solicitud vs contratación, reserva.
Escribir historias de usuario por módulo, con criterios de aceptación tomados de la sección 15 de la consigna.
Hacer el modelo de dominio: entidades, value objects, agregados y multiplicidades.
Diagramar las máquinas de estado de Publicación y Contratación.
Hacer el diagrama de clases en StarUML marcando los patrones.
Hacer un diagrama de secuencia del flujo principal. Lo piden para “recorrer un caso de uso sobre el UML”.
Escribir un borrador del informe con las decisiones de arquitectura.

Hito 2 · Núcleo (sin base de datos)

Configurar el proyecto Maven, JUnit 5, Mockito y JaCoCo.
Programar dominio y value objects, con tests unitarios de cada regla y estado.
Programar los casos de uso con repositorios en memoria (fakes) que implementen los puertos.
Asegurar que funcione la demo publicar → solicitar → aceptar, con validación de estados en tests.
Programar las Strategies, el Decorator de promociones y el Observer, cada uno con su test.

Hito 3 · Infraestructura

Hacer el mapeo JPA (orm.xml o anotaciones), persistence.xml y las migraciones Flyway con datos de demo.
Implementar los repositorios JPA de los mismos puertos. Los casos de uso no cambian, y eso es la prueba de que la arquitectura funciona.
Implementar el UnitOfWork JPA, el optimistic locking y las restricciones UNIQUE.
Programar los adapters mock de identidad, email, push y pasarela.
Escribir tests de persistencia, usando H2 en modo MySQL o Testcontainers, más el test de concurrencia de cupo.

Hito 4 · Producto

Implementar los controllers reales: delgados, con command objects, validación de permisos por userId y un manejo de errores uniforme (por ejemplo un Resultado<T> o una excepción de aplicación mapeada).
Conectar la UI de la cátedra en el Main.
Escribir tests de integración controller → caso de uso → base de datos para los 10 casos de aceptación.
Verificar cobertura de al menos 80 % en dominio y aplicación, y completar README, UML final e informe PDF.
Ensayar la demo y hacer una defensa cruzada: cada uno explica el módulo de otro.
4. Reparto sugerido para 5 personas
Publicaciones y búsqueda/recomendación: State de publicación, Strategy de recomendación, paginación.
Contratación: State de contratación, reprogramación, historial.
Wallet y pagos: SkillCoins, movimientos, Decorator de promociones, política de cancelación.
Perfiles, reputación y calificaciones: Facade del perfil, baja lógica.
Notificaciones e infraestructura transversal: Observer, Adapters, Flyway, Composition Root, CI.