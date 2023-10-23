
## 1. Spring boot

Una organización no gubernamental (ONG) dedicada a la protección de los derechos de los animales se muestra profundamente preocupada por el bienestar de los animales y las diversas especies que residen en zoológicos alrededor del mundo. En aras de abordar esta inquietud, se plantea la creación de una solución tecnológica que permita la gestión integral de toda la información relacionada.

Con el propósito de cumplir con este objetivo, se propone el desarrollo de una API REST, la cual estará disponible para una amplia variedad de entidades, incluyendo organizaciones privadas, gubernamentales, otras ONG y cualquier individuo interesado. Este sistema permitirá el acceso a información detallada sobre los animales y especies alojados en los zoológicos, promoviendo así la transparencia y la concienciación acerca de su bienestar.

En cuanto a la responsabilidad de ingresar los datos relativos a los animales, esta incumbirá a los propios zoológicos. A continuación, se detallan los requisitos esenciales del sistema.

Cada zoológico se caracteriza por su identificación, que incluye su nombre, ciudad y país de ubicación, así como su extensión en metros cuadrados y el presupuesto anual asignado. Por otro lado, respecto a las especies animales, se almacena su denominación común y científica, su clasificación en términos de familia, y se registra si se encuentran en situación de peligro de extinción. Además, para cada individuo animal que reside en estos zoológicos, se guarda información detallada, incluyendo un número de identificación único, su especie, género, año de nacimiento, lugar de origen (país), y su región geográfica (continente).

**Tablas con algunos datos de ejemplos**

Aquí tienes ejemplos de zoológicos, especies y algunos animales en una tabla Markdown:

```markdown
| Zoológico     | Ciudad       | País          | Tamaño (m2) | Presupuesto Anual (USD) |
|---------------|--------------|---------------|------------|-------------------------|
| Zoo A         | Ciudad A     | País A        | 10000      | 500000                  |
| Zoo B         | Ciudad B     | País B        | 8000       | 400000                  |
| Zoo C         | Ciudad C     | País C        | 12000      | 600000                  |

| Especie Animal | Nombre Vulgar     | Nombre Científico      | Familia      | En Peligro de Extinción  |
|----------------|-------------------|------------------------|--------------|--------------------------|
| Tigre          | Tigre común       | Panthera tigris        | Felidae      | Sí                       |
| Jirafa         | Jirafa común      | Giraffa camelopardalis | Giraffidae   | No                       |
| Elefante       | Elefante asiático | Elephas maximus        | Elephantidae | Sí                       |

| Número de Identificación | Especie     | Sexo  | Año de Nacimiento  | País de Origen | Continente |
|--------------------------|-------------|-------|--------------------|----------------|------------|
| 001                      | Tigre       | Macho | 2010               | India          | Asia       |
| 002                      | Jirafa      | Hembra| 2015               | Sudáfrica      | África     |
| 003                      | Elefante    | Macho | 2012               | Tailandia      | Asia       |
```

**Desarrolle un servicio web API REST utilizando Java y Spring Boot para satisfacer los siguientes requerimientos:**

-  Estructura del Proyecto: El proyecto debe seguir una estructura organizativa que incluye las capas de controladores (controllers), servicios (services), y repositorios (repositories). En la capa de repositories, se deben definir las entidades (entities) que representarán los objetos de la base de datos.

-  Base de Datos: La base de datos utilizada será H2 SQL, una base de datos en memoria. Para poblar la base de datos con datos iniciales, se debe incluir un archivo import.sql. Cada una de las tablas en la base de datos debe contener minimo los registros propocionados en la tablas de ejemplo.

-  Creación de Registros de Animales: Debe existir un servicio que permita la creación de registros de animales, los cuales deben estar asociados a un **zoológico** y **especia** existente y  en la base de datos. Cada animal debe tener una relación con un zoológico existente.

-  Consulta de Zoológicos y sus Animales Asociados: Debe proporcionarse un servicio que permita la consulta de información detallada sobre un zoológico específico, incluyendo la lista de animales que están relacionados con ese zoológico. Esto se logrará mediante la identificación del zoológico por su identificador único (ID) y la presentación de una lista de los animales vinculados a él.
