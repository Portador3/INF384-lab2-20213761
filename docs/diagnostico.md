1.1 Los cuatro defectos. Para cada uno: qué está mal, en qué archivo y en qué líneas se manifiesta, y qué consecuencia tiene. Un defecto no es "falta una línea": es qué garantía se pierde por no tenerla.
  1. Falta "needs: validar" en "publicar" (línea 43). Se pierde garantía del despliegue seguro y Quality Gate. El paquete puede ser publicado aunque fallen las pruebas.
  2. El reporte de pytest no se pasa a SonarCloud ni se espera una respuesta del Quality Gate (línea 39). Se pierde la garantía de la auditoría del código y su respuesta de automatización del flujo de CD.
  3. No se define caché (línea 21 y 51). Esto genera que en cada ejecución se realice una descarga.
  4. No se instala "build" y "pytest" de forma independiente (línea 56). El job "validar" no necesita la herramienta de empaquetado; y el job "publicar" no necesita la herramienta de test.

1.2 El defecto que explica la duración. De los cuatro, cuál explica el tiempo que
registraron en docs/linea-base.md. Sustenten con el número que midieron.
  El defecto 3 genera la demora. Los tiempos superan los 58s porque en cada ejecución se vuelve a descargar los paquetes por la ausencia de caché.

1.3 El vínculo con su caso. Cuál de los cuatro defectos ataca la restricción del caso transversal de su grupo. Citen un dato del value stream map que levantaron en la Sesión 1.
Caso TransPerú: La restricción del caso es que los lanzamientos a producción son menos frecuentes. Los defectos 1 y 2 atacan el problema. En este caso se decidió reducir la frecuencia de despliegues por el tiempo que les demoraba. Pero con la automatización corregida del CD se aborda el problema.

1.4 La métrica DORA. Qué métrica DORA esperan mover con la intervención y por qué. Solo dos son alcanzables sin despliegue: identifiquen cuáles y elijan una.
Lead time for changes: incluye la validación. Además, no involucra el despliegue.

1.5 El proxy. Qué número concreto van a medir para sustentar que la métrica se movió. Decláralo antes de intervenir.
Tiempo ahorrado: (Tiempo base - Tiempo nuevo) * 100 / (Tiempo original)

4.1 Medición posterior. El valor del proxy después de la intervención, junto al de la línea base. Qué cambió y en qué proporción.
1m 26s es luego de cambios. Antes era 1m 8s.
Proxy: -26.47%
El tiempo aumentó. Lo cuál podría significar un peor caso. Sin embargo, anteriormente no existía la espera de la validación de SonarCloud.

4.2 Justificación de la versión. Qué versión declararon y qué commits del historial la sustentan.
Versión 1.2.1. Fueron parches (correcciones):
  - 11d145a - Bump version from 1.2.0 to 1.2.1
  - 872c968 - Add pull request trigger to pipeline workflow
  - beaee87 - Fix typo in sonar.organization property
  - dd4f6b8 - Modify GitHub Actions pipeline for Python project
  - 590d3e4 - Update SonarQube project properties
  - 5a37f9a - Add diagnostic documentation for defect analysis
  - c8dce27 - "docs/linea-base.md"

4.3 Lo que no se resolvió. El pipeline sigue teniendo limitaciones. Nombren una y
expliquen qué haría falta para resolverla.
Los jobs de "validar" y "publicar" usan máquinas virtuales independientes. Lo que repite pasos de descarga. La solución sería construir un entorno en el primer job y compartirlo al segundo.

4.4 Declaración de uso de IA generativa, conforme al sílabo
Asistencia en el diagnóstico de errores sintácticos de GitHub Actions, depuración del error de ejecución de SonarScanner (código de salida 3), estructuración de comandos Git y generación de plantillas explicativas.
