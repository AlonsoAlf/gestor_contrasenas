Gestor de Contraseñas

Aplicación de línea de comandos desarrollada en Dart puro que permite a los usuarios registrarse, iniciar sesión y gestionar sus contraseñas de forma centralizada. Integra la API pública de Have I Been Pwned(https://haveibeenpwned.com/API/v3#PwnedPasswords) para comprobar si una contraseña ha sido filtrada en alguna brecha de datos conocida y cuántas veces ha aparecido.

Tabla de contenidos

- [Características]
- [Tecnologías utilizadas]
- [Requisitos previos]
- [Instalación]
- [Uso]
- [Estructura del proyecto]
- [Seguridad y mejoras futuras]
- [Autor]

## Características

- **Registro e inicio de sesión** de usuarios.
- **Gestión de contraseñas**: añadir, modificar y eliminar contraseñas asociadas a distintos servicios.
- **Comprobación de filtraciones**: consulta en tiempo real a la API de Have I Been Pwned para saber si una contraseña ha sido comprometida y en cuántas filtraciones ha aparecido, usando el modelo de *k-anonimity* mediante hash **SHA-1**.
- **Persistencia de datos** en una base de datos **MySQL**.
- **Interfaz por consola** guiada por menús numéricos, pensada para ser simple e intuitiva desde la terminal.

## Tecnologías utilizadas

- **[Dart](https://dart.dev/)** (sin Flutter) — lógica de la aplicación y ejecución por terminal.
- **MySQL** — almacenamiento de usuarios y contraseñas.
- **API de Have I Been Pwned** — verificación de contraseñas filtradas (endpoint de rango de hashes SHA-1, no requiere API key).

## Requisitos previos

Antes de ejecutar el proyecto necesitas tener instalado:

- [Dart SDK](https://dart.dev/get-dart) (versión 3.x o superior recomendada)
- Un servidor **MySQL** local o remoto en funcionamiento
- Conexión a internet (para las consultas a la API de HIBP)

## Instalación

1. Clona el repositorio:

   ```bash
   git clone (https://github.com/AlonsoAlf/gestor_contrasenas)
   cd gestor-contrasenas
   ```

2. Instala las dependencias del proyecto:

   ```bash
   dart pub get
   ```

3. Configura la base de datos:
El fichero database.dart esta diseño de forma que la única modificación que tengas que hacer sea comentar la línea 14 en el fichero database.dart, una vez hecho esto, en el terminal ejecutas el fichero main con el comando **dart .\main.dart**
y la base de datos se creará de forma automática y comenzará la ejecución.

<img width="527" height="283" alt="image" src="https://github.com/user-attachments/assets/6917dee7-cbe2-47b8-8245-e20b083ecc99" />


5. Ejecuta la aplicación:
 Utiliza el comando **dart .\main.dart** en el terminal para ejecutar el programa.

##  Uso

Al ejecutar la aplicación se muestra un menú interactivo por terminal. El usuario interactúa introduciendo el **número de la opción** deseada y pulsando **Enter**. El flujo típico es:

<img width="355" height="161" alt="image" src="https://github.com/user-attachments/assets/ae7a3126-fbfa-4b04-9293-afd7b417c856" />


1. Registrarse.
2. Iniciar Sesión.
3. Una vez dentro, elegir entre:
   - Añadir una nueva contraseña (usuario + contraseña asociados a un servicio).
   - Consultar si una contraseña ha sido filtrada y cuántas veces.
   - Modificar una contraseña existente.
   - Eliminar una contraseña.

4. Salir de la aplicación.

<img width="366" height="195" alt="image" src="https://github.com/user-attachments/assets/eb0e8f52-f01d-4e3f-a40c-79042164258c" />

## Estructura del proyecto

```
gestor-contrasenas/
├── bin/
│   ├── entities/
│   │   ├── cuenta.dart          # Modelo del objeto cuenta: cuenta/contraseña y funciones que manejan los datos de la cuenta (recuperar, modificar y borrar)
│   │   └── usuario.dart         # Modelo del objeto usuario: funciones encargadas del registro y el inicio de sesión
│   ├── utils/
│   │   ├── controladormenu.dart # Menús que se muestran por consola
│   │   ├── database.dart        # Creación de la BBDD y sus tablas y conexión con la misma.
│   │   ├── encriptacion.dart    # Hash SHA-1 y consulta a la API de HIBP
│   │   ├── sesionglobal.dart    # Manejo del estado de la sesión del usuario
│   │   └── utils.dart           # Recopilación de todos los ficheros de la carpeta en uno para facilitar las importaciones de ficheros
│   └── main.dart                # Punto de entrada de la aplicación
├── pubspec.yaml                 # Dependencias del proyecto
└── README.md
```


## Mejoras futuras

Este proyecto se desarrolló como proyecto final, y actualmente presenta algunas limitaciones pendientes de mejora:

- **Almacenamiento de contraseñas**: actualmente las contraseñas se guardan en texto plano en la base de datos. El hash SHA-1 solo se utiliza para consultar la API de Have I Been Pwned siguiendo el modelo k-anonimity, no para el almacenamiento. Como mejora futura, se incorporará un algoritmo de hash seguro con salt (como **bcrypt** o **Argon2**) para el almacenamiento real de la información.
- **Gestión de credenciales de configuración**: los datos de conexión a la base de datos se encuentran en un fichero dentro del proyecto. Se plantea migrar a variables de entorno para evitar exponer credenciales en el control de versiones.
- **Creacion de nuevas contraseñas**: se valorará la integración de métodos que creen contraseñas seguras.
- **Integración de una interfaz**: se va a trabajar en desarrollar una interfaz mas avanzada y que mejora la experiencia del usuario (probablemente basada en Flutter, pero no se descarta crear una basada en HTML y CSS de manera provisional y para practicar desarrollo frontend).

## Autor

Desarrollado por Alonso Alfayate como proyecto de aprendizaje en Dart y bases de datos.

- GitHub: [https://github.com/AlonsoAlf]
