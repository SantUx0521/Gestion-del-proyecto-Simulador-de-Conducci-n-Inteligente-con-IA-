**Estructura de Desglose del Trabajo (EDT)**

```
@startmindmap
top to bottom direction
* Simulador de conducción\n inteligente con IA (100%)
** 1. Telemetria y\n datos (10%)
*** 1.1. Registro de\n acciones y eventos (6%)
*** 1.2 Almacenamiento\n de registros (4%)

** 2. Visualización web\n en tiempo real (30%)
*** 2.1. Diseño interfaz \ngráfica (10%)
*** 2.2. Notificaciones \nmaniobras\n contradictorias (5%)
*** 2.3. Sincronización\n entre el mando y\n la web (10%)
*** 2.4. Notificación giros\n sin direccional (5%)

** 3. Seguimiento\n histórico desempeño\n del estudiante (10%)
*** 3.1. Acceso a\n reportes de errores\n por estudiante (2%)
*** 3.2. Acceso a\n recomendaciones\n de mejora (2%)
*** 3.3. Consulta por\n sesión y estudiante (6%) 

** 4. IA para detección\n de errores en la\n conducción (20%)
*** 4.1. Mapeo y modelo\n de detección de\n errores (8%)
*** 4.2. Registro de\n errores de\n conducción (6%)
*** 4.3. Registro de\n recomendaciones\n de mejora (6%)

** 5. Interacción\n física (20%)
*** 5.1. Montaje del \ncircuito (10%)
*** 5.2. Gestión de \nestados (3%)
*** 5.3. Comunicación \nwifi (4%)
*** 5.4. Pausa por\n pérdida de\n conexión (3%)

** 6. Gestión del proyecto (10%)
*** 6.1. Reuniones (2%)
*** 6.2. Documentación (3%)
*** 6.3. Seguimiento (2%)
*** 6.4. Pruebas finales y\n sustentación (3%)
@endmindmap

```

Visualizar el diagrama copiando el codigo aca:

<https://www.planttext.com/>

**Diccionario de la EDT**

