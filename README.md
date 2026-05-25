# Sistema de Gestión Hospitalaria (SGH)

Proyecto Final — Programación Orientada a Objetos

Aplicación de consola en Python para la gestión de pacientes, médicos, citas y registros clínicos en una institución de salud.

---

## Tabla de Contenidos

- [Descripción General](#descripción-general)
- [Estructura del Proyecto](#estructura-del-proyecto)
- [Arquitectura](#arquitectura)
- [Requisitos](#requisitos)
- [Instalación y Ejecución](#instalación-y-ejecución)
- [Uso del Sistema](#uso-del-sistema)
- [Modelo de Datos](#modelo-de-datos)
- [Estado del Proyecto](#estado-del-proyecto)
- [Autor](#autor)

---

## Descripción General

El Sistema de Gestión Hospitalaria (SGH) permite administrar la información básica de una institución de salud: pacientes, médicos, especialidades y citas médicas. La información se persiste en archivos de texto plano `.txt` dentro de una carpeta local llamada `SGH_datos/`, por lo que los datos se conservan entre sesiones sin necesidad de una base de datos.

---

## Estructura del Proyecto

```
SGH/
│
├── main.py                  # Punto de entrada del sistema
│
└── SGH_datos/               # Carpeta generada automáticamente al ejecutar
    ├── pacientes.txt
    ├── medicos.txt
    ├── especialidades.txt
    └── citas.txt
```

La carpeta `SGH_datos/` y sus archivos se crean automáticamente al ejecutar el programa por primera vez.

---

## Arquitectura

El proyecto sigue una arquitectura en capas que separa las responsabilidades de cada componente:

```
Interfaz de Usuario  →  Menús y entrada/salida por consola
Capa de Servicio     →  Lógica de negocio y validaciones
Capa de Repositorio  →  Acceso y persistencia en archivos
Capa de Dominio      →  Clases del modelo (entidades)
```

Las clases principales del dominio son `Paciente`, `Medico`, `Especialidad` y `Cita`. Cada entidad sabe cómo serializarse a una línea de texto (`to_linea`) y reconstruirse desde ella (`from_linea`). La clase `ArchivoUtil` centraliza todas las operaciones de lectura y escritura sobre los archivos, y los repositorios usan esa utilidad para abstraer el acceso al almacenamiento. Los servicios aplican las reglas de negocio antes de delegar en los repositorios.

Para garantizar valores controlados se usan enumeraciones: `RegimenEnum` (`CONTRIBUTIVO` / `SUBSIDIADO`) y `EstadoCitaEnum` (`PROGRAMADA` / `ATENDIDA` / `CANCELADA`).

---

## Requisitos

Python 3.7 o superior. No requiere librerías externas; solo se usan módulos de la biblioteca estándar: `enum`, `datetime` y `os`.

---

## Instalación y Ejecución

Clona el repositorio y ejecuta el archivo principal:

```bash
git clone https://github.com/tu-usuario/sistema-gestion-hospitalaria.git
cd sistema-gestion-hospitalaria
python main.py
```

---

## Uso del Sistema

Al iniciar se muestra el menú principal con los cinco módulos del sistema. Desde el submenú de pacientes se puede registrar un nuevo paciente, consultarlo por número de documento o listar todos los registrados.

Los datos se almacenan en texto plano separados por `|`. Por ejemplo, un registro en `pacientes.txt` se ve así:

```
10234567|Juan Pérez|1990-05-14|O+|SURA|CONTRIBUTIVO|Hipertensión
```

---

## Modelo de Datos

### Paciente

| Campo | Descripción |
|---|---|
| `num_documento` | Identificador único del paciente |
| `nombre` | Nombre completo |
| `fecha_nacimiento` | Formato `AAAA-MM-DD` |
| `tipo_sangre` | Ej: `O+`, `A-` |
| `eps` | Entidad Promotora de Salud |
| `regimen` | `CONTRIBUTIVO` o `SUBSIDIADO` |
| `antecedentes` | Historial de condiciones médicas |

### Medico

| Campo | Descripción |
|---|---|
| `num_registro` | Número de registro médico |
| `nombre` | Nombre completo |
| `especialidad` | Especialidad médica |
| `consultorio` | Número o nombre del consultorio |
| `horario` | Horario de atención |

### Cita

| Campo | Descripción |
|---|---|
| `codigo` | Código único generado automáticamente con marca de tiempo |
| `num_documento_paciente` | Referencia al paciente |
| `num_registro_medico` | Referencia al médico |
| `fecha` / `hora` | Fecha y hora de la cita |
| `motivo` | Motivo de consulta |
| `estado` | `PROGRAMADA`, `ATENDIDA` o `CANCELADA` |

---

## Estado del Proyecto

El módulo de pacientes está completamente implementado: registro, consulta, listado y persistencia. Los módulos de médicos, citas, registro clínico y análisis de datos están definidos en el menú principal pero pendientes de implementación en el siguiente avance.

---

## Autor

**[David Santiago Vargas Parra]**  
**[Sergio Andres Cristancho Moreno]**
[Universidad de Santander]  
[2026] — Proyecto Final de [Programación II]
