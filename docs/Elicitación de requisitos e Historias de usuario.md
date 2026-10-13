# Elicitación de requisitos e Historias de usuario

## 

 ## 1. Identificación de Stakeholders

| Stakeholder | Rol | Lo que puede aportar |
| ----- | :---: | :---: |
| Director de la escuela de conducción | Patrocinador/Decisor | Visión del negocio, presupuesto, decisiones  |
| Instructor de conducción | Usuario experto | Conocimiento sobre errores frecuentes, prácticas de conducción y criterios para evaluar al estudiante |
| Estudiante de conducción | Usuario final | Experiencia de uso, dificultades al practicar y percepción de la retroalimentación  |
| Administradores de la escuela de conducción | Usuario interno | Cómo se gestionan actualmente las prácticas, sesiones y seguimiento de estudiantes  |
| Equipo de desarrollo | Equipo técnico | Desarrollo del ESP32, página web, almacenamiento de datos e integración con IA  |
| Gerente del proyecto | Gestión del proyecto | Organización, seguimiento del proyecto, recursos, tiempos y decisiones  |
| Usuarios de prueba | Usuario de prueba | Opiniones sobre facilidad de uso, funcionamiento y experiencia con el simulador  |
| Docente director del proyecto | Asesor / supervisor  | Orientación académica, revisión del proyecto y cumplimiento de objetivo  |

 ## 2. Definición roles de equipo

| Rol | Persona | Responsabilidad principal en este proyecto |
| :---: | :---: | :---: |
| Project Manager | Santiago | Entrevistas, acta, cronograma |
| Product Owner | Joan | Backlog, priorización, aceptación |
| Scrum Master | Alejandra | Facilitar ceremonias, eliminar impedimentos |
| Development Team | Todos | Estimar, desarrollar, probar |

 ## 3. Preparación guía de entrevista

Escribe una guía de entrevista para el stakeholder principal de tu proyecto. Incluye al menos:

* 2 preguntas sobre el proceso actual (cómo funciona HOY)  
  En las prácticas de conducción actuales ¿De qué manera el instructor registra las correcciones del estudiante?  
  R/ En la práctica no se registra nada en el momento. El proceso es puramente observacional, el instructor va al lado del estudiante, le da indicaciones verbales y le corrige los errores sobre la marcha. No se lleva ningún tipo de control escrito o digital de las maniobras específicas que falla el alumno durante la sesión.  
  ¿Existe algún método o formato para conservar el historial de desempeño de un alumno a lo largo de las sesiones?  
  R/ No. Lo único que se registra en el sistema de la escuela es la asistencia del alumno y las horas completadas para el RUNT. La evolución del manejo depende únicamente de la memoria del instructor que le toque en esa clase, por lo que no hay un historial técnico para medir su avance real entre sesión y sesión.  
* 2 preguntas sobre los puntos de dolor (qué problemas tiene HOY)  
  ¿Qué errores de conducción son más difíciles de evaluar de forma objetiva durante una práctica tradicional?   
  R/ La coordinación de los pedales y la brusquedad en maniobras. Determinar a ojo si un frenado fue demasiado brusco o si el alumno aceleró a destiempo en un alto es muy subjetivo y depende de la apreciación de cada instructor.  
  Al final de una práctica ¿Qué dificultades enfrentan los instructores o estudiantes para justificar o comprender las fallas cometidas?  
  R/ La falta de evidencia. Al no haber telemetría ni datos grabados, la retroalimentación al final de la clase se vuelve una discusión subjetiva, porque el estudiante no recuerda exactamente qué hizo o siente que el instructor exageró.  
* 2 preguntas sobre la visión (qué espera que cambie)  
  ¿De qué forma espera que la visualización en tiempo real mediante una interfaz web cambie la dinámica de aprendizaje del estudiante?  
  R/ Ayudará a la memoria muscular. Ver reflejada en pantalla la reacción inmediata del vehículo al presionar los botones del control hace que el alumno entienda rápido la relación causa-efecto antes de subirse al carro real.   
  ¿Qué tipo de métricas generadas al final de la sesión considera prioritarias para que el reporte sea útil y significativo?  
  R/ Un conteo de faltas por categoría (frenadas bruscas, marchas incorrectas, no parar en un STOP) y un resumen con recomendaciones puntuales sobre lo que debe corregir para la siguiente clase.  
