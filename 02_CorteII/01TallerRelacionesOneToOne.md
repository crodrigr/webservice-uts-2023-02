# Construir un API

Para una biblioteca que permita consultar el listado de libros y crear autores según la siguente relación entre libro y autor. Relación OneToOne Bidireccional.

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/66330c49-06e4-4398-a685-4a366099cac5)

**/**: Petición GET que obtiene el listado de libros con autor

**/{idLibro}**  Petición POST recibe el idLibro y en RequesBody los datos del autor. Guarda la relación entre libro y autor, en la tabla autor. 

## Dependencias del proyecto

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/217a8a38-d85e-4823-befd-e6cbc9aa8216)


## Estructura del proyecto


![image](https://github.com/crodrigr/programacion-java-2023-02/assets/31961588/be9e08c5-a147-4122-98d5-555b0c98a8f8)


## Ejemplo import.sql

El el directorio **resources** se crea un archivo **import.sql** para que ejecute scripts de  **sql** en la base datos. En este caso se va a realizar con insert into libros para tener data de libros en la tabla **libros**

```sql

INSERT INTO LIBROS (TITULO) VALUES('CIEN AÑOS DE SOLEDAD');
INSERT INTO LIBROS (TITULO) VALUES('PROGRAMACION EN PYTHON');
INSERT INTO LIBROS (TITULO) VALUES('LA MEJOR COCINA');



```

## Redundancia ciclica en la serialización JSON

Para evitar la reducancia ciclica en una relación **OneToOne** se debe hacer uso el de **@JsonIgnoreProperties**. Por ejemplo tengo la relación entre Estudiante y Matricula. 

**EstudianteEntity**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/8ba094e4-f054-4ef0-bc1d-fae1950842f8)



**MatriculaEntity**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/031b0cf1-1348-4b73-bebf-f5f6d3031383)




