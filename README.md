# NEXA

**Plataforma digital de navegación, articulación y acceso a recursos del ecosistema emprendedor.**

> **Estado:** fase inicial de análisis y definición del producto. Este repositorio comienza con la visión del proyecto y será ampliado conforme se validen los requisitos con su promotor. No existe todavía una versión ejecutable ni una arquitectura tecnológica aprobada.

## 1. ¿Qué es NEXA?

NEXA busca ayudar a personas emprendedoras, proyectos, negocios, empresas e instituciones a identificar sus necesidades, comprender sus próximos pasos y encontrar recursos, formación, orientación, oportunidades y actores con quienes conectarse.

La plataforma no se concibe como siete catálogos aislados. Su principal valor está en **relacionar el perfil y las necesidades del usuario con recursos pertinentes**, mediante un proceso de:

**Diagnóstico → Ruta → Acción → Conexión → Resultado.**

Se contemplan dos dimensiones de un mismo ecosistema: **NEXA Cuba** y **NEXA Global**. Ambas deberán compartir identidad, datos y reglas centrales, con condiciones configurables por territorio, idioma, vigencia y elegibilidad.

## 2. Objetivos

- Facilitar el acceso organizado a información y servicios útiles para emprender o desarrollar negocios.
- Ofrecer un diagnóstico inicial y una ruta de acciones ajustada al perfil y contexto del usuario.
- Conectar emprendedores, empresas, instituciones, proveedores, formadores y entidades de apoyo.
- Difundir información confiable sobre capacitación, normativa, capital y oportunidades.
- Mejorar la visibilidad de actores y capacidades del ecosistema emprendedor.
- Dar seguimiento a acciones y conexiones, distinguiendo resultados declarados de resultados verificados.
- Disponer de una plataforma extensible, preparada para crecer funcional y territorialmente.

## 3. Alcance funcional previsto

La primera versión contempla siete módulos integrados:

| Módulo | Propósito |
| --- | --- |
| **Emprende** | Perfiles, proyectos, diagnóstico y rutas de acción. |
| **Aprende** | Catálogo de cursos, talleres y recursos formativos. |
| **Capital** | Información sobre fuentes de financiamiento y preparación de solicitudes. |
| **Empresas** | Directorio de organizaciones, productos, servicios y capacidades. |
| **Legal** | Consulta de normas, trámites y guías con fuentes y vigencia. |
| **Oportunidades** | Convocatorias, concursos, alianzas y demandas relevantes. |
| **Comunidad** | Publicaciones, intercambio y conexiones entre participantes. |

**Capacidades transversales:**

- Registro, autenticación, perfiles y permisos.
- Diagnóstico configurable y motor de recomendaciones explicables.
- Búsqueda, filtros y navegación entre módulos.
- Gestión de actores, organizaciones, proyectos y recursos relacionados.
- Solicitudes de conexión y seguimiento de estados, según alcance acordado.
- Validación de fuentes, vigencia y flujos de publicación.
- Administración, moderación, auditoría e indicadores básicos.
- **Eventos NEXA:** catálogo y difusión de actividades, articulado con los demás módulos. Su profundidad funcional definitiva está pendiente de validación.

La incorporación de los siete módulos desde la primera versión **no implica automatizar todos sus procesos**. El alcance detallado y los criterios de aceptación de cada módulo se acordarán antes de su implementación.

## 4. Canales de acceso

El producto contempla:

1. **Aplicación Android (APK)** para usuarios finales.
2. **Portal web** adaptable a distintos dispositivos.
3. **Panel administrativo web** para gestión de contenido, verificación y soporte.
4. **Backend y API compartidos** para ofrecer funciones y datos a todos los clientes y permitir futuras integraciones.

Se prestará especial atención a la eficiencia en el consumo de datos y al uso desde entornos con conectividad limitada.

## 5. Arquitectura propuesta (por validar)

Se plantea una arquitectura **API-first**, con un **backend modular** y separación clara de responsabilidades. Inicialmente se priorizará una solución sencilla de desplegar, probar y mantener, sin introducir microservicios por defecto.

```text
          ┌────────────────┐  ┌────────────────┐  ┌─────────────────┐
          │ Android (APK)  │  │ Portal web     │  │ Administración  │
          └────────┬───────┘  └────────┬───────┘  └────────┬────────┘
                   └───────────────────┼───────────────────┘
                                       │
                              API REST / OpenAPI
                                       │
                      ┌────────────────▼────────────────┐
                      │        Backend modular         │
                      │ Identidad · Actores · Recursos │
                      │ Diagnóstico · Rutas · Conexión │
                      │ Contenidos · Eventos · Auditoría│
                      └────────────────┬────────────────┘
                                       │
                          Datos · Archivos · Caché
```

