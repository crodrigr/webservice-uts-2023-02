# Usuario y Roles

Todos los sistemas tienen su modulo de **usuarios** que gestiona la información de las personas que interactuan con el aplicativo. Información como el username, password, nombre, entro otros. Un usuario puede tener varios permisos, y estos permisos se pueden agrupar, y la mejor forma de hacerlo es por medio de **roles**. Por lo tanto, se va tener una relación entre **usuario** y **role**. Un usuario puede tener uno o varios roles, y un role puede estar asignado en varios usarios. 

Se crea la clase Role de tipo Entity. A continuación el diagrama de clases. Es una relación de muchos a muchos bidireccional entre **Usuario** y **Role** 

```mermaid
classDiagram
    Usuario "1..*" <--> "1..*" Role
    Usuario : -Long id
    Usuario : -String username
    Usuario : -String password
    Usuario : -Boolean enable
    Usuario : -String nombre
    Usuario : -String apellido
    Usuario : -String email
    Usuario: +getter()
    Usuario: +setter()
    class Role{
        -Long id
        +String nombre
        +getterSetter()        
    }
    
```

## 1. Crear entity Role

```mermaid
classDiagram    
     class Role{
        -Long id
        +String nombre
        +getterSetter()        
    }
    
```

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/970d7e93-0c26-4795-ae4e-f0c94fea4d87)

## 2. Crear entity Usuario

Se crea la clase Usuario de tipo Entity

```mermaid
classDiagram    
    class Usuario{
         -Long id
         -String username
         -String password
         -Boolean enable
         -String nombre
         -String apellido
         -String email
         +getter()
         +setter()     
    }
    
```

### 2.1 Atributos
![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/488f355e-6bd4-47fb-ad7c-c0716da7d5e9)

### 2.2 Getter y Setter

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/72cbe6e0-fb77-4878-a61b-87cf37a844ed)

## 3. Insert de usuario y roles

En el archivo import.sql se adiciona los scripts para insertar roles, usuarios, usuarios y roles. Esto a que es una relación muchos a muchos

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/52fdd256-c60e-4cf8-8e36-7b0f383dd574)