* 2 preguntas sobre casos bordes (¿qué pasa cuando...?)  
  ¿Qué debería hacer el sistema si durante una simulación ocurre una secuencia inusual o contradictoria de entradas? ¿Cómo presionar el acelerador y freno a la vez?  
  R/ Debe marcarlo como una falta directa de conducción, restar puntos en el desempeño y mostrar una alerta en la pantalla indicando que es una maniobra inválida, sin colapsar el sistema.  
  ¿Cómo debería comportarse la simulación si la conexión wifi entre el esp32 y la aplicación web se interrumpe durante la práctica?  
  R/ Debe pausar la simulación inmediatamente y notificar la pérdida de señal en la web, reteniendo los datos acumulados hasta que se restablezca el enlace sin perder la sesión.  
* 1 pregunta de cierre (¿qué no te pregunté?)  
  ¿Hay alguna regla de tránsito o aspecto clave para el proyecto que no hayamos mencionado y que consideres indispensable incluir en este proyecto?  
  R/ El uso anticipado de las direccionales antes de realizar un giro o cambio de carril. En la práctica real muchos estudiantes olvidan señalizar la maniobra antes de accionar el volante, y sería clave que el simulador valide que se active la direccional antes de registrar el giro.

 ## 4. Conducción de la entrevista y escritura del acta

```
ACTA DE ELICITACIÓN
Proyecto: Simulador de Conducción Inteligente con IA
Entrevistado: Jose David Marmol
Fecha: 2/10/2026

PUNTOS DE DOLOR ACTUALES:
- Proceso de evaluación 100% observacional y subjetivo, sin registro técnico de maniobras ni errores específicos durante la clase.
- Falta de historial de desempeño; solo se registra la asistencia para el RUNT, dejando el seguimiento del avance a la memoria del instructor.

- Dificultad para evaluar objetivamente la brusquedad en frenadas/aceleraciones y la coordinación de pedales.
- Retroalimentación compleja al final de la sesión por falta de evidencia gráfica o telemetría para respaldar las correcciones.

VISIÓN DEL NEGOCIO:
- Digitalización y objetivación de las prácticas iniciales mediante el prototipo de control físico y la simulación web.
- Desarrollo de memoria muscular y comprensión rápida de la relación causa-efecto en el estudiante antes de pasar al vehículo real.
- Generación de reportes automáticos con métricas claras (conteo de faltas por categoría y recomendaciones) para guiar las siguientes clases.

ACTORES IDENTIFICADOS:
- Estudiante de conducción (usuario del simulador).
- Instructor de conducción (evaluador de las métricas y fallas).
- Director / Administrador de la escuela de conducción (gestor del avance y las sesiones).

RESTRICCIONES EXPLÍCITAS:
- El sistema solo evaluará las acciones capturadas por el control físico de 6 botones (sin vehículo real ni sensores externos).
- Sin procesamiento visual por cámaras ni gráficos 3D avanzados; la simulación será una interfaz web funcional.
- Las sesiones dependen de una conexión estable a internet/Wi-Fi entre el hardware y la web; ante caídas de red, la simulación debe pausarse sin perder datos.

REQUISITOS LATENTES DESCUBIERTOS:
- Manejo de entradas contradictorias (ej. presionar freno y acelerador al tiempo) penalizando la falta y mostrando alerta en pantalla sin bloquear el sistema.
- Validación del uso obligatorio y anticipado de direccionales antes de registrar una maniobra de giro o cambio de carril.
- Pausa automática y retención de estado ante interrupciones de señal Wi-Fi.
```

 ## 5. Historias de usuario y criterios de aceptación

**HU-01: Interacción mediante control físico**

Como estudiante de conducción, quiero ejecutar acciones básicas de manejo (acelerar, frenar, girar y cambiar marchas) mediante los botones del mando físico con ESP32, para familiarizarme con los mandos y desarrollar memoria muscular previa a la práctica en un vehículo real.

**Criterio 1 \- Interacción con el mando**  
Dado que el estudiante quiere practicar las acciones básicas de manejo en un mando físico  
Cuando presiona en el botón correspondiente de una acción determinada (acelerar, frenar, girar, subir/bajar marcha)  
Entonces el sistema debe enviar la señal correspondiente correctamente

**Criterio 2 \- Ausencia de interacción**  
Dado que el estudiante no ejecuta ninguna acción  
Cuando se está realizando una práctica de manejo  
Entonces el sistema no envía ninguna señal

**Criterio 3 \- Acciones simultáneas válidas**  
Dado que el estudiante está realizando una práctica de manejo  
Cuando presiona dos botones compatibles al mismo tiempo (por ejemplo, acelerar y girar)  
Entonces el sistema debe enviar ambas señales correctamente y sin pérdida de ninguna de ellas

**HU-02: Visualización de la simulación en tiempo real**

