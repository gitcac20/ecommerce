# Ecommerce API

## Descripción

Ecommerce API es una aplicación REST desarrollada con **Spring Boot** para administrar un sistema de comercio electrónico.

La API permite gestionar productos, categorías y carritos de compra mediante operaciones CRUD, realizar búsquedas por nombre y categoría, controlar el stock de los productos y administrar el contenido de un carrito.

---

# Tecnologías utilizadas

- Java 17
- Spring Boot
- Spring Web MVC
- Spring Data JPA
- Hibernate
- MySQL
- Maven
- Lombok
- Hibernate Validator

---

# Requisitos

Antes de ejecutar el proyecto es necesario tener instalado:

- Java 17
- Maven
- MySQL (XAMPP o MySQL Server)
- Un IDE compatible (IntelliJ IDEA, Eclipse o VS Code)

---

# Configuración de la base de datos

Crear una base de datos llamada:

```sql
CREATE DATABASE ecommerce;
```

Luego verificar la configuración del archivo `application.properties`.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/ecommerce
spring.datasource.username=root
spring.datasource.password=
```

---

# Cómo ejecutar la aplicación

1. Clonar el repositorio.

```bash
git clone https://github.com/gitcac20/ecommerce.git
```

2. Abrir el proyecto con Maven.

3. Crear la base de datos **ecommerce**.

4. Ejecutar la clase principal del proyecto.

5. La API estará disponible en:

```text
http://localhost:8080
```

---

# Endpoints

## Productos

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | `/productos` | Lista todos los productos |
| GET | `/productos/{id}` | Obtiene un producto por ID |
| POST | `/productos` | Crea un producto |
| PUT | `/productos/{id}` | Actualiza un producto |
| DELETE | `/productos/{id}` | Elimina un producto |
| GET | `/productos/nombre/{nombre}` | Buscar productos por nombre |
| GET | `/productos/categoria/{categoria}` | Buscar productos por categoría |

---

## Categorías

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | `/categorias` | Lista todas las categorías |
| GET | `/categorias/{id}` | Obtiene una categoría |
| POST | `/categorias` | Crea una categoría |
| PUT | `/categorias/{id}` | Actualiza una categoría |
| DELETE | `/categorias/{id}` | Elimina una categoría |

---

## Carritos

| Método | Endpoint | Descripción |
|---------|----------|-------------|
| GET | `/carritos` | Lista todos los carritos |
| GET | `/carritos/{id}` | Obtiene un carrito |
| POST | `/carritos` | Crea un carrito vacío |
| POST | `/carritos/{carritoId}/productos/{productoId}` | Agrega un producto al carrito |
| DELETE | `/carritos/{id}/vaciar` | Vacía el carrito |
| DELETE | `/carritos/{id}` | Elimina un carrito |

---

# Pruebas con Thunder Client

La URL base de la API es:

```text
http://localhost:8080
```

Para los endpoints que reciben datos (**POST** y **PUT**):

- Seleccionar **Body → JSON**.
- Enviar el encabezado:

```text
Content-Type: application/json
```

---

## 1. Crear una categoría

**POST**

```text
http://localhost:8080/categorias
```

**Body**

```json
{
  "nombre": "Notebooks",
  "descripcion": "Computadoras portátiles"
}
```

---

## 2. Verificar que se creó

**GET**

```text
http://localhost:8080/categorias
```

---

## 3. Obtener la categoría por ID

**GET**

```text
http://localhost:8080/categorias/1
```

---

## 4. Crear un producto

**POST**

```text
http://localhost:8080/productos
```

**Body**

```json
{
  "nombre": "Notebook Lenovo",
  "precio": 1500000,
  "stock": 10,
  "imagenUrl": "https://imagen.com/notebook.jpg",
  "categoria": {
    "id": 1
  }
}
```

---

## 5. Listar productos

**GET**

```text
http://localhost:8080/productos
```

---

## 6. Obtener un producto por ID

**GET**

```text
http://localhost:8080/productos/1
```

---

## 7. Buscar productos por nombre

**GET**

```text
http://localhost:8080/productos/nombre/Notebook
```

---

## 8. Buscar productos por categoría

**GET**

```text
http://localhost:8080/productos/categoria/Notebooks
```

---

## 9. Actualizar un producto

**PUT**

```text
http://localhost:8080/productos/1
```

**Body**

```json
{
  "nombre": "Notebook Lenovo Gamer",
  "precio": 1800000,
  "stock": 8,
  "imagenUrl": "https://imagen.com/notebook2.jpg",
  "categoria": {
    "id": 1
  }
}
```

---

## 10. Crear un carrito

**POST**

```text
http://localhost:8080/carritos
```

No requiere Body.

---

## 11. Ver los carritos

**GET**

```text
http://localhost:8080/carritos
```

---

## 12. Agregar un producto al carrito

**POST**

```text
http://localhost:8080/carritos/1/productos/1
```

No requiere Body.

Para verificar que el stock disminuyó:

**GET**

```text
http://localhost:8080/productos/1
```

Al agregar un producto al carrito, el stock se reduce automáticamente en una unidad.

---

## 13. Ver un carrito

**GET**

```text
http://localhost:8080/carritos/1
```

---

## 14. Vaciar un carrito

**DELETE**

```text
http://localhost:8080/carritos/1/vaciar
```

---

## 15. Eliminar un carrito

**DELETE**

```text
http://localhost:8080/carritos/1
```

---

## 16. Eliminar un producto

**DELETE**

```text
http://localhost:8080/productos/1
```

---

## 17. Eliminar una categoría

**DELETE**

```text
http://localhost:8080/categorias/1
```

---

# Validaciones

La API implementa validaciones utilizando **Hibernate Validator**.

- El nombre del producto no puede estar vacío.
- El precio debe ser mayor que cero.
- El stock no puede ser negativo.
- El nombre de la categoría no puede estar vacío.

---

# Manejo de errores

La aplicación implementa un manejo global de excepciones.

| Código HTTP | Descripción |
|-------------|-------------|
| 200 OK | Operación realizada correctamente |
| 201 Created | Recurso creado correctamente |
| 400 Bad Request | Datos inválidos o stock insuficiente |
| 404 Not Found | Producto, categoría o carrito inexistente |
| 500 Internal Server Error | Error inesperado del servidor |

---

# Funcionalidades principales

- Gestión de productos.
- Gestión de categorías.
- Gestión de carritos.
- Búsqueda de productos por nombre.
- Búsqueda de productos por categoría.
- Validación de datos.
- Manejo global de excepciones.
- Control automático del stock al agregar productos al carrito.

---

# Autor

Proyecto desarrollado como trabajo práctico para la materia de Programación Java con Spring Boot.