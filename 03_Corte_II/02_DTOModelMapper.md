# Tutorial implementar DTO con model mapper

DTO es una abreviatura de **"Data Transfer Object"** en el contexto de programación y desarrollo de software. Un DTO no es un patrón de diseño formal, sino un concepto que se utiliza para transferir datos entre diferentes componentes de una aplicación. Su propósito principal es encapsular un conjunto de datos y enviarlos desde una capa de la aplicación a otra, lo que facilita la comunicación entre las capas.

Los DTOs son especialmente útiles en arquitecturas de aplicaciones en capas, como las aplicaciones empresariales, donde los datos necesitan pasar a través de varias capas, como la capa de presentación, la capa de lógica de negocio y la capa de acceso a datos. Algunas de las razones para utilizar DTOs incluyen:

1. **Evitar la exposición de detalles internos:** Los DTOs permiten ocultar los detalles internos de las entidades de dominio y proporcionar solo la información necesaria para la capa que necesita los datos.

2. **Optimizar el rendimiento:** Puedes reducir la cantidad de datos transferidos entre las capas, enviando solo los datos necesarios.

3. **Compatibilidad:** Ayudan a gestionar la compatibilidad entre diferentes versiones de la aplicación, ya que puedes cambiar la estructura de los DTOs sin afectar directamente a las capas que los utilizan.

4. **Flexibilidad:** Los DTOs pueden contener datos de múltiples entidades o fuentes, lo que permite consolidar la información de diferentes lugares en un solo objeto.

Un ejemplo común es un DTO que se utiliza para transferir datos entre el controlador de una aplicación web (capa de presentación) y la capa de servicios. Este DTO podría contener solo los campos relevantes que se mostrarán en la interfaz de usuario, en lugar de toda la entidad de dominio.

En base al siguiente diagrama de clases de un ApiRestFull de una **Universidad** vamos aplicar DTO con **ModlerMapper**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/bbd4d411-1b53-4efa-b320-58e17b5c9db8)


<br><br>

## 1. Dependencias: 

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/b382dd6a-c055-4d22-8261-df8c3fa22ab3)


El proyecto maneja la siguiente estructura basica de paquetes:

 - **controller**: la clase que están expuesta a escuchar las peticiones http, que se denominan controladores. 
 - **services**: Dentro de services se tiene **impl**
 - **repositories**: Dentro de repositories **entities** y/o **documents** si es el caso. Entities se usa para la clases que se mapea con base datos sql y documents para base datos Nosql.  

<br>

## 2. Dependencia de ModelMapper

En el **pom.xml** coloca la dependencia del modelmapper

```xml
    <dependency>
	<groupId>org.modelmapper</groupId>
	<artifactId>modelmapper</artifactId>
	<version>3.1.1</version>
    </dependency>
```
<br>
<br>

## 3. Capa persistencia

En el paquete entities que está dentro de repositores se tiene las siguiente clases: **UniversidadEntity**, **EstudianteEntity** y **MatriculaEntity**. En el siguiente código correspondiente a estas clases entities, se observa las relaciones que hay entre ellas, apartir del diagrama de clases. Universidad y estudiantes con matriculas,  de uno a muchos bidirecional. Se usa esta solución de DTO para evitar serialización loop. 

<br>

**UniversidadEntity**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/0eacb1cc-bd9e-4119-bcf9-315dd879459f)

<details>
<summary>Código</summary>

```java
package com.uts.relation.repositories.entities;

import java.io.Serializable;
import java.util.List;

import jakarta.persistence.CascadeType;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.OneToMany;
import jakarta.persistence.Table;
import lombok.Data;

@Entity
@Table(name="universidad")
@Data
public class UniversidadEntity implements Serializable {
    
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre;
    @OneToMany(mappedBy = "universidad", cascade = CascadeType.ALL, fetch=FetchType.LAZY)
    private List<EstudianteEntity> estudiantes;
    
}

```

</details>

<br>

**EstudianteEntity**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/b59c1c66-8d48-47c0-a1e8-21556539fd0c)

<details>
<summary>Código</summary>

```java
package com.uts.relation.repositories.entities;

import java.io.Serializable;

import jakarta.persistence.CascadeType;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.ManyToOne;
import jakarta.persistence.OneToOne;
import jakarta.persistence.Table;
import lombok.Data;

@Entity
@Table(name="estudiantes")
@Data
public class EstudianteEntity implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String nombre; 

    @OneToOne(mappedBy = "estudiante", cascade = CascadeType.ALL, fetch = FetchType.LAZY) 
    private MatriculaEntity matricula;

    @JoinColumn(name = "universidad_id")    
    @ManyToOne(fetch = FetchType.LAZY)
    private UniversidadEntity universidad;

    
}

```

