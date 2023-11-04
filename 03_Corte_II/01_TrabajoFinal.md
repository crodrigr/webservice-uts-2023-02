# Trabajo final 🌋

<br>

## 1. Problema 🔥

Una agencia inmobiliaria posee varias oficinas. Ya que la ficha de cada inmueble se encuentra en la oficina a la que se ha dirigido el propietario para ponerlo en venta o alquiler, la forma de compartir esta información actualmente es consultándola telefónicamente entre oficinas. A continuación se detallan los datos que se desea conocer sobre los inmuebles, que pueden ser pisos nuevos (apartamentos nuevos), pisos de ocasión(apartamentos usados), villas, casas y locales.

De todos los tipos de inmueble se desea conocer la superficie en m2 y la dirección completa; si se trata de una villa, hay que especificar además el tamaño de la parcela y la urbanización en la que se encuentra. De pisos, villas y casas se quiere conocer cuántas estancias posee de cada tipo: habitaciones, baños, aseos,cocinas, etc., y sus características específicas: si tiene gas ciudad, puerta blindada, parquet, etc. De los locales sólo se quiere conocer sus características: número de puertas de entrada, si es diáfano (vitrina a la calle), si está acondicionado, etc. De pisos, casas y locales se desea conocer la zona de la ciudad en la que se
encuentran. 

Estas zonas son las mismas en las que se encuentra dividido el mapa de la ciudad que se hay en cada oficina y que se utiliza para mostrar la localización de los inmuebles.
Los inmuebles pueden ofrecerse sólo para venta, sólo para alquiler, o para venta o alquiler. 

En cualquier caso, se desea conocer el precio, ya sea de venta o alquiler. Cada inmueble tiene un número de referencia, e interesa el nombre y el teléfono del propietario. Si se posee llaves del inmueble, se deberá reflejar en qué
oficina se encuentran. Además, para cada inmueble se deben anotar las visitas que se han realizado o se van a realizar, con los datos del cliente, fecha y hora de la visita y un comentario sobre la impresión que ha
manifestado el cliente al respecto. La información se guarda actualmente en fichas

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/ad57a357-6624-4e3d-8a28-e97c02190ced)

## 2. Solución 🍾


### Desarrollo de un API para la Gestión de Inmuebles en una Agencia Inmobiliaria

**Descripción:**
La agencia inmobiliaria necesita una solución eficiente para gestionar la información de los inmuebles que posee en varias de sus oficinas. Actualmente, la información se comparte telefónicamente entre oficinas, lo que es ineficiente. Se requiere desarrollar un API con Spring Boot para centralizar y gestionar la información de los inmuebles de manera efectiva.

**Requisitos Funcionales:**

1. **Gestión de Inmuebles:**
   - Registrar nuevos inmuebles con detalles como tipo (piso nuevo, piso de ocasión, villa, casa, local), superficie en m2 y dirección completa.
   - Especificar información adicional según el tipo de inmueble (por ejemplo, número de habitaciones, baños, características específicas).
   - Para villas, registrar el tamaño de la parcela y la urbanización.
   - Para locales, definir características como número de puertas de entrada, si es diáfano, si está acondicionado, etc.
   - Asignar zonas de la ciudad a los inmuebles.
   - Establecer disponibilidad para venta, alquiler o ambas opciones.
   - Indicar el precio de venta y alquiler.
   - Asignar un número de referencia y almacenar los datos del propietario (nombre y teléfono).
   - Gestionar la ubicación de las llaves de los inmuebles en oficinas.
   - Registrar visitas con detalles de los clientes, fecha, hora y comentarios.

**Requisitos Adicionales:**

2. **Gestión de Oficinas:**
   - Registrar oficinas con información de dirección y ubicación en el mapa de la ciudad.

3. **Seguridad:**
   - Implementar autenticación y autorización para proteger las operaciones de gestión de inmuebles y oficinas.

**Tecnologías Utilizadas:**
- Spring Boot para el desarrollo del API RESTful.
- Spring Data JPA para el acceso a la base de datos.
- Base de datos relacional **H2** (opcinal por ejemplo, MySQL, PostgreSQL) para almacenar los datos.
- Autenticación y autorización basada en tokens (por ejemplo, JWT).

**Entregables:**
- Código fuente del API desarrollado en Spring Boot.
- Documentación de la API, incluyendo rutas, parámetros y ejemplos de uso.
- Pruebas unitarias y de integración para garantizar la calidad del código.

**Plazo de Entrega:**
El proyecto debe ser entregado en [indicar plazo] semanas a partir del inicio.

---

Este enunciado proporciona una descripción general del proyecto, sus requisitos funcionales y tecnologías clave. Asegúrate de ajustar el enunciado según los plazos y recursos disponibles para tu proyecto. Una vez que tengas este enunciado, puedes utilizarlo como guía para desarrollar tu API de Spring Boot y documentarla adecuadamente.
