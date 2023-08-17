# Crear factura

En esta sección se va construir las clases entities que hace faltan del proyecto de facturación. Se va iniciar con la creación de la clase **Producto**, dicha clase no tiene dependencias. Luego se continua con **Item** de la factura y finalmente con **Factura**

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/6dcd9c12-46d1-4ed9-b069-ef82de2e23d1)

## 1. Crear la entity Producto

Dentro del directorio de entites se crea una nueva clase **Producto** de tipo **@Entity**

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/c0e981ce-af6b-4e67-8eb6-2df56325d6f0)

### 1.1 Insert de productos en import.sql

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/6acbf681-fc80-4090-b228-ac3f2a0e94c0)

## 2. Crear ItemFactura 

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/398bf97f-d446-4460-b647-1f85c56e244b)

## 3. Crear Factura

### 3.1 Factura.java
![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/30b389ac-b526-40cc-a6e5-8df33ba797c3)

### 3.2 Factura getter y setter
![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/48eb4a0e-e11a-45b2-9b49-fd7ba8d676e8)

### 3.3 Relación cliente con factura

Un cliente tiene una o muchas facturas. Construir la relación desde el cliente a factura de **OneToMany**

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/9e7a73a5-7225-46ae-8093-ca8df06aaad3)

### 3.4 Insert de facturas

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/9d376c64-8937-4a4e-9ab5-5e55904ece65)

## 4. Crear el ProductoRepository

Se crea una consulta personalizada para buscar productos por nombre. Esta consulta se va usar en el front para un buscador de productos. 

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/9de75182-6314-410c-9a5f-2c9b019feaf7)


## 5. Crear la FacturaRepository

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/e8dc2f4c-d43b-4d1a-b18a-5c61d7ff22b8)

## 6. Servicios de factura en ClienteService

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/bfc81453-dc74-44ca-be88-2cf1c3dd6682)

## 7. ClienteServiceImpl implementación

En la clase **ClienteServiceImpl** se implenta los método de factura definidos en la interfaz **ClienteService**

### 7.1 Inyección de dependencia

Se hace la inyección de dependencia de **ProductoRepository** y **FacturaRepository**

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/3b96f31d-7b84-4fa4-b37e-b6603061dfaa)

### 7.2 Implementación o sobreescritura de métodos

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/52d7930f-a561-4644-9bf8-6edbd2a69492)

## 8. Crear el FacturaController

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/051f9541-f077-4955-8165-9e4bbc4b0fb0)