</details>

<br>


**MatriculaEntity**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/7be39074-4fa8-4c2f-b2fc-b95d18ca4472)


<details>
<summary>Código</summary>

```java

@Entity
@Table(name="matriculas")
@Data
public class MatriculaEntity implements Serializable{
   
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private Double feed;
    @JoinColumn(name="estudainte_id")
    @OneToOne(fetch = FetchType.LAZY)
    private EstudianteEntity estudiante;

    
}

```

</details>

<br>

**EstudianteRepository**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/416daf69-c1ab-45c5-ba65-13d169a82096)


<details>
<summary>Código</summary>

```java

package com.uts.relation.repositories;

import org.springframework.data.repository.CrudRepository;

import com.uts.relation.repositories.entities.EstudianteEntity;

public interface EstudianteRepository extends CrudRepository<EstudianteEntity,Long>{
    
}


```

</details>

<br>

**MatriculaRepository**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/69a84d78-4d7d-4195-a048-d26856e81ae9)


<details>
<summary>Código</summary>

```java

package com.uts.relation.repositories;

import org.springframework.data.repository.CrudRepository;

import com.uts.relation.repositories.entities.MatriculaEntity;

public interface MatriculaRepository extends CrudRepository<MatriculaEntity,Long> {
    
}



```

</details>

<br>

## 4. Clases DTO

La definición de la clases DTO puede ser varias por cada clases entity. El objetivo de esta clases es definir cuales son los datos que se van a manejar tanto para la entrada y salida de nuestro API. Este conjunto de clases, se puede crear en un paquete **dto**.

En este ejemplo son tres los api's que se van a construir:

- Obtener el listado de estudianes
- Obtener la matricula por id
- Crea una matricula

El **Obtener el listado de estudiantes** se requiere obtener solo el Id de la matricula y el Id de la universidad. Si se utiliza el **EstudianteEntity**, se va a utilizar el tipo de dato MatriculaEntity y UniveridadEntity, la cual, a su vez, va carga la información nuevamente de estudiante creandose un loop. Por lo tanto, no es una buena practica. Por eso se propone un EstudianteDTO que sería la información que se va ha utilizar para retornar el listado de estudiante.

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/93844f93-87c5-4507-96b7-f34d5d64f460)


El **Obtener la matricula por id** se requiere obtener una matricula por Id. Si se utilizara **MatriculaEntity** tiene como tipo de dato **EstudianteEntity**, el cual, trae los datos del estudiantes y su relaciones con universidad y matricual, la cual, crea un loop. Por eso se propone **MatriculaDTO**. Este DTO sirver para **crear matricula**

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/08ab130f-a5c0-41d3-a15d-1192b044a489)


### 4.1 EstudianteDTO

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/e519e8f5-9459-44b6-be7a-f19e751df503)


<details>
<summary>Código</summary>

```java
package com.uts.relation.dto;

import lombok.Data;

@Data
public class EstudianteDTO {

    private Long id;
    private String nombre;
    private Long universidadId;
    private Long matriculaId;
    
}



```

</details>


### 4.2 MatriculaDTO

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/fa883c8e-288e-49e3-9d0d-a6f8cbc6b398)


<details>
<summary>Código</summary>

```java

package com.uts.relation.dto;

import lombok.Data;

@Data
public class MatriculaDTO {

   
    private Long id;
    private Double feed;    
    private Long estudianteId;

    
}



```

</details>


### 4.3 UniversidadDTO

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/09fd4ae8-a54b-425c-9abc-f2f364026a17)


<details>
<summary>Código</summary>

```java
package com.uts.relation.dto;

import java.util.List;

import lombok.Data;

@Data
public class UniversidadDTO {

    private Long id;
    private String nombre;
    List<EstudianteDTO> estudiantes;
    
}


```

</details>


## 5. Config 

Creación del **Bean** modelMapper. Se crea un paquete **config** para crear un **Bean** modelMapper.

## 5.1 ModelMapperConfig

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/352da858-87e1-45a7-b279-6cc5094391fa)


<details>
<summary>Código</summary>

```java

package com.uts.relation.config;

import org.modelmapper.ModelMapper;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class ModelMapperConfig {

    @Bean
    public ModelMapper modelMapper(){        
        return new ModelMapper();
    }
    
}

```