Como estudiante de conducción, quiero observar en la interfaz web una animación que responda de forma inmediata a las acciones que presiono en el control físico, para comprender la relación causa-efecto de mis maniobras sobre el vehículo durante el recorrido.

**Criterio 1 \- causa-efecto acción**  
Dado que el estudiante ha presionado una acción mediante el mando  
Cuando se envíe la señal al sistema  
Entonces se debe observar inmediatamente en la interfaz web la animación que corresponda la acción ejecutada.

**Criterio 2 \- Ausencia de animación**  
Dado que el estudiante no ha presionado ninguna acción  
Cuando se observa en la interfaz  
Entonces no debería visualizarse la animación

**Criterio 3 \- Sincronización de la animación con el mando**  
Dado que el estudiante deja de presionar un botón del mando  
Cuando el sistema deja de recibir la señal de esa acción  
Entonces la animación correspondiente debe detenerse de inmediato en la interfaz web

**HU-03: Notificación de maniobras contradictorias**

Como estudiante de conducción, quiero recibir una alerta visual inmediata en pantalla si ejecuto entradas simultáneas inválidas (como acelerar y frenar al mismo tiempo), para reconocer el error al instante y corregir malos hábitos de coordinación de pedales.

**Criterio 1 \- Alerta por entradas contradictorias**  
Dado que el estudiante está realizando una práctica de manejo  
Cuando presiona simultáneamente acelerar y frenar  
Entonces el sistema debe mostrar de inmediato una alerta visual en pantalla indicando la maniobra inválida

**Criterio 2 \- Ausencia de alerta en maniobras válidas**  
Dado que el estudiante ejecuta acciones individuales o combinaciones compatibles  
Cuando el sistema procesa las señales recibidas  
Entonces no debe mostrarse ninguna alerta de maniobra contradictoria

**Criterio 3 \- Desaparición de la alerta**  
Dado que se está mostrando una alerta de maniobra contradictoria  
Cuando el estudiante suelta uno de los botones en conflicto  
Entonces la alerta debe desaparecer de la pantalla

**HU-04: Validación del uso de direccionales**

Como estudiante de conducción, quiero que el simulador valide la activación previa de la direccional antes de ejecutar un giro o cambio de carril, para reforzar el hábito de señalización reglamentaria antes de maniobrar.

**Criterio 1 \- Giro con direccional previa**  
Dado que el estudiante activó la direccional correspondiente antes de maniobrar  
Cuando ejecuta un giro o cambio de carril hacia ese lado  
Entonces el sistema debe validar la maniobra como correcta y no registrar ninguna falta

**Criterio 2 \- Giro sin direccional**  
Dado que el estudiante no activó la direccional antes de maniobrar  
Cuando ejecuta un giro o cambio de carril  
Entonces el sistema debe notificar la omisión y registrarla como una infracción de señalización

**Criterio 3 \- Direccional incorrecta**  
Dado que el estudiante activó la direccional de un lado  
Cuando ejecuta un giro o cambio de carril hacia el lado contrario  
Entonces el sistema debe notificar la inconsistencia y registrarla como una infracción de señalización

**HU-05: Pausa automática por pérdida de conexión**

Como estudiante de conducción, quiero que el sistema pause automáticamente la simulación y conserve los datos acumulados si se interrumpe la conexión Wi-Fi con el ESP32, para no perder el progreso de mi sesión ni registrar datos erróneos por falta de comunicación.

**Criterio 1 \- Pausa por desconexión**  
Dado que la simulación está en curso  
Cuando se interrumpe la conexión Wi-Fi entre el ESP32 y el sistema  
Entonces el sistema debe pausar automáticamente la simulación e informar al estudiante de la desconexión

**Criterio 2 \- Conservación de datos**  
Dado que la simulación fue pausada por pérdida de conexión  
Cuando el sistema se encuentra en estado de pausa  
Entonces los datos acumulados de la sesión deben conservarse sin modificaciones y no debe registrarse ninguna acción

**Criterio 3 \- Reanudación al reconectar**  
Dado que la simulación está pausada por pérdida de conexión  
Cuando se restablece la conexión con el ESP32  
Entonces el sistema debe permitir al estudiante reanudar la sesión desde el punto exacto donde se interrumpió

**HU-06: Registro y almacenamiento de telemetría de la sesión**

Como instructor de conducción, quiero que el sistema registre y guarde de manera estructurada todas las acciones, tiempos y eventos ocurridos durante cada sesión, para contar con un respaldo objetivo y técnico del desempeño del alumno durante la práctica.