| Código | Nombre | Descripción | Criterio de aceptación | Responsable | Esfuerzo estimado | Depende de | 
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | 
| 1.1 | Registro de acciones y eventos | Módulo encargado de capturar cada botón que se presiona en el mando y organizarlo con su hora y fecha exacta para saber qué hizo el alumno. | Al presionar alguno de los botones del control, el sistema genera un paquete de datos ordenado con la acción y el tiempo exacto sin perder información. | Santiago | 16h | 5.2 | 
| 1.2 | Almacenamiento de registros | Componente de base de datos y scripts de persistencia encargados de guardar los datos procesados de la sesión en el servidor. | La base de datos almacena y recupera el archivo JSON de telemetría completo asociado al ID de un estudiante y número de sesión, verificando la integridad mediante pruebas de lectura/escritura sin corrupción de datos. | Joan | 18h | 1.1 | 
| 2.1 | Diseño interfaz gráfica | Elementos visuales interactivos en HTML5/Canvas que representan el vehículo, la carretera y el entorno vial 2D. | La interfaz renderiza el vehículo en pantalla y responde visualmente (movimiento, aceleración, giros) en menos de 100 ms ante las señales recibidas desde la simulación. | Vanessa | 28h |  | 
| 2.2 | Notificaciones maniobras contradictorias | Componente de interfaz web encargado de desplegar alertas visuales inmediatas cuando el usuario ejecuta entradas incompatibles (freno y acelerador al tiempo). | Despliega un aviso flotante de alerta roja en el centro de la pantalla en menos de 100 ms al presionar simultáneamente Freno + Acelerador, y la remueve automáticamente al soltar cualquiera de los dos botones. | Alejandra | 14h | 2.1, 2.3 | 
| 2.3 | Sincronización entre el mando y la web | Conexión entre el control físico y la pantalla web para que el carro se mueva inmediatamente al presionar los botones. | Al presionar un botón en el mando físico, la animación correspondiente en la pantalla web responde en un tiempo máximo de 100 milisegundos, manteniendo esta velocidad de respuesta de forma fluida durante toda la prueba. | David | 24h | 5.3, 2.1 | 
| 2.4 | Notificación giros sin direccional | Muestra un aviso de infracción en pantalla si el usuario gira el vehículo sin haber puesto la direccional correspondiente un momento antes. | El sistema evalúa cuando el vehículo realiza un cambio de carril o giro; si la direccional del lado hacia donde se giró no estuvo encendida durante al menos 1 segundo previo a la maniobra, se muestra una alerta visual de infracción de forma inmediata y se suma una falta al contador de la clase. | Alejandra | 16h | 2.3, 2.1 | 
| 3.1 | Acceso a reportes de errores por estudiante | Pantalla donde el profesor puede seleccionar a un alumno y ver cuántas faltas cometió en total clasificadas por tipo. | El instructor elige un estudiante de la lista y la pantalla muestra un resumen claro con el número de frenadas bruscas, fallas de direccional y STOP. | Santiago | 14h | 4.2 | 
| 3.2 | Acceso a recomendaciones de mejora | Pantalla donde el estudiante o profesor leen los consejos automáticos para corregir los errores cometidos. | Muestra una lista legible con recomendaciones prácticas sobre lo que debe mejorar para la próxima clase, o un mensaje de felicitación si no tuvo errores. | Alejandra | 12h | 4.3 | 
| 3.3 | Consulta por sesión y estudiante | Buscador para filtrar las prácticas pasadas por fecha o por alumno y revisar qué pasó en una clase específica. | Se puede buscar una clase por la fecha o el nombre del alumno y al darle clic abre el resumen detallado de esa sesión en particular. | Joan | 18h | 1.2, 3.1 | 
| 4.1 | Mapeo y modelo de detección de errores | Definición y desarrollo del mecanismo/modelo inteligente encargado de clasificar y detectar anomalías en la telemetría (frenada brusca, pedalera simultánea, direccional omitida, colisión o ignorar STOP). | Al procesar los datos registrados de una clase completada, el módulo de IA identifica al menos el 96 % de los eventos anómalos y los clasifica con precisión en su categoría correspondiente sin generar falsos positivos críticos. | David | 25h | 1.1 | 
| 4.2 | Registro de errores de conducción | Función que guarda en la base de datos el conteo final de cuántas fallas cometió el alumno en esa práctica. | Guarda en la base de datos la lista final con el total de errores de la clase en menos de 2 segundos después de terminar la simulación. | Santiago | 20h | 4.1, 1.2 | 
| 4.3 | Registro de recomendaciones de mejora | Módulo que relaciona los errores cometidos con una lista de sugerencias para guardar los consejos adecuados en la base de datos. | Si el alumno cometió errores, el sistema guarda en la base de datos al menos un consejo útil por cada tipo de falta cometida en la sesión. | Alejandra | 20h | 4.1 | 
| 5.1 | Montaje del circuito | Armado físico del control conectando el ESP32 con los 6 botones en la protoboard usando los cables correspondientes. | Los 6 botones quedan firmes en la tabla de pruebas, no hacen falso contacto y envían energía al pin correcto del ESP32 al presionarlos. | Vanessa | 28h |  | 
| 5.2 | Gestión de estados | Programa en el ESP32 para leer bien los botones, evitar que se marquen dobles clics por falla del botón y entender combinaciones. | El mando responde limpio al presionar un botón y entiende cuando se presionan dos a la vez (como acelerar y girar) sin mandar señales erróneas. | Joan | 18h | 5.1 | 
| 5.3 | Comunicación wifi | Configuración en el ESP32 para conectarse al Wi-Fi e ir mandando la información de los botones a la aplicación web. | El ESP32 se conecta al Wi-Fi en unos segundos al prenderlo y empieza a mandar los datos de las teclas hacia la aplicación web de forma fluida. | Alejandra | 16h | 5.1 | 
| 5.4 | Pausa por pérdida de conexión | Sistema de seguridad que detecta si el Wi-Fi se cae para congelar la simulación sin perder lo que el alumno llevaba hecho. | Si se desconecta la red por más de 2 segundos, la pantalla se pausa sola, no deja seguir jugando y reanuda cuando regresa el internet sin borrar nada. | David | 14h | 5.3 | 
| 6.1 | Reuniones | Organización y registro de las sesiones semanales del grupo de trabajo y las citas con el profesor director. | Archivo con las notas de cada reunión realizada, donde se anota la fecha, quiénes asistieron y las tareas que le tocaron a cada uno. | Alejandra | 12h |  | 
| 6.2 | Documentación | Redacción de todos los documentos escritos que pide la materia (requisitos, historias de usuario, arquitectura y la EDT). | Documento final completo con toda la teoría y entregables del proyecto listo para entregar. | Santiago | 24h |  | 
| 6.3 | Seguimiento | Control semanal de los avances del grupo para ver qué tareas ya se terminaron y qué faltas o problemas hay. | Tablero de trabajo actualizado semana a semana mostrando qué tareas se hicieron, cuáles están en proceso y quién las está haciendo. | Alejandra | 14h |  | 
| 6.4 | Pruebas finales y sustentación | Ejecución de pruebas funcionales de integración extremo a extremo (Hardware–Web–IA), preparación de diapositivas y ensayo de sustentación final. | Plan de pruebas completado con éxito validando la comunicación integrada del prototipo, diapositivas listas y ensayo general previo a la fecha de entrega. | Todos | 20h | Todos | 
