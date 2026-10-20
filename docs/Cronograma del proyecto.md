# Cronograma y ruta crítica

# 1. De paquete de trabajo a tarea

| Código | Nombre | Esfuerzo | Duración |
| :---- | :---- | :---- | :---- |
| 1.1 | Registro de acciones y eventos | 16h | 8 días |
| 1.2 | Almacenamiento de registros | 18h | 9 días |
| 2.1 | Diseño interfaz gráfica | 28h | 14 días |
| 2.2 | Notificaciones maniobras contradictorias  | 14 h | 6 días |
| 2.3 | Sincronización entre el mando y la web  | 24h | 12 días |
| 2.4 | Notificación giros sin direccional  | 16h | 8 días |
| 3.1 | Acceso a reportes de errores por estudiante   | 14h | 6 días |
| 3.2 | Acceso a recomendaciones de mejora  | 12h | 5 dias |
| 3.3 | Consulta por sesión y estudiante  | 18h | 8 días |
| 4.1 | Mapeo de categorías de error  | 25h | 14 días |
| 4.2 | Registro de errores de conducción | 20h | 10 días |
| 4.3 | Registro de recomendaciones de mejora  | 20h | 10 días |
| 5.1 | Montaje del circuito | 28h | 14 días |
| 5.2 | Gestión de estados  | 18h | 9 días |
| 5.3 | Comunicación wifi | 16h | 8 días |
| 5.4 | Pausa por pérdida de conexión  | 14h | 7 días |
| 6.1 | Reuniones | 12h | 6 días |
| 6.2 | Documentación  | 24h | 12 días |
| 6.3 | Seguimiento  | 14h | 7 días |
| 6.4 | Sustentación | 20h | 4 días |

# 2. Las dependencias

```
@startuml
left to right direction
skinparam shadowing false
skinparam defaultFontSize 11
skinparam rectangle {
  BackgroundColor #1f2a3a
  BorderColor #5aa0ff
  FontColor white
  RoundCorner 10
}
skinparam rectangle<<crit>> {
  BackgroundColor #4a2a2e
  BorderColor #ff6b6b
}
skinparam ArrowColor #888888

title Diagrama de red – Dependencias ajustadas (EDT)\nRuta crítica en rojo: 73 días

rectangle "Inicio" as INI

rectangle "**5.1** Montaje del circuito\n14 días" as T51 <<crit>>
rectangle "**5.2** Gestión de estados\n9 días" as T52 <<crit>>
rectangle "**5.3** Comunicación wifi\n8 días" as T53
rectangle "**5.4** Pausa por pérdida\nde conexión\n7 días" as T54
rectangle "**1.1** Registro de acciones\ny eventos\n8 días" as T11 <<crit>>
rectangle "**1.2** Almacenamiento\nde registros\n9 días" as T12
rectangle "**2.1** Diseño interfaz gráfica\n14 días" as T21
rectangle "**2.2** Notif. maniobras\ncontradictorias\n6 días" as T22
rectangle "**2.3** Sincronización\nmando - web\n12 días" as T23
rectangle "**2.4** Notif. giros sin\ndireccional\n8 días" as T24
rectangle "**4.1** Mapeo y modelo de\ndetección de errores\n14 días" as T41 <<crit>>
rectangle "**4.2** Registro de errores\nde conducción\n10 días" as T42 <<crit>>
rectangle "**4.3** Registro de\nrecomendaciones\n10 días" as T43
rectangle "**3.1** Reportes de errores\npor estudiante\n6 días" as T31 <<crit>>
rectangle "**3.2** Recomendaciones\nde mejora\n5 días" as T32
rectangle "**3.3** Consulta por sesión\ny estudiante\n8 días" as T33 <<crit>>
rectangle "**6.1** Reuniones\n6 días" as T61
rectangle "**6.2** Documentación\n12 días" as T62
rectangle "**6.3** Seguimiento\n7 días" as T63
rectangle "**6.4** Pruebas finales y\nsustentación\n4 días" as T64 <<crit>>

' Tareas sin predecesora
INI -[#ff6b6b,thickness=2]-> T51
INI --> T21
INI --> T61
INI --> T62
INI --> T63

' Paquete 5
T51 -[#ff6b6b,thickness=2]-> T52
T51 --> T53
T53 --> T54

' 5.2 habilita 1.1
T52 -[#ff6b6b,thickness=2]-> T11

' Paquetes 1 y 4
T11 --> T12
T11 -[#ff6b6b,thickness=2]-> T41
T12 --> T42
T41 -[#ff6b6b,thickness=2]-> T42
T41 --> T43

' Paquete 2
T21 --> T23
T53 --> T23
T21 --> T22
T23 --> T22
T21 --> T24
T23 --> T24

' Paquete 3
T42 -[#ff6b6b,thickness=2]-> T31
T43 --> T32
T12 --> T33
T31 -[#ff6b6b,thickness=2]-> T33

' Cierre (6.4 depende de todos)
T22 --> T64
T24 --> T64
T54 --> T64
T32 --> T64
T61 --> T64
T62 --> T64
T63 --> T64
T33 -[#ff6b6b,thickness=2]-> T64

legend bottom
  **Ruta crítica:** 5.1 → 5.2 → 1.1 → 4.1 → 4.2 → 3.1 → 3.3 → 6.4
  14 + 9 + 8 + 14 + 10 + 6 + 8 + 4 = **73 días**
endlegend
@enduml
```

