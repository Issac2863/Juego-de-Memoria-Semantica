---

README para Desarrolladores

Este archivo README proporciona las instrucciones necesarias para que los desarrolladores puedan configurar y ejecutar el proyecto localmente utilizando MySQL Workbench.


---

Proyecto: Memoria Semántica

Este proyecto es una aplicación web para terapeutas y pacientes, diseñada para fortalecer las capacidades cognitivas mediante un juego interactivo. Incluye funcionalidades como inicio de sesión, visualización de pacientes y estadísticas de sus partidas.


---

Requisitos Previos

1. Software

Python 3.8 o superior

MySQL Server y MySQL Workbench

Un editor de texto o IDE (como Visual Studio Code o PyCharm)


2. Bibliotecas de Python

Instalar las siguientes dependencias usando pip:

Flask

mysql-connector-python



---

Pasos para Ejecutar el Proyecto

1. Clonar el Repositorio

git clone <URL_DEL_REPOSITORIO>
cd <NOMBRE_DEL_PROYECTO>

2. Crear la Base de Datos con MySQL Workbench

1. Abre MySQL Workbench e inicia sesión con tu usuario y contraseña de MySQL.


2. Ve a la pestaña Query.


3. Copia y pega el siguiente script en el editor de consultas y ejecútalo para crear la base de datos y las tablas necesarias:

CREATE DATABASE memoria_semantica;

USE memoria_semantica;

CREATE TABLE terapeutas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    correo VARCHAR(255) UNIQUE NOT NULL,
    contraseña VARCHAR(64) NOT NULL
);

CREATE TABLE pacientes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(255) NOT NULL
);

CREATE TABLE jugadas (
    id INT AUTO_INCREMENT PRIMARY KEY,
    paciente_id INT NOT NULL,
    errores INT NOT NULL,
    tiempo INT NOT NULL,
    FOREIGN KEY (paciente_id) REFERENCES pacientes(id)
);

INSERT INTO terapeutas (correo, contraseña) VALUES
('terapeuta@ejemplo.com', SHA2('password123', 256));


4. Verifica que las tablas se hayan creado correctamente desde el panel de exploración de esquema en MySQL Workbench.



3. Configurar la Conexión a la Base de Datos

1. Abre el archivo db_connection.py y actualiza los datos de conexión para que coincidan con tu configuración local:

import mysql.connector

def create_connection():
    return mysql.connector.connect(
        host="localhost",
        user="<USUARIO>",          # Reemplaza con tu usuario de MySQL
        password="<CONTRASEÑA>",   # Reemplaza con tu contraseña de MySQL
        database="memoria_semantica"
    )



4. Instalar Dependencias

Ejecuta este comando para instalar las bibliotecas necesarias:

pip install flask mysql-connector-python

5. Ejecutar la Aplicación

1. Asegúrate de estar en el directorio raíz del proyecto.


2. Inicia el servidor de desarrollo:

python app.py


3. Accede a la aplicación en tu navegador en http://127.0.0.1:5000.




---

Estructura del Proyecto

<RAIZ_DEL_PROYECTO>/
│
├── templates/
│   ├── login.html         # Página de inicio de sesión
│   └── index.html         # Página principal del juego
│
├── app.py                 # Lógica principal de la aplicación
├── db_connection.py       # Configuración de la conexión a MySQL
├── requirements.txt       # Dependencias del proyecto
└── README.md              # Este archivo


---

Notas Importantes

Si usas otro puerto que no sea el 3306 para MySQL, actualiza el parámetro port en db_connection.py:

mysql.connector.connect(
    host="localhost",
    user="<USUARIO>",
    password="<CONTRASEÑA>",
    database="memoria_semantica",
    port=<PUERTO>
)

Los terapeutas y pacientes adicionales deben ser añadidos directamente desde MySQL Workbench o con una funcionalidad futura en la aplicación.



---

Contribuciones

Si deseas contribuir al proyecto, envía un Pull Request o contacta al administrador del repositorio.


---

¿Te gustaría agregar algo más, como instrucciones para desplegar el proyecto en producción?