</details>

## 5.1 EstudianteDTOConverte

Esta clase convert va tener dos métodos:  **converEstudianteDTO** EstudianteEntity a un EstudianteDTO  y converEstudianteEntity: EstudianteDTO a EstudianteEntity 

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/5136e2c8-f494-48c7-a3df-8174648fc1f6)


<details>
<summary>Código</summary>

```java

package com.uts.relation.config;

import org.modelmapper.ModelMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.uts.relation.dto.EstudianteDTO;
import com.uts.relation.repositories.entities.EstudianteEntity;

@Component
public class EstudianteDTOConverte {

    @Autowired
    private ModelMapper dbm;

    public EstudianteDTO converEstudianteDTO(EstudianteEntity estudiante){

           
                EstudianteDTO estudianteDTO=dbm.map(estudiante,EstudianteDTO.class);
                if(estudiante.getMatricula()!=null){
                  estudianteDTO.setMatriculaId(estudiante.getMatricula().getId());
                }
                estudianteDTO.setUniversidadId(estudiante.getUniversidad().getId());

                return estudianteDTO;
                
    

    }

    public EstudianteEntity converEstudianteEntity(EstudianteDTO estudianteDTO){
          return dbm.map(estudianteDTO,EstudianteEntity.class);
          
    }
    
}


```

</details>

## 5.2 MatriculaDTOConverte

Esta clase convert va tener dos métodos:  **converMatriculaDTO** MatriculaEntity a un MatriculaDTO y **convertMatriculaEntity**: MatriculaEntity a MatriculaDTO

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/a2303c2a-f041-41e8-aaff-2d58d448f349)



<details>
<summary>Código</summary>

```java

package com.uts.relation.config;

import org.modelmapper.ModelMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

import com.uts.relation.dto.MatriculaDTO;
import com.uts.relation.repositories.entities.MatriculaEntity;

@Component
public class MatriculaDTOConverte {

    @Autowired
    private ModelMapper dbm;

    public MatriculaDTO converMatriculaDTO(MatriculaEntity matricula){
        
        MatriculaDTO matriculaDTO=dbm.map(matricula,MatriculaDTO.class);
        matriculaDTO.setEstudianteId(matricula.getId());    
        return matriculaDTO;     

    }

  
    public MatriculaEntity convertMatriculaEntity(MatriculaDTO matriculaDTO){
          return dbm.map(matriculaDTO,MatriculaEntity.class);
    }

    
    
}


```

</details>

<br>

## 6. Capa services

### 6.1 interface MatriculaService

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/cd20a5e0-f360-42ad-bce1-d726149f41fa)


<details>
<summary>Código</summary>

```java

package com.uts.relation.services;

import java.util.List;

import com.uts.relation.dto.MatriculaDTO;
import com.uts.relation.repositories.entities.MatriculaEntity;

public interface MatriculaService {

    MatriculaDTO save(MatriculaDTO matricula);

    List<MatriculaEntity> findAll();
    
}


```

</details>

### 6.2 interface EstudianteService

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/20512f9d-1ef9-40a4-a754-6e916c24d9e3)


<details>
<summary>Código</summary>

```java

package com.uts.relation.services;

import java.util.List;

import com.uts.relation.dto.EstudianteDTO;

public interface EstudianteService {

    List<EstudianteDTO> findAll();
    
}



```

</details>

### 6.3 MatriculaServiceImpl

Se hace inyección de dependencia de **MatriculaDTOConverte** el método save recibe un **MatriculaDTO** en el punto 2 lo convierte un **MatriculaEntity** se guarda en la base datos y luego se convierte nuevamente a **MatriculaDTO** para dar la respuesta. 

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/415ea0d5-1fc1-4921-9aad-52481d6a47f6)

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/d9f1eae8-9ae0-44b8-9517-1519a4beaf5c)

<details>
<summary>Código</summary>