# 3. El recorrido hacia adelante

| Tarea | Duración | Predecesoras | ES | EF |
| ----- | ----- | ----- | ----- | ----- |
| 5.1 Montaje del circuito | 14 | — | 0 | 14 |
| 5.2 Gestión de estados | 9 | 5.1 | 14 | 23 |
| 5.3 Comunicación wifi | 8 | 5.1 | 14 | 22 |
| 5.4 Pausa por pérdida de conexión | 7 | 5.3 | 22 | 29 |
| 1.1 Registro de acciones y eventos | 8 | 5.2 | 23 | 31 |
| 1.2 Almacenamiento de registros | 9 | 1.1 | 31 | 40 |
| 2.1 Diseño interfaz gráfica | 14 | — | 0 | 14 |
| 2.3 Sincronización mando-web | 12 | 2.1, 5.3 | 22 | 34 |
| 2.2 Notif. maniobras contradictorias | 6 | 2.1, 2.3 | 34 | 40 |
| 2.4 Notif. giros sin direccional | 8 | 2.1, 2.3 | 34 | 42 |
| 4.1 Mapeo y modelo de errores | 14 | 1.1 | 31 | 45 |
| 4.2 Registro de errores de conducción | 10 | 4.1, 1.2 | 45 | 55 |
| 4.3 Registro de recomendaciones | 10 | 4.1 | 45 | 55 |
| 3.1 Reportes de errores por estudiante | 6 | 4.2 | 55 | 61 |
| 3.2 Recomendaciones de mejora | 5 | 4.3 | 55 | 60 |
| 3.3 Consulta por sesión y estudiante | 8 | 1.2, 3.1 | 61 | 69 |
| 6.1 Reuniones | 6 | — | 0 | 6 |
| 6.2 Documentación | 12 | — | 0 | 12 |
| 6.3 Seguimiento | 7 | — | 0 | 7 |
| 6.4 Pruebas finales y sustentación | 4 | Todas | 69 | 73 |

El proyecto dura 73 dias

# 4. El recorrido hacia atrás y la holgura

Cálculo del fin más tardío ($LF$), inicio más tardío ($LS$) y holgura ($H = LS - ES$) recorriendo la red desde el día 73:

