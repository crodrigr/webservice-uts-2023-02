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

```sql

INSERT INTO LIBROS (TITULO) VALUES('CIEN AÑOS DE SOLEDAD');
INSERT INTO LIBROS (TITULO) VALUES('PROGRAMACION EN PYTHON');
INSERT INTO LIBROS (TITULO) VALUES('LA MEJOR COCINA');



```

## Redundancia ciclica en la serialización JSO

Para evitar la reducancia ciclica en una relación **OneToOne** se debe hacer uso el de **@JsonIgnoreProperties**. Por ejemplo tengo la relación entre Estudiante y Matricula. 

**EstudianteEntity**

![Uploading image.png…]()


**MatriculaEntity**
![Uploading image.png…]()