```java

package com.uts.relation.services.impl;

import java.util.List;
import java.util.Optional;

import org.modelmapper.ModelMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import com.uts.relation.config.EstudianteDTOConverte;
import com.uts.relation.config.MatriculaDTOConverte;
import com.uts.relation.dto.EstudianteDTO;
import com.uts.relation.dto.MatriculaDTO;
import com.uts.relation.repositories.EstudianteRepository;
import com.uts.relation.repositories.MatriculaRepository;
import com.uts.relation.repositories.entities.EstudianteEntity;
import com.uts.relation.repositories.entities.MatriculaEntity;
import com.uts.relation.services.MatriculaService;



@Service
public class MatriculaServiceImpl implements MatriculaService {
    
    @Autowired
    private MatriculaRepository matriculaRepository;

    @Autowired EstudianteRepository estudianteRepository;

   @Autowired
    private MatriculaDTOConverte convert;

    
    @Override
    @Transactional
    public MatriculaDTO save(MatriculaDTO matricula) {

        Optional<EstudianteEntity> estuidanteOpintal= estudianteRepository.findById(matricula.getEstudianteId());       

        if(estuidanteOpintal.isPresent()){
           MatriculaEntity matriculaEntity=convert.convertMatriculaEntity(matricula);
           matriculaEntity.setEstudiante(estuidanteOpintal.get());
           matriculaRepository.save(matriculaEntity); 
           return convert.converMatriculaDTO(matriculaEntity);
                  
           
        }
        return null;        
    }

    @Override
    @Transactional(readOnly = true)
    public List<MatriculaDTO> findAll() {
         List<MatriculaEntity> matriculasEntity =(List<MatriculaEntity>) matriculaRepository.findAll();
         return matriculasEntity.stream()
                                .map(matricula->convert.converMatriculaDTO(matricula))
                                .toList();
         
    }
    
}



```

</details>


### 6.3 EstudianteServiceImpl

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/af6227ec-f951-4483-96a8-feffc8fde347)


<details>
<summary>Código</summary>

```java

package com.uts.relation.services.impl;

import java.util.ArrayList;
import java.util.List;

import org.modelmapper.ModelMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.uts.relation.config.EstudianteDTOConverte;
import com.uts.relation.dto.EstudianteDTO;
import com.uts.relation.dto.MatriculaDTO;
import com.uts.relation.dto.UniversidadDTO;
import com.uts.relation.repositories.EstudianteRepository;
import com.uts.relation.repositories.entities.EstudianteEntity;
import com.uts.relation.repositories.entities.MatriculaEntity;
import com.uts.relation.repositories.entities.UniversidadEntity;
import com.uts.relation.services.EstudianteService;

import jakarta.transaction.Transactional;

@Service
public class EstudianteServiceImpl  implements EstudianteService{

    @Autowired
    private EstudianteRepository estudianteRepository;

    @Autowired
    private EstudianteDTOConverte convert;


    @Override
    @Transactional
    public List<EstudianteDTO> findAll() {
        List<EstudianteEntity> estudiantesEntity= (List<EstudianteEntity>) estudianteRepository.findAll();
        List<EstudianteDTO> estudiantesDTO=new ArrayList<>();       

           for(EstudianteEntity  estudiante  :estudiantesEntity){
                estudiantesDTO.add(convert.converEstudianteDTO(estudiante));
          }
          return estudiantesDTO;

        
       
    }
    
}



```

</details>

<br>

## 7. Controllers

### 7.1 MatriculaController

Los api's obtener el listado de matricula y  guardar una matricula, no exponen a **MatriculaEntity*** y lo hacen a través el **DTO**, los cuales, se adpanta a las necesidades de la información que se quiere usar como entrada y salida. 

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/813faa00-4248-496a-a655-0694166edee3)


<details>
<summary>Código</summary>

```java

package com.uts.relation.controllers;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.uts.relation.dto.MatriculaDTO;
import com.uts.relation.services.MatriculaService;

@RestController
@RequestMapping("/matriculas")
public class MatriculaController {
      
      @Autowired
      private MatriculaService matriculaService;    


      @GetMapping("/")
      public List<MatriculaDTO> findAll(){
         return matriculaService.findAll();
      }


      @PostMapping("/")
      public MatriculaDTO save(@RequestBody MatriculaDTO matricula){
           return matriculaService.save(matricula);

      }

    
}


```

</details>

### 7.1 EstudianteController

![image](https://github.com/crodrigr/webservice-uts-2023-02/assets/31961588/0b467b86-bf80-47bb-a020-fa7aa8567477)


<details>
<summary>Código</summary>

```java

package com.uts.relation.controllers;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.uts.relation.dto.EstudianteDTO;
import com.uts.relation.services.EstudianteService;

@RestController
@RequestMapping("/estudiantes")
public class EstudianteController {

    @Autowired
    private EstudianteService estudianteService;


    @GetMapping("/")
    public List<EstudianteDTO> findAll(){
        return estudianteService.findAll();
    }
    
}



```

</details>