| Código | Tarea | Duración | ES | EF | LS | LF | Holgura | ¿Ruta Crítica? |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **5.1** | Montaje del circuito | 14 | 0 | 14 | 0 | 14 | **0** | **SÍ** |
| **5.2** | Gestión de estados | 9 | 14 | 23 | 14 | 23 | **0** | **SÍ** |
| **5.3** | Comunicación wifi | 8 | 14 | 22 | 29 | 37 | **15** | NO |
| **5.4** | Pausa por pérdida de conexión | 7 | 22 | 29 | 62 | 69 | **40** | NO |
| **1.1** | Registro de acciones y eventos | 8 | 23 | 31 | 23 | 31 | **0** | **SÍ** |
| **1.2** | Almacenamiento de registros | 9 | 31 | 40 | 36 | 45 | **5** | NO |
| **2.1** | Diseño interfaz gráfica | 14 | 0 | 14 | 23 | 37 | **23** | NO |
| **2.3** | Sincronización mando-web | 12 | 22 | 34 | 37 | 49 | **15** | NO |
| **2.2** | Notif. maniobras contradictorias | 6 | 34 | 40 | 63 | 69 | **29** | NO |
| **2.4** | Notif. giros sin direccional | 8 | 34 | 42 | 61 | 69 | **27** | NO |
| **4.1** | Mapeo y modelo de errores | 14 | 31 | 45 | 31 | 45 | **0** | **SÍ** |
| **4.2** | Registro de errores de conducción | 10 | 45 | 55 | 45 | 55 | **0** | **SÍ** |
| **4.3** | Registro de recomendaciones | 10 | 45 | 55 | 54 | 64 | **9** | NO |
| **3.1** | Reportes de errores por estudiante | 6 | 55 | 61 | 55 | 61 | **0** | **SÍ** |
| **3.2** | Recomendaciones de mejora | 5 | 55 | 60 | 64 | 69 | **9** | NO |
| **3.3** | Consulta por sesión y estudiante | 8 | 61 | 69 | 61 | 69 | **0** | **SÍ** |
| **6.1** | Reuniones | 6 | 0 | 6 | 63 | 69 | **63** | NO |
| **6.2** | Documentación | 12 | 0 | 12 | 57 | 69 | **57** | NO |
| **6.3** | Seguimiento | 7 | 0 | 7 | 62 | 69 | **62** | NO |
| **6.4** | Pruebas finales y sustentación | 4 | 69 | 73 | 69 | 73 | **0** | **SÍ** |

---

### Conclusión de holguras
Las tareas con **holgura cero** (**5.1 → 5.2 → 1.1 → 4.1 → 4.2 → 3.1 → 3.3 → 6.4**) pertenecen a la ruta crítica; cualquier retraso en ellas pospondrá la entrega final de 73 días.

# 5. La ruta crítica