**Criterio 1 \- Registro de acciones y eventos**  
Dado que el estudiante realiza una práctica de manejo  
Cuando ejecuta una acción o se produce un evento en la simulación  
Entonces el sistema debe registrar la acción o evento junto con su marca de tiempo

**Criterio 2 \- Almacenamiento al finalizar la sesión**  
Dado que la sesión de práctica ha finalizado  
Cuando el sistema cierra la simulación  
Entonces todos los datos registrados deben guardarse de forma estructurada y asociarse al estudiante y a la sesión correspondiente

**Criterio 3 \- Sesión sin actividad**  
Dado que el estudiante inicia una sesión pero no ejecuta ninguna acción  
Cuando la sesión finaliza  
Entonces el sistema debe guardar la sesión indicando que no hubo acciones registradas

**HU-07: Analisis inteligente de errores de conducción**

Como instructor de conducción, quiero que un módulo de IA identifique y categorice automáticamente infracciones y fallas técnicas (como frenadas bruscas, marchas incorrectas, colisiones e incumplimiento de señales de STOP), para eliminar la subjetividad en la evaluación de maniobras complejas.

**Criterio 1 \- Detección y categorización de errores**  
Dado que la sesión de práctica ha finalizado y cuenta con datos de telemetría  
Cuando el módulo de IA analiza la sesión  
Entonces debe identificar y categorizar cada error ocurrido (frenada brusca, marcha incorrecta, colisión o incumplimiento de señal de STOP)

**Criterio 2 \- Sesión sin errores**  
Dado que el estudiante realizó una sesión sin cometer infracciones ni fallas técnicas  
Cuando el módulo de IA analiza la sesión  
Entonces no debe registrar ningún error y debe indicar que la sesión fue completada sin infracciones

**Criterio 3 \- Trazabilidad del error**  
Dado que el módulo de IA detectó un error en la sesión  
Cuando el instructor consulta el detalle de ese error  
Entonces el sistema debe mostrar la categoría, el momento en que ocurrió y la acción que lo originó

**HU-08: Reporte final de desempeño y recomendaciones**

Como estudiante de conducción, quiero consultar al finalizar la simulación un resumen con el conteo de errores por categoría y recomendaciones automáticas de mejora, para entender con claridad qué aspectos debo corregir en mi siguiente sesión.

**Criterio 1 \- Resumen de errores por categoría**  
Dado que la simulación ha finalizado y fue analizada  
Cuando el estudiante consulta el reporte final  
Entonces el sistema debe mostrar el conteo de errores por cada categoría

**Criterio 2 \- Recomendaciones de mejora**  
Dado que el reporte final registra al menos un error  
Cuando el estudiante consulta el reporte  
Entonces el sistema debe mostrar recomendaciones automáticas de mejora asociadas a las categorías de error cometidas

**Criterio 3 \- Reporte sin errores**  
Dado que la sesión finalizó sin errores registrados  
Cuando el estudiante consulta el reporte final  
Entonces el sistema debe mostrar el conteo en cero para todas las categorías y un mensaje de felicitación en lugar de recomendaciones correctivas

**HU-09: Consulta de historial de desempeño por estudiante**

Como instructor de conducción, quiero acceder al historial de las prácticas anteriores de cada estudiante, para hacer seguimiento a su evolución técnica y planificar las correcciones pedagógicas pertinentes.

**Criterio 1 \- Consulta del historial**  
Dado que el instructor accede al módulo de historial  
Cuando selecciona a un estudiante  
Entonces el sistema debe mostrar la lista de sus prácticas anteriores con fecha y resumen de errores

**Criterio 2 \- Estudiante sin prácticas**  
Dado que el estudiante seleccionado aún no ha realizado ninguna práctica  
Cuando el instructor consulta su historial  
Entonces el sistema debe mostrar un mensaje indicando que no existen sesiones registradas

**Criterio 3 \- Detalle de una sesión anterior**  
Dado que el instructor visualiza el historial de un estudiante  
Cuando selecciona una práctica específica  
Entonces el sistema debe mostrar el reporte detallado de esa sesión, incluyendo errores por categoría y recomendaciones

6. ## Product Backlog priorizado 

Estructura Jerárquica del Backlog:

