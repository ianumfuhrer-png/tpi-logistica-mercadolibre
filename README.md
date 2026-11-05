# TPI Organización Empresarial: Módulo de Gestión de Logística (Mercado Libre)

Trabajo Práctico Integrador y Progresivo (TPI). Tecnicatura Universitaria en Programación a Distancia, Universidad Tecnológica Nacional (UTN).

## Descripción del sistema

El proyecto propone mejorar el **Módulo de Gestión de Logística** del ecosistema de Mercado Libre con dos funciones:

- **Motor de consolidación de envíos:** agrupa en un solo paquete hasta 5 objetos, incluso de distintos vendedores.
- **Seguimiento en mapa en tiempo real:** muestra la posición y la localidad del paquete, y notifica a cada comprador solo cuando se entregó el pedido anterior de la ruta del repartidor.

Este repositorio aloja la documentación técnica del proyecto.

## Integrantes

- Ian Uriel Umfuhrer

## Enlaces

- Tablero de gestión (GitHub Projects): https://github.com/users/ianumfuhrer-png/projects/1

## Contenido del repositorio

| Carpeta o archivo | Descripción |
|---|---|
| `entregas/TPI_Consolidado.pdf` | Versión final del TPI (integra las cuatro entregas) |
| `entregas/` | Entregas parciales 1, 2, 3 y 4 |
| `diagramas/` | BPMN, organigrama y diagrama de sistema abierto |
| `docs/proceso_bpmn.md` | Proceso de envío consolidado modelado en BPMN |
| `docs/diccionario_de_datos.md` | Diccionario de datos inicial |
| `docs/historias_de_usuario.md` | Las tres historias de usuario del backlog |
| `docs/indicadores_de_control.md` | Indicadores y estándares de control |

## Flujo de trabajo

- La rama `main` solo se actualiza mediante Pull Requests.
- Cada documento se desarrolla en una rama `feature/...`.
- Mensajes de commit claros y descriptivos que empiezan con un verbo (por ejemplo `Agregar diagrama BPMN del envío consolidado`).
- La revisión del PR fue realizada por el propio autor por tratarse de un trabajo individual; los comentarios y correcciones quedan documentados en el PR.

## Declaración de Uso de IA

Se utilizó la IA **Claude (Anthropic)** como asistente a lo largo de las cuatro entregas y en la consolidación, con estos propósitos:

1. **Entrega 1:** recolectar información sobre Mercado Libre y recibir ideas de cómo ordenar el trabajo.
2. **Entrega 2:** diseñar el diagrama de Gantt, que no pudo realizarse en OpenProject, y mejorar la redacción y la estructura gramatical.
3. **Entregas 3:** corregir la ortografía, la gramática y proponer cómo armar la Figura 1 (organigrama) de acuerdo con lo establecido en las Entregas N.º 1 y N.º 2 
4. **Entregas 4:** Usando las entregas N.º 1, 2, 3 y 4 se pidió un chequeo para mantener la continuidad entre entregas, la estructura en la presentacion, la ortografia y gramatica. A su vez se le pidió a la IA la realización del Diagrama BPMN a Imagen.
5. **Consolidación:** ordenar la versión final a partir de los documentos ya elaborados, sin agregar información nueva.

**Correcciones humanas efectuadas sobre los resultados de la IA:**

- Se verificó que la IA no cambiara la estructura y que la presentación del diagrama vaya de acuerdo con los archivos.
- Se detectó que el diccionario de datos subido estaba incompleto (le faltaba la tabla de relaciones) y se corrigió.
- Se creó y gestionó el repositorio, las ramas, los commits, los Pull Requests y el tablero de GitHub.
- Se siguió la indicación del tutor en el foro para documentar la autorevisión de cada Pull Request.
- Se incorporaron las observaciones del tutor: nombres del cuerpo docente, ubicación de la declaración de IA, campos calculados y dirección de entrega del diccionario de datos, y flujos de secuencia del diagrama BPMN.
El contenido fue revisado, ajustado y validado por el alumno, quien es responsable de su veracidad y coherencia conceptual.