```
@startuml
left to right direction
skinparam shadowing false
skinparam defaultFontSize 10
skinparam ArrowColor #888888
skinparam linetype ortho

skinparam rectangle {
  BackgroundColor #1f2a3a
  BorderColor #5aa0ff
  FontColor white
  RoundCorner 8
}

skinparam rectangle<<crit>> {
  BackgroundColor #4a2a2e
  BorderColor #ff6b6b
}

title Diagrama de red – Dependencias ajustadas (EDT)\nRuta crítica en rojo: 73 días

rectangle "Inicio" as INI

rectangle "5.1 Montaje del circuito\nES | Dur | EF\n0 | 14 | 14\nLS | Holg | LF\n0 | 0 | 14" as T51 <<crit>>

rectangle "5.2 Gestión de estados\nES | Dur | EF\n14 | 9 | 23\nLS | Holg | LF\n14 | 0 | 23" as T52 <<crit>>

rectangle "5.3 Comunicación wifi\nES | Dur | EF\n14 | 8 | 22\nLS | Holg | LF\n29 | 15 | 37" as T53

rectangle "5.4 Pausa por pérdida de conexión\nES | Dur | EF\n22 | 7 | 29\nLS | Holg | LF\n62 | 40 | 69" as T54

rectangle "1.1 Registro de acciones y eventos\nES | Dur | EF\n23 | 8 | 31\nLS | Holg | LF\n23 | 0 | 31" as T11 <<crit>>

rectangle "1.2 Almacenamiento de registros\nES | Dur | EF\n31 | 9 | 40\nLS | Holg | LF\n36 | 5 | 45" as T12

rectangle "2.1 Diseño de interfaz gráfica\nES | Dur | EF\n0 | 14 | 14\nLS | Holg | LF\n23 | 23 | 37" as T21

rectangle "2.2 Notificaciones de maniobras contradictorias\nES | Dur | EF\n34 | 6 | 40\nLS | Holg | LF\n63 | 29 | 69" as T22

rectangle "2.3 Sincronización mando-web\nES | Dur | EF\n22 | 12 | 34\nLS | Holg | LF\n37 | 15 | 49" as T23

rectangle "2.4 Notificación de giros sin direccional\nES | Dur | EF\n34 | 8 | 42\nLS | Holg | LF\n61 | 27 | 69" as T24

rectangle "4.1 Mapeo y modelo de errores\nES | Dur | EF\n31 | 14 | 45\nLS | Holg | LF\n31 | 0 | 45" as T41 <<crit>>

rectangle "4.2 Registro de errores de conducción\nES | Dur | EF\n45 | 10 | 55\nLS | Holg | LF\n45 | 0 | 55" as T42 <<crit>>

rectangle "4.3 Registro de recomendaciones\nES | Dur | EF\n45 | 10 | 55\nLS | Holg | LF\n54 | 9 | 64" as T43

rectangle "3.1 Reportes de errores por estudiante\nES | Dur | EF\n55 | 6 | 61\nLS | Holg | LF\n55 | 0 | 61" as T31 <<crit>>

rectangle "3.2 Recomendaciones de mejora\nES | Dur | EF\n55 | 5 | 60\nLS | Holg | LF\n64 | 9 | 69" as T32

rectangle "3.3 Consulta por sesión y estudiante\nES | Dur | EF\n61 | 8 | 69\nLS | Holg | LF\n61 | 0 | 69" as T33 <<crit>>

rectangle "6.1 Reuniones\nES | Dur | EF\n0 | 6 | 6\nLS | Holg | LF\n63 | 63 | 69" as T61

rectangle "6.2 Documentación\nES | Dur | EF\n0 | 12 | 12\nLS | Holg | LF\n57 | 57 | 69" as T62

rectangle "6.3 Seguimiento\nES | Dur | EF\n0 | 7 | 7\nLS | Holg | LF\n62 | 62 | 69" as T63

rectangle "6.4 Pruebas finales y sustentación\nES | Dur | EF\n69 | 4 | 73\nLS | Holg | LF\n69 | 0 | 73" as T64 <<crit>>

' Inicio y tareas sin predecesoras
INI -[#ff6b6b,thickness=2]-> T51
INI --> T21
INI --> T61
INI --> T62
INI --> T63

' Paquete 5
T51 -[#ff6b6b,thickness=2]-> T52
T51 --> T53
T53 --> T54

' Paquete 1 y 4
T52 -[#ff6b6b,thickness=2]-> T11
T11 --> T12
T11 -[#ff6b6b,thickness=2]-> T41
T12 --> T42
T41 -[#ff6b6b,thickness=2]-> T42
T41 --> T43

' Paquete 2
T21 --> T23
T53 --> T23
T21 --> T22
T23 --> T22
T21 --> T24
T23 --> T24

' Paquete 3
T42 -[#ff6b6b,thickness=2]-> T31
T43 --> T32
T12 --> T33
T31 -[#ff6b6b,thickness=2]-> T33

' Cierre
T22 --> T64
T24 --> T64
T54 --> T64
T32 --> T64
T61 --> T64
T62 --> T64
T63 --> T64
T33 -[#ff6b6b,thickness=2]-> T64

legend bottom
  ES = Inicio temprano | EF = Fin temprano
  LS = Inicio tardío | LF = Fin tardío
  Dur = Duración | Holg = Holgura
  Ruta crítica: 5.1 → 5.2 → 1.1 → 4.1 → 4.2 → 3.1 → 3.3 → 6.4
  14 + 9 + 8 + 14 + 10 + 6 + 8 + 4 = 73 días
endlegend

@enduml
```

# 6. El cronograma contra el equipo real

El cruce de la matriz de asignación de responsabilidades (RACI/OBS) con las fechas de inicio y fin temprano ($ES - EF$) del cronograma permite identificar y resolver conflictos de sobreasignación mediante la nivelación de recursos.

### Identificación de sobreasignaciones y resolución

1. **Vanessa (Hardware / Frontend):**
   * **Conflicto:** Tenía asignadas en paralelo **5.1 Montaje del circuito** (días 0 a 14) y **2.1 Diseño interfaz gráfica** (días 0 a 14).
   * **Resolución:** Aprovechando los **23 días de holgura** de la tarea **2.1**, se reprograma su inicio para el día 14 (desplazada al intervalo días 14 a 28).

2. **Alejandra (Interfaz / Alertas):**
   * **Conflicto:** Solapamiento entre **2.2 Notificación de maniobras contradictorias** (días 34 a 40) y **2.4 Notificación de giros sin direccional** (días 34 a 42).
   * **Resolución:** Al contar con holguras superiores a 25 días, se secuencian para ejecutarse entre los días 34 y 48.

3. **David (Integración / IA):**
   * **Conflicto:** Solapamiento entre **4.1 Mapeo de errores de IA** (días 31 a 45, Ruta Crítica) y **5.4 Pausa por pérdida de conexión** (días 22 a 29).
   * **Resolución:** Se desplaza la ejecución de **5.4** (holgura de 40 días) para iniciar después del día 45, garantizando la dedicación exclusiva a la tarea de la ruta crítica.


# 7. Hitos y línea base
