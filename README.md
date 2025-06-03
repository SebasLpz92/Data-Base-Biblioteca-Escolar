# Base de Datos Biblioteca

## Descripción

Esta base de datos está diseñada para gestionar una biblioteca simple que controla los libros disponibles y los préstamos realizados por los usuarios.

---

## Estructura de las Tablas

### Tabla: `libros`

- **id** (INT, AUTO_INCREMENT, PRIMARY KEY): Identificador único para cada libro.
- **Titulo** (VARCHAR(255), NOT NULL): Título del libro.
- **Autor** (VARCHAR(255)): Nombre del autor del libro.
- **Isbn** (VARCHAR(20), NOT NULL, UNIQUE): Código ISBN único del libro.
- **cantidad** (INT, DEFAULT 1): Número de ejemplares disponibles.

### Tabla: `Prestamos`

- **id** (INT, AUTO_INCREMENT, PRIMARY KEY): Identificador único del préstamo.
- **nombre_usuario** (VARCHAR(100), NOT NULL): Nombre del usuario que realiza el préstamo.
- **libro_id** (INT, NOT NULL): Referencia al `id` del libro prestado.
- **fecha_prestamo** (DATE, DEFAULT CURDATE()): Fecha en la que se realiza el préstamo.

**Relación entre tablas:**

- `libro_id` es clave foránea que referencia a `libros(id)` con `ON DELETE CASCADE`.
- Si un libro es eliminado, se eliminan automáticamente sus préstamos asociados.

---

## Funcionamiento

- Se registran libros con título, autor, ISBN y cantidad disponible.
- Los préstamos registran qué usuario tomó qué libro y cuándo.
- La integridad referencial evita préstamos sin libro asociado.
- La eliminación de un libro elimina sus préstamos relacionados.

---

## Posibles mejoras

- Añadir tabla para usuarios con más detalles.
- Controlar cantidad disponible ajustándola en préstamos y devoluciones.
- Registrar fecha de devolución y estado del préstamo.
- Añadir triggers o procedimientos para manejar la lógica de préstamo.

---

## Código SQL

```sql
CREATE TABLE libros (
    id INT AUTO_INCREMENT PRIMARY KEY,
    Titulo VARCHAR(255) NOT NULL,
    Autor VARCHAR(255),
    Isbn VARCHAR(20) NOT NULL UNIQUE,
    cantidad INT DEFAULT 1
);

CREATE TABLE Prestamos (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre_usuario VARCHAR(100) NOT NULL,
    libro_id INT NOT NULL,
    fecha_prestamo DATE DEFAULT CURDATE(),
    FOREIGN KEY (libro_id) REFERENCES libros(id) ON DELETE CASCADE
);