```
-- ÉPICA 01: Captura de Telemetría e Interacción Física (Hardware & IoT)
   │
   ├── HU-01: Interacción mediante control físico (ESP32 y 6 botones)
   │     └── Tarea técnica: Montaje de circuito con ESP32 y 6 botones físicos
   │     └── Tarea técnica: Firmware en C++ para debounce de botones y gestión de estados
   │     └── Tarea técnica: Implementación de comunicación Wi-Fi / WebSockets desde el ESP32
   │
   └── HU-05: Pausa automática por pérdida de conexión
         └── Tarea técnica: Protocolo de Heartbeat para detectar pérdida de señal Wi-Fi
         └── Tarea técnica: Lógica de retención de estado en frontend y congelamiento de tiempo

-- ÉPICA 02: Simulación y Visualización Web en Tiempo Real
   │
   ├── HU-02: Visualización de la simulación en tiempo real
   │     └── Tarea técnica: Diseño de la interfaz gráfica del vehículo y carril en HTML5/Canvas
   │     └── Tarea técnica: Cliente WebSocket en JS para recepción de eventos sin latencia
   │
   ├── HU-03: Notificación de maniobras contradictorias
   │     └── Tarea técnica: Algoritmo de validación de entradas simultáneas inválidas (Acelerador + Freno)
   │     └── Tarea técnica: Componente UI de alerta visual e interrupción momentánea
   │
   └── HU-04: Validación del uso de direccionales
         └── Tarea técnica: Lógica temporizada para validar activación previa de direccional antes del giro
         └── Tarea técnica: Detección de giros sin direccional o direccional opuesta

-- ÉPICA 03: Motor de Análisis de IA y Reportes de Desempeño
   │
   ├── HU-06: Registro y almacenamiento de telemetría de la sesión
   │     └── Tarea técnica: Estructuración de datos JSON de telemetría con marcas de tiempo
   │     └── Tarea técnica: Esquema de base de datos y endpoints para guardar sesiones
   │
   ├── HU-07: Análisis inteligente de errores de conducción (IA)
   │     └── Tarea técnica: Modelo/módulo de reglas e IA para detección de infracciones complejas
   │     └── Tarea técnica: Mapeo de categorías de error (frenadas bruscas, STOP, cambios de marcha)
   │
   └── HU-08: Reporte final de desempeño y recomendaciones
         └── Tarea técnica: Vista UI de resumen con gráficos/contadores de faltas por categoría
         └── Tarea técnica: Motor de generación automática de sugerencias pedagógicas

-- ÉPICA 04: Gestión Administrativa y Seguimiento Histórico
   │
   └── HU-09: Consulta de historial de desempeño por estudiante
         └── Tarea técnica: Módulo de búsqueda y filtrado de estudiantes para instructores
         └── Tarea técnica: Vista detallada del historial de sesiones y evolución del alumno
```

## Tabla del Product Backlog Priorizado:

| ID | Historia de Usuario | Prioridad | Justificación de Negocio / Técnica |
| :---- | :---- | :---- | :---- |
| **HU-01** | Interacción mediante control físico | **Must Have** | Sin captura de entradas desde el ESP32 no hay simulación ni datos que procesar. Core del producto. |
| **HU-02** | Visualización de la simulación en tiempo real | **Must Have** | Permite al estudiante ver el efecto directo e inmediato de sus maniobras en pantalla. |
| **HU-06** | Registro y almacenamiento de telemetría | **Must Have** | La base de datos guardada es el insumo indispensable para alimentar el módulo de análisis de IA. |
| **HU-07** | Análisis inteligente de errores de conducción | **Must Have** | Cumple con el objetivo diferenciador del proyecto: evaluación objetiva de fallas mediante IA. |
| **HU-08** | Reporte final de desempeño y recomendaciones | **Must Have** | Entregable directo para que el estudiante comprenda sus errores y aplique correcciones. |
| **HU-03** | Notificación de maniobras contradictorias | **Should Have** | Corrección inmediata de vicios de manejo (pedales simultáneos); alto valor pedagógico. |
| **HU-04** | Validación del uso de direccionales | **Should Have** | Requisito clave descubierto en la elicitación para evaluar hábitos de señalización vial. |
| **HU-05** | Pausa automática por pérdida de conexión | **Should Have** | Protege la integridad de la prueba y evita que se guarden datos erróneos por caídas de red. |
| **HU-09** | Consulta de historial de desempeño por estudiante | **Should Have** | Permite al instructor medir la evolución técnica del alumno entre clase y clase. |
| **—** | Visualización gráfica con escenarios 3D avanzados | **Won't Have** | Excluido explícitamente en el Alcance del Proyecto para acotar la complejidad. |
| **—** | Evaluación o certificación oficial para el RUNT | **Won't Have** | Fuera del alcance académico; el sistema no sustituye la homologación legal. |
| **—** | Aplicación móvil nativa | **Won't Have** | Se usará exclusivamente una interfaz web para acortar tiempos de desarrollo. |

