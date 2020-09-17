Lineamientos para el Desarrollo de Software del ITColima
=======================================
*Un código bonito, es un código más fácil de leer*

Lenguaje PHP
----------------------------------------

Seguir la recomendación de estructura del código PSR-1 y PSR-12 del ***PHP
Framework Interop Group*** (https://www.php-fig.org)

- PSR-1: Basic Coding Standard (https://www.php-fig.org/psr/psr-1/)
- PSR-12: Extended Coding Style Guide (https://www.php-fig.org/psr/psr-12/)

Bases de datos
----------------------------------------

Todo diseño de base de datos debe colocarse en archivo SQL estándar.

Las actualizaciones de la base de datos, una vez implementada en producción,
deberán hacerse mediante scripts independientes, cuyo nombre tenga el patrón:
`database_<año{4}><mes{2}><dia{2}>.sql`

Todas las tablas cuentan con dos columnas al final que corresponden a la fecha
de creación y actualización (create_time, update_time).

Los nombres de las tablas tienen que ser en minúsculas separando palabras con
guión bajo `_`.

Los nombres de los columnas tienen que ser en minúsculaes separando palabras con
guión bajo `_`.

Las palabras clave (*keywords*) de SQL deben ser en MAYÚSCULAS.

Las llaves primarias de cada tabla deben ser las primeras columnas visibles.

Las llaves foraneas se colocan después de de las llaves primarias.

En el caso de la base de datos de SIITEC 2 los nombres de las llaves deben ser
`<nombre>_id`, para otras bases de datos preferir la estructura `id_<nombre>`.

Mantener una identación por columnas de nombre, tipo, nulabilidad, y opciones
en tabulaciones.

Todas las definiciones de llaves primarias, únicas, índices y foráneas, deberán
hacerse dentro de la misma tabla con la referencia al final.

Ejemplo:
```sql
CREATE TABLE usuarios (
    id_usuario      INTEGER         NOT NULL    AUTO_INCREMENT,
    usuario         VARCHAR(30)     NOT NULL,
    contrasenia     VARCHAR(255)    NOT NULL,
    create_time     TIMESTAMP       NOT NULL    DEFAULT CURRENT_TIMESTAMP,
    update_time     TIMESTAMP       NOT NULL    DEFAULT CURRENT_TIMESTAMP   ON UPDATE CURRENT_TIMESTAMP,
    PRIMARY KEY     (id_usuario)
);

CREATE TABLE permisos (
    id_permiso      INTEGER         NOT NULL    AUTO_INCREMENT,
    id_usuario      INTEGER         NOT NULL,
    create_time     TIMESTAMP	    NOT NULL    DEFAULT CURRENT_TIMESTAMP,
    update_time     TIMESTAMP       NOT NULL    DEFAULT CURRENT_TIMESTAMP   ON UPDATE CURRENT_TIMESTAMP,
    PRIMARY KEY     (id_permiso),
    FOREIGN KEY     (id_usuario)    REFERENCES  usuarios(id_usuario)
)
```