### Stack técnico candidato

| Componente | Tecnología propuesta |
| --- | --- |
| Backend | NestJS + TypeScript |
| Portal web | Next.js + React |
| Panel administrativo | React / Next.js |
| Android | React Native + Expo |
| Base de datos | PostgreSQL |
| Caché y trabajos asíncronos | Redis + BullMQ, si se requieren |
| Documentos y adjuntos | Almacenamiento compatible con S3 |
| Autenticación | Solución IAM compatible con OIDC |
| Interoperabilidad | REST + OpenAPI |
| Despliegue inicial | Linux, proxy inverso y servicios gestionados por systemd, sujeto a infraestructura disponible |

**Estas herramientas son una propuesta del equipo de desarrollo, no decisiones aprobadas.** Podrán ajustarse tras el análisis funcional, operativo y de infraestructura.

## 6. Principios de ingeniería

- **Modelo de datos común:** evitar duplicar usuarios, organizaciones, recursos y oportunidades entre módulos.
- **Seguridad desde el diseño:** controles de acceso en backend, principio de mínimo privilegio y auditoría.
- **Trazabilidad y calidad:** registrar fuentes, responsables, fechas de revisión y vigencia cuando corresponda.
- **Privacidad:** separar información pública y privada, y aplicar minimización de datos.
- **Interoperabilidad:** exponer APIs documentadas y reutilizables por diferentes clientes.
- **Configurabilidad:** cuestionarios, catálogos y reglas de navegación ajustables sin modificar código para cambios simples.
- **Experiencia contextual:** comenzar por las necesidades del usuario, no solo por los nombres de los módulos.
- **Evolución incremental:** entregas pequeñas, pruebas automatizadas y validación frecuente con el promotor.

La primera versión del motor de navegación podrá funcionar con **reglas explícitas y explicables**, sin depender de inteligencia artificial generativa.

## 7. Estrategia de desarrollo

El desarrollo se plantea con un **equipo técnico inicial de dos personas**, apoyado en herramientas de asistencia a la programación, incluida **OpenAI Codex**, con revisión humana del código, decisiones de arquitectura y pruebas.

La estrategia prevista comprende:

1. **Descubrimiento:** validar las decisiones abiertas del expediente, perfiles de usuario, casos prioritarios y fuentes de datos.
2. **Definición:** precisar historias de usuario, modelo de dominio, permisos, flujos y criterios de aceptación.
3. **Diseño técnico:** establecer arquitectura, contratos API, prototipos y estrategia de pruebas.
4. **Construcción iterativa:** desarrollar el núcleo común y los módulos por entregas verificables.
5. **Validación:** ejecutar pruebas funcionales, de integración, seguridad y uso real.
6. **Piloto y puesta en marcha:** desplegar una primera versión, formar a quienes la administrarán y recoger mejoras.

Se estudiará un horizonte **orientativo de 12 a 16 semanas** para una primera versión de alcance básico, condicionado a la validación funcional, disponibilidad de contenidos y capacidad efectiva del equipo. **No constituye un plazo contractual.**

## 8. Aspectos pendientes de definición

Antes de cerrar el backlog de implementación deben validarse, entre otros:

- Responsable del producto y mecanismo de aprobación de requisitos.
- Alcance preciso de cada módulo en la primera entrega.
- Cuestionarios, reglas y ejemplos esperados del diagnóstico y las rutas.
- Fuentes, datos de arranque y responsables de actualización/verificación.
- Países prioritarios de NEXA Global e idiomas iniciales.
- Registro, verificación de perfiles y matriz de permisos.
- Profundidad de Comunidad, Eventos y solicitudes de conexión.
- Necesidades reales de trabajo sin conexión en Android.
- Infraestructura, disponibilidad, copias de seguridad y soporte.
- Políticas de protección de datos y tratamiento de información internacional.

## 9. Alcance excluido por defecto hasta nueva decisión

No se asume inicialmente el desarrollo de una plataforma bancaria o de inversión, custodia de fondos, intermediación financiera, asesoría jurídica definitiva, pagos, chat avanzado, sistema completo de formación virtual ni recomendaciones sofisticadas basadas en IA. Su incorporación requerirá definición funcional y validación específica.

## 10. Estado del repositorio

**Repositorio en inicialización.** Por ahora, contiene únicamente este documento de orientación. Las carpetas de código, configuraciones, decisiones arquitectónicas, pruebas y documentación se añadirán cuando se apruebe el punto de partida técnico.

> **Nota:** Este README recoge la visión inicial de NEXA y propuestas preliminares de ejecución. No sustituye al expediente de requisitos ni constituye un compromiso contractual de alcance, fechas o tecnologías.

---

**NEXA — Conectar necesidades, recursos y oportunidades.**
