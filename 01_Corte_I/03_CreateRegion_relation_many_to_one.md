# Relaciones en spring data jpa

[Documentación relaciones spring data jpa](https://www.adictosaltrabajo.com/2020/04/02/hibernate-onetoone-onetomany-manytoone-y-manytomany/)

# 1. Región y cliente. 

Una región tiene uno o muchos clientes y un cliente pertenece a una única región. Por parte de la región no nos interesa obtener los clientes por región. Por lo tanto, se convierte e una relación unidireccional desde cliente que si nos interesa saber a que región pertenece.  

![image](https://user-images.githubusercontent.com/31961588/156847559-791a4e02-125d-402e-925a-27cd0be338e9.png)

# 2. Se crea la entidad región

Se crea la entidad región dentro del paquete de entities. 

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/49ace39b-6b91-4890-a09e-55948fdfb2cb)

# 3. Se construye la relación entre cliente y región. 

Esta relación es una relación **ManytoOne** en una sola direción, y va estar al lado del cliente. Se debe crear el atributo Region con sus métodos getter y setter.

El tipo de relacion **@ManyToOne** usa carga peresoza con Fetch Lazy, si se usa, debe tener la anotación **@JsonIgnoreProperties({"hibernateLazyInitializer","handler"})** por que si no, genera error. Ver en el último apartado la explicación

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/72fe4f12-f5cb-44f4-a77d-5ed6b3efca43)


# 4. Se agrega regiones en Import.sql

En el archivo de import.sql se hace el insert de las regiones, con id, para relacionarlo con los clientes.

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/406a118f-c8d1-4d25-acdf-954ae2a353d8)

# 5. Crear un endpoint o servicio para listar las regiones

Este servicio se va asignar al ClienteController para no crear un serivicio completo y exclusivo para regiones, desde la capa de repositories. Por lo tanto, en el ClienteRepoistory se adiciona un método con una consulta personalizada para que traiga el listado de regiones. 

## 5.1 Consulta personlizada para regiones

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/5d237557-80f3-4322-866e-11d596ba1eda)

## 5.2 Se adiciona un método en la interfaz ClienteService

El nuevo método va trae el listado de regiones. 

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/45473eb3-8b96-484f-9723-9b0d82a4bcfb)

## 5.3 Se crea el método findAllRegiones en ClienteServiceImpl

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/2434d757-5786-4de9-b664-3925b03a85c8)

## 5.4 Agregar un endpoin /cliente/regiones en ClienteController  

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/f411a96c-4c56-47e6-a770-58006a6a2ba0)

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/838b3245-cd76-4809-bc4b-2ea983f9f813)

# 6. @JsonIgnoreProperties

La anotación **@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})** se utiliza en relaciones de entidades de Hibernate en aplicaciones de Spring Boot para evitar problemas de serialización y deserialización cíclica al mapear objetos relacionados.

Cuando tienes una relación entre entidades en Hibernate, como una relación de uno a muchos o muchos a muchos, Hibernate utiliza el mecanismo de carga diferida (lazy loading) para cargar los objetos relacionados solo cuando se acceden a ellos. Esto se hace mediante el uso de proxies o clases de implementación especiales generadas por Hibernate.

Sin embargo, al serializar las entidades a JSON (por ejemplo, al devolver una respuesta HTTP con objetos relacionados), podría producirse un problema de serialización cíclica. Esto ocurre cuando un objeto A tiene una referencia al objeto B y el objeto B tiene una referencia nuevamente al objeto A, creando un bucle infinito de referencias.

La anotación **@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})** se utiliza para evitar que se incluyan estas propiedades específicas de Hibernate en la serialización. Al anotar una relación con esta anotación, le estás diciendo a Jackson (la biblioteca utilizada por Spring Boot para la serialización y deserialización JSON) que ignore las propiedades hibernateLazyInitializer y handler durante el proceso de serialización.

Aquí tienes un ejemplo de cómo se usaría esta anotación en una relación:

```Java
@Entity
@Table(name = "parent")
public class Parent {
    @OneToMany(mappedBy = "parent")
    @JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})
    private List<Child> children;
    // otras propiedades y métodos
}

@Entity
@Table(name = "child")
public class Child {
    @ManyToOne
    @JoinColumn(name = "parent_id")
    private Parent parent;
    // otras propiedades y métodos
}


```

En este ejemplo, al anotar la lista children en la clase Parent con **@JsonIgnoreProperties({"hibernateLazyInitializer", "handler"})**, se evita la serialización de esas propiedades específicas durante la respuesta JSON. Esto resuelve el problema de serialización cíclica que puede ocurrir al tener una relación bidireccional entre Parent y Child.
