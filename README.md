#  Sistema de Gestión Hospitalaria (SGH)

Sistema de gestión hospitalaria desarrollado en Python para Google Colab, con interfaz interactiva mediante `ipywidgets` y persistencia de datos en archivos `.txt`. Permite administrar pacientes, médicos, citas, registros clínicos y análisis estadísticos.

---

##  Tabla de contenidos

- [Características](#características)
- [Requisitos](#requisitos)
- [Instalación y ejecución](#instalación-y-ejecución)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Módulos del sistema](#módulos-del-sistema)
- [Formato de datos](#formato-de-datos)
- [Consideraciones](#consideraciones)

---

##  Características

- Registro y consulta de pacientes y médicos.
- Programación, consulta y cancelación de citas médicas.
- Registro clínico con diagnóstico (CIE-10), signos vitales, tratamiento y medicamentos.
- Historial clínico cronológico por paciente.
- Análisis de datos: promedios de consultas, diagnósticos frecuentes, ocupación por especialidad, distribución por EPS y medicamentos más prescritos.
- Persistencia automática en archivos `.txt` mediante separador `|`.
- Compatible con Google Drive para almacenamiento en la nube.

---

##  Requisitos

- Python 3.7 o superior
- Google Colab (recomendado) o entorno local con Jupyter Notebook
- Librerías estándar: `os`, `datetime`, `collections`
- Librería externa:

```
ipywidgets
```

Para instalar en entorno local:

```bash
pip install ipywidgets
jupyter nbextension enable --py widgetsnbextension
```

---

##  Instalación y ejecución

### En Google Colab

1. Sube el archivo `.py` o pega el código en una celda de Colab.
2. Ejecuta la celda. El sistema intentará montar automáticamente Google Drive en `/content/drive/MyDrive/SGH/datos/`.
3. Si el montaje falla, los datos se guardarán localmente en `SGH/datos/`.
4. El menú principal aparecerá de forma interactiva en la salida de la celda.

### En entorno local

1. Clona o descarga el archivo del proyecto.
2. Instala las dependencias necesarias.
3. Ejecuta el script dentro de un Jupyter Notebook:

```bash
jupyter notebook
```

4. Abre el archivo y ejecuta todas las celdas.

---

##  Estructura del proyecto

```
SGH/
└── datos/
    ├── pacientes.txt
    ├── medicos.txt
    ├── citas.txt
    ├── consultas.txt
    ├── tratamientos.txt
    └── medicamentos.txt
```

Todos los archivos se crean automáticamente al iniciar el sistema si no existen.

---

##  Módulos del sistema

### 1. Pacientes

Permite registrar y listar pacientes con los siguientes datos:

| Campo | Descripción |
|---|---|
| Documento | Identificación única del paciente |
| Nombre | Nombre completo |
| Fecha de nacimiento | Formato `AAAA/MM/DD` |
| Tipo de sangre | O+, O-, A+, A-, B+, B-, AB+, AB- |
| EPS | Entidad promotora de salud |
| Régimen | Contributivo o Subsidiado |
| Antecedentes | Antecedentes médicos relevantes |

### 2. Médicos

Registro y búsqueda de médicos por especialidad.

| Campo | Descripción |
|---|---|
| Registro | Identificación única del médico |
| Nombre | Nombre completo |
| Especialidad | Medicina General, Pediatría, Cardiología, Ortopedia, Dermatología, Neurología, Psiquiatría |
| Consultorio | A1, A2, A3, B1, B2, B3 |
| Horario | 08:00-20:00 o 20:00-08:00 |

### 3. Citas

Gestión completa del ciclo de una cita médica.

- **Programar:** valida disponibilidad del médico en fecha y hora seleccionadas.
- **Consultar:** búsqueda por código de cita.
- **Cancelar:** cambia el estado a `CANCELADA` y registra el motivo.
- **Listar por rango:** filtra citas por paciente o médico entre dos fechas.

Estados posibles: `ACTIVA`, `ATENDIDA`, `CANCELADA`.

### 4. Registro Clínico

Registro de la consulta médica vinculada a una cita activa.

- Diagnóstico con código CIE-10.
- Síntomas y signos vitales (presión, temperatura, frecuencia cardíaca).
- Observaciones clínicas.
- Tratamiento con medicamento, dosis, frecuencia y duración en días.
- Al guardar, la cita asociada cambia automáticamente a estado `ATENDIDA`.
- Consulta del historial clínico cronológico completo del paciente.

### 5. Análisis de Datos

Reportes estadísticos con filtro opcional por rango de fechas:

| Reporte | Descripción |
|---|---|
| Promedio de consultas por médico | Total y promedio diario en el periodo indicado |
| Diagnósticos frecuentes (CIE-10) | Los N diagnósticos más registrados |
| Ocupación por especialidad | Citas programadas vs. atendidas y tasa de ocupación |
| Distribución EPS y régimen | Cantidad y porcentaje de pacientes por EPS, régimen y combinación |
| Medicamentos más prescritos | Los N medicamentos con mayor número de prescripciones |

---

##  Formato de datos

Cada archivo `.txt` almacena un registro por línea, con campos separados por el carácter `|`.

**Ejemplo — pacientes.txt:**
```
12345678|Juan Pérez|1990/05/15|O+|EPS Sura|CONTRIBUTIVO|Hipertensión
```

**Ejemplo — citas.txt:**
```
CIT-20240601120000|12345678|MED001|2024/06/10|09:00|Control general|ACTIVA|
```

> El carácter `|` está reservado como separador. El sistema lo elimina automáticamente de cualquier dato ingresado por el usuario.

---

##  Consideraciones

- Las fechas deben ingresarse siempre en formato `AAAA/MM/DD`.
- El documento del paciente y el registro del médico son identificadores únicos; no se permiten duplicados.
- Para el correcto funcionamiento de los análisis, se recomienda ingresar datos completos en todos los módulos.
- En Google Colab, los datos persisten en Google Drive entre sesiones; en entorno local, en la carpeta `SGH/datos/` relativa al directorio de ejecución.
- El sistema no implementa autenticación de usuarios; se recomienda uso en entornos controlados.

##  Autores

- David Santiago Vargas Parra
- Sergio Andres Cristancho Moreno
- Universidad de Santander
- Ingenieria de Software
