# Spring Securiyt

<br>
<br>
<br>

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/31a02210-3c5f-4c1b-a55f-60033a4f4fba)

<br>
<br>
<br>

## 1 Authorization Server

<br>

En el contexto de Spring Boot y la seguridad de aplicaciones web, un "Authorization Server" (Servidor de Autorización) es un componente que se encarga de emitir tokens de acceso y validar las solicitudes de autorización realizadas por aplicaciones cliente. Este servidor juega un papel crucial en la implementación del flujo de OAuth 2.0, un protocolo de autorización ampliamente utilizado para proteger recursos y permitir que las aplicaciones accedan a ellos en nombre de los usuarios.

El Authorization Server es responsable de autenticar a los usuarios y de emitir tokens de acceso (tokens de acceso OAuth 2.0) que representan los derechos de acceso del usuario a recursos protegidos. Estos tokens de acceso son utilizados por las aplicaciones cliente para acceder a recursos protegidos en nombre del usuario autenticado, sin que las aplicaciones tengan que solicitar las credenciales del usuario en cada solicitud.

En una arquitectura típica de OAuth 2.0, el Authorization Server trabaja junto con otros componentes clave, como:

1. **Resource Server (Servidor de Recursos)**: Es el servidor que almacena y protege los recursos a los que se accede mediante tokens de acceso. El Resource Server utiliza el token de acceso para validar las solicitudes de las aplicaciones cliente y proporcionar acceso a los recursos solicitados si el token es válido y autorizado.

2. **Client Application (Aplicación Cliente)**: Es la aplicación que solicita el acceso a los recursos protegidos en nombre del usuario. La aplicación cliente obtiene el token de acceso del Authorization Server y lo envía junto con las solicitudes al Resource Server para acceder a los recursos.

En el ecosistema de Spring Boot, puedes implementar un Authorization Server utilizando Spring Security OAuth 2.0, que proporciona una amplia gama de características y opciones para gestionar la seguridad y la autorización en tu aplicación. Spring Security OAuth 2.0 facilita la configuración de un Authorization Server personalizado y te permite controlar el proceso de emisión y validación de tokens de acceso.

Es importante entender que la implementación de un Authorization Server debe realizarse con especial cuidado, ya que la seguridad y la protección de los recursos de los usuarios dependen de su correcto funcionamiento y configuración. Por lo tanto, siempre es recomendable seguir las mejores prácticas de seguridad y utilizar bibliotecas y herramientas probadas para asegurar la robustez de tu Authorization Server y tu aplicación en general.

<br>
<br>
<br>

## 2. Resource Server

<br>

En el contexto de seguridad de aplicaciones web y OAuth 2.0, un "Resource Server" (Servidor de Recursos) es el componente que almacena y protege los recursos a los que se accede mediante tokens de acceso emitidos por el Authorization Server (Servidor de Autorización).

En el flujo de OAuth 2.0, una vez que un usuario ha sido autenticado y autorizado por el Authorization Server, este emite un token de acceso al cliente (aplicación cliente). El cliente utiliza este token de acceso para acceder a los recursos protegidos en nombre del usuario en el Resource Server.

El Resource Server tiene la responsabilidad de validar el token de acceso recibido de la aplicación cliente y, si el token es válido y autorizado, permitir el acceso a los recursos solicitados. Los recursos pueden ser datos, servicios o cualquier otra información protegida que el usuario haya permitido que la aplicación cliente acceda.

El Resource Server debe asegurarse de que el token de acceso es válido, no ha caducado y que la aplicación cliente tiene los permisos adecuados para acceder a los recursos solicitados. Además, puede aplicar políticas de autorización adicionales para determinar si el cliente tiene el derecho de acceder a recursos específicos.

En una arquitectura típica de OAuth 2.0, el Resource Server trabaja junto con otros componentes clave, como:

1. **Authorization Server (Servidor de Autorización)**: Es el servidor que emite los tokens de acceso después de autenticar y autorizar al usuario. El Authorization Server y el Resource Server pueden ser el mismo servidor en algunos casos.

2. **Client Application (Aplicación Cliente)**: Es la aplicación que solicita el acceso a los recursos protegidos en nombre del usuario. La aplicación cliente obtiene el token de acceso del Authorization Server y lo envía junto con las solicitudes al Resource Server para acceder a los recursos.

El Resource Server juega un papel importante en la implementación de la seguridad y la protección de recursos en aplicaciones distribuidas y sistemas que utilizan el protocolo OAuth 2.0 para gestionar el acceso a recursos protegidos. Al validar los tokens de acceso y aplicar políticas de autorización, el Resource Server garantiza que solo las aplicaciones autorizadas y autenticadas pueden acceder a los datos y servicios protegidos.

<br>
<br>
<br>

## 3. Proceso autenticación

<br>

Detalle del proyeceso de autenticación. Lo que ocurre detras de escena. 

### 3.1 Authorization Server

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/39af06cd-95cf-4fe8-9426-c4b42bbfd87a)

<br>

### 3.2 Resource Server

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/28fc066f-8fb1-4e8b-96f4-81777310ea14)


## 4. Dependencias

<br>

### 4.1 Version spring

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/ecea92f4-f36c-458d-bc81-cfd176d379bf)


<br>

### 4.2 Dependencias oauth

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/54639980-270a-41d3-8370-4b2fc25c663f)


<br>

### 4.3 Jakarta a javax

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/10f2fe27-16ce-4eea-a0ff-5879e14a1e48)

<br>

<details><summary>Mostrar código</summary>

<p>   
    
```xml

<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.5.6</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.demo</groupId>
	<artifactId>demo</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>demo</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>17</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>	      
		<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
       <dependency>
        <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
       </dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-validation</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.security.oauth</groupId>
			<artifactId>spring-security-oauth2</artifactId>
			<version>2.3.4.RELEASE</version>
		</dependency>
			<dependency>
			<groupId>org.springframework.security</groupId>
			<artifactId>spring-security-jwt</artifactId>
			<version>1.0.9.RELEASE</version>
		</dependency>
		<dependency>
			<groupId>javax.xml.bind</groupId>
			<artifactId>jaxb-api</artifactId>
		</dependency>
		<dependency>
			<groupId>org.glassfish.jaxb</groupId>
			<artifactId>jaxb-runtime</artifactId>
		</dependency>		
		
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>


```

</p>
</details>

<br>
<br>
<br>

## 5. Usuario 

### 5.1 UsuarioService 

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/ad57fc04-f86b-490d-82a3-70617b2545bc)

<details><summary>Mostrar código</summary>

<p>   
    
```java

package com.demo.demo.services;

import com.demo.demo.repository.entities.Usuario;

public interface UsuarioService {

    
	public Usuario findByUsername(String username);
	
	public void delete(Usuario Usuario);


}


```

</p>
</details>

<br>

### 5.2 UsuarioRepository

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/5f16822c-a2d6-435e-88c5-6ff0fc2e9fb9)


<details><summary>Mostrar código</summary>

<p>   
    
```java
package com.demo.demo.repository;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;

import com.demo.demo.repository.entities.Usuario;

public interface UsuarioRepository  extends CrudRepository<Usuario,Long> {

    public Usuario findByUsername(String username);
	
	@Query("select u from Usuario u where u.username=?1")	
	public Usuario findByUsername2(String username);
    
}


```

</p>
</details>

<br>

### 5.3 UsuarioServiceImpl

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/3aafa639-d97a-4bcb-bae9-cc44ff8a6b8a)


<details><summary>Mostrar código</summary>

<p>   
    
```java

package com.demo.demo.services.impl;

import java.util.List;
import java.util.stream.Collectors;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;
import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;

import com.demo.demo.repository.UsuarioRepository;
import com.demo.demo.repository.entities.Usuario;
import com.demo.demo.services.UsuarioService;

@Service
public class UsuarioServiceImpl implements UsuarioService, UserDetailsService {
	
	private Logger logger = LoggerFactory.getLogger(UsuarioServiceImpl.class);

	@Autowired
	private UsuarioRepository usuarioDao;
	
	@Override
	@Transactional(readOnly=true)
	public Usuario findByUsername(String username) {
		return usuarioDao.findByUsername(username);
	}
	@Override
	@Transactional
	public void delete(Usuario usuario) {
		usuarioDao.delete(usuario);
		
	}

	@Override
	@Transactional(readOnly=true)
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
		
		Usuario usuario=usuarioDao.findByUsername(username);
		
		if(usuario==null){
		  logger.error("Error en el login: no existe el usuario "+username+" en el sistema!");
		  throw new UsernameNotFoundException("Error en el login: no existe el usuario " +username+ " en el sistema!");
		}
		
		List<GrantedAuthority> authorities = usuario.getRoles()
				.stream()
				.map(role-> new SimpleGrantedAuthority(role.getNombre()))
				.peek(authority-> logger.info("Role: "+authority.getAuthority()))
				.collect(Collectors.toList());
		
		return new User(usuario.getUsername(),usuario.getPassword(),usuario.getEnabled(),true,true,true,authorities);
		
		
	}

}

```

</p>
</details>

El código que proporcionaste es una implementación del método `loadUserByUsername` de una clase de servicio en Spring Boot que implementa la interfaz `UserDetailsService`. Este método se utiliza para cargar los detalles del usuario durante el proceso de autenticación en Spring Security. Vamos a revisar cada parte del código:

1. **Método `loadUserByUsername`**: Este método se anota con `@Override`, lo que indica que está sobrescribiendo el método de la interfaz `UserDetailsService`.

2. **Buscar el usuario en el repositorio**: Se utiliza el `usuarioRepository` para buscar un usuario en la base de datos a partir del nombre de usuario proporcionado.

3. **Comprobación de existencia del usuario**: Si no se encuentra ningún usuario con el nombre de usuario proporcionado, se lanza una excepción `UsernameNotFoundException`. Esto ocurre cuando un usuario intenta autenticarse con un nombre de usuario que no existe en el sistema.

4. **Mapeo de roles a authorities**: Si el usuario es encontrado en la base de datos, se procede a obtener sus roles y mapearlos a objetos `GrantedAuthority`. Cada rol del usuario se transforma en un `SimpleGrantedAuthority` y se agrega a una lista de `authorities`. Los `GrantedAuthority` representan los permisos o roles que un usuario tiene en el sistema y se utilizan para controlar el acceso a recursos y funcionalidades.

5. **Logging**: Se utilizan registros (logs) para registrar información relevante sobre los roles del usuario. Cada rol se registra utilizando el `logger`.

6. **Creación del objeto `User`**: Finalmente, se crea un objeto `User` que implementa la interfaz `UserDetails`, que representa al usuario autenticado. Se utilizan varios atributos del usuario, como el nombre de usuario, contraseña, estado de cuenta y la lista de `authorities` (roles), para construir el objeto `User`.

7. **Retorno del objeto `User`**: El objeto `User` construido se devuelve como resultado del método. Es utilizado por Spring Security para llevar a cabo el proceso de autenticación y autorización.

En resumen, este método carga los detalles del usuario durante el proceso de autenticación y devuelve un objeto `User` que representa al usuario autenticado, incluyendo sus roles que se utilizarán para controlar el acceso en la aplicación protegida por Spring Security.  `usuarioRepository` representa un componente de acceso a datos (un repositorio) que se utiliza para interactuar con la base de datos y obtener la información del usuario.

<br>

## 6. Oauth

<br>

### 6.1 InfoAdicionalToken


Este código muestra una clase llamada `InfoAdicionalToken`, que implementa la interfaz `TokenEnhancer` en una aplicación Spring Boot. La función de esta clase es mejorar el token de acceso OAuth2 al agregar información adicional al mismo antes de ser devuelto al cliente que lo solicitó. Aquí está una explicación detallada de cada parte del código:

1. **Anotación `@Component`**: Esta anotación indica que la clase es un componente de Spring y será escaneada y administrada por el contenedor de Spring.

2. **Inyección de Dependencia**: La clase utiliza la anotación `@Autowired` para inyectar una instancia de `IUsuarioService`, que representa un servicio que interactúa con la entidad `Usuario`. Esto permite que la clase acceda al servicio `usuarioService` para obtener información adicional sobre el usuario que está solicitando el token.

3. **Método `enhance`**: Esta es la implementación del método `enhance` de la interfaz `TokenEnhancer`. Este método se llama durante el proceso de emisión de tokens de acceso OAuth2 para mejorar el token antes de que se devuelva al cliente.

4. **Obtención de información adicional sobre el usuario**: Dentro del método `enhance`, se utiliza el objeto `authentication` para obtener el nombre de usuario (el identificador del usuario) que está solicitando el token. Luego, se utiliza el servicio `usuarioService` para buscar al usuario en la base de datos utilizando el nombre de usuario.

5. **Creación de información adicional**: Se crea un mapa llamado `info`, que contiene información adicional que se agregará al token. En este caso, se agrega un mensaje de saludo personalizado con el nombre de usuario, así como el nombre, apellido y email del usuario que se obtuvo de la base de datos.

6. **Establecimiento de información adicional en el token**: La información adicional creada en el mapa `info` se establece en el token de acceso OAuth2 utilizando el método `setAdditionalInformation` de `DefaultOAuth2AccessToken`, que es una implementación de `OAuth2AccessToken`.

7. **Retorno del token mejorado**: Finalmente, el token de acceso OAuth2 con la información adicional se devuelve al cliente que lo solicitó.

En resumen, esta clase `InfoAdicionalToken` actúa como un mejorador de tokens de acceso OAuth2 al agregar información adicional al token antes de que sea devuelto al cliente. Esto permite personalizar el token con información específica del usuario, lo que puede ser útil para ciertos casos de uso en la aplicación.

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/55223daf-0a22-4ff7-bf2d-853aa0d95b0b)

<details><summary>Mostrar código</summary>

<p>  

```java

package com.demo.demo.auth;

import java.util.HashMap;
import java.util.Map;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.oauth2.common.DefaultOAuth2AccessToken;
import org.springframework.security.oauth2.common.OAuth2AccessToken;
import org.springframework.security.oauth2.provider.OAuth2Authentication;
import org.springframework.security.oauth2.provider.token.TokenEnhancer;
import org.springframework.stereotype.Component;

import com.demo.demo.repository.entities.Usuario;
import com.demo.demo.services.UsuarioService;

@Component
public class InfoAdicionalToken implements TokenEnhancer {
	
	@Autowired
	private UsuarioService usuarioService;

	@Override
	public OAuth2AccessToken enhance(OAuth2AccessToken accessToken, OAuth2Authentication authentication) {
		
		Usuario usuario=usuarioService.findByUsername(authentication.getName());
		
		Map<String,Object> info = new HashMap<>();
		info.put("info_adicional", "Hola que tal! : ".concat(authentication.getName()));
		info.put("nombre",usuario.getNombre());
		info.put("apellido",usuario.getApellido());
		info.put("email",usuario.getEmail());

		((DefaultOAuth2AccessToken) accessToken).setAdditionalInformation(info);		
			
		return accessToken;
	}
	
	
	

}


```

</p>
</details>

<br>

### 6.2 JwtConfig

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/6124aec3-4d43-4c56-a02c-26e7c683ab08)

<details><summary>Mostrar código</summary>

<p>   
    
```java

package com.demo.demo.auth;

public class JwtConfig {

    public static final String LLAVE_SECRETA="alguna.clave.secreta.322929292";
    
}



```

</p>
</details>

<br>

### 6.3 ResourceServerConfig

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/10dd152b-bb68-4348-b915-04dcdb6820e1)


Este código muestra una configuración de un servidor de recursos (Resource Server) en una aplicación Spring Boot con Spring Security. El servidor de recursos es responsable de proteger y controlar el acceso a los recursos (endpoints/APIs) de la aplicación. A continuación, se explica cada parte del código:

1. **Anotaciones `@Configuration` y `@EnableResourceServer`**: La clase está anotada con `@Configuration`, lo que indica que es una clase de configuración de Spring, y con `@EnableResourceServer`, lo que habilita la funcionalidad de servidor de recursos en la aplicación. El servidor de recursos es una característica de Spring Security que protege y autentica las solicitudes de recursos.

2. **Método `configure(HttpSecurity http)`**: Este método sobrescrito se utiliza para configurar la seguridad del servidor de recursos. Aquí, se define cómo se deben proteger los endpoints/APIs de la aplicación. En este caso:

   - El endpoint `/api/clientes` con el método HTTP GET se configura para permitir el acceso a todos, lo que significa que es de acceso público sin requerir autenticación. Esto se hace utilizando el método `permitAll()` para el método GET específico.
   - Para cualquier otra solicitud (otros endpoints y métodos HTTP), se requiere autenticación para acceder. Esto se establece con el método `authenticated()`.

3. **Método `corsConfigurationSource()`**: Este método define la configuración CORS (Cross-Origin Resource Sharing) que permite solicitudes desde el origen `http://localhost:4200`. CORS es necesario cuando la aplicación del cliente se ejecuta en un dominio diferente al del servidor.

4. **Configuración de CORS**: En el método `corsConfigurationSource()`, se crea un objeto `CorsConfiguration` y se establecen las reglas de CORS:

   - `setAllowedOrigins`: Se establece el origen permitido para las solicitudes. En este caso, se permite `http://localhost:4200`, lo que significa que las solicitudes desde este origen se aceptarán.
   - `setAllowedMethods`: Se definen los métodos HTTP permitidos. Aquí, se permiten GET, POST, PUT, DELETE y OPTIONS.
   - `setAllowCredentials`: Se habilita el envío de credenciales (cookies, encabezados de autorización) en la solicitud CORS.
   - `setAllowedHeaders`: Se definen los encabezados permitidos en la solicitud CORS.

5. **Configuración del filtro CORS**: Se crea un bean de tipo `FilterRegistrationBean<CorsFilter>` que registra el filtro CORS con la configuración CORS definida en el método `corsConfigurationSource()`. Este filtro se asegura de que las solicitudes CORS sean manejadas correctamente.

6. **Orden del filtro CORS**: Se establece el orden del filtro CORS con el método `setOrder()`, para asegurar que este filtro se aplique antes que otros filtros de seguridad.

En resumen, esta clase `ResourceServerConfig` configura la seguridad para proteger los recursos/APIs en la aplicación utilizando Spring Security. Se permite el acceso público al endpoint `/api/clientes` con el método GET, y para otros endpoints y métodos HTTP, se requiere autenticación. Además, se habilita y configura CORS para permitir solicitudes desde `http://localhost:4200`, que es el origen de la aplicación del cliente.

<details><summary>Mostrar código</summary>

<p>   
    
```java

@Configuration
@EnableResourceServer
public class ResourceServerConfig extends ResourceServerConfigurerAdapter {

    @Override
	public void configure(HttpSecurity http) throws Exception {
		http.authorizeRequests().antMatchers(HttpMethod.GET,"/api/clientes").permitAll()
		.anyRequest().authenticated()
		.and().cors().configurationSource(corsConfigurationSource());
			
		
	}

	@Bean
	public CorsConfigurationSource corsConfigurationSource() {
		CorsConfiguration config = new CorsConfiguration();
		config.setAllowedOrigins(Arrays.asList("http://localhost:4200"));
		config.setAllowedMethods(Arrays.asList("GET", "POST", "PUT", "DELETE", "OPTIONS"));
		config.setAllowCredentials(true);
		config.setAllowedHeaders(Arrays.asList("Content-Type", "Authorization"));		
		UrlBasedCorsConfigurationSource source = new UrlBasedCorsConfigurationSource();
		source.registerCorsConfiguration("/**", config);
		return source;
	}
	
	
	@Bean
	public FilterRegistrationBean<CorsFilter> corsFilter(){
		FilterRegistrationBean<CorsFilter> bean = new FilterRegistrationBean<CorsFilter>(new CorsFilter(corsConfigurationSource()));
		bean.setOrder(Ordered.HIGHEST_PRECEDENCE);
		return bean;
	}
	
    
}


```

</p>
</details>

<br>

### 6.4 SpringSecurityConfig

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/7eac8ddb-f1b8-4082-b515-cbf7981cf550)


Este código muestra una clase de configuración de seguridad para una aplicación Spring Boot con Spring Security habilitado para proteger los métodos (global method security). A continuación, se explica cada parte del código:

1. **Anotación `@EnableGlobalMethodSecurity(securedEnabled=true)`**: Esta anotación habilita la seguridad a nivel de método en la aplicación. Permite el uso de anotaciones como `@Secured`, `@PreAuthorize`, `@PostAuthorize`, etc., para definir los permisos necesarios para acceder a métodos específicos.

2. **Clase de Configuración `SpringSecurityConfig`**: Esta clase es una configuración personalizada de Spring Security que extiende de `WebSecurityConfigurerAdapter`. Con esta clase, puedes personalizar la seguridad de tu aplicación.

3. **Inyección de Dependencia**: Se inyecta una implementación de `UserDetailsService`, que generalmente es proporcionada por el desarrollador para manejar la autenticación y carga de detalles de usuario durante el proceso de inicio de sesión.

4. **Bean `BCryptPasswordEncoder`**: Se define un bean llamado `passwordEncoder` que devuelve una instancia de `BCryptPasswordEncoder`. Esta es una clase proporcionada por Spring Security que se utiliza para codificar contraseñas utilizando el algoritmo BCrypt.

5. **Método `configure(AuthenticationManagerBuilder auth)`**: Se sobrescribe este método para configurar la autenticación. Aquí, se utiliza el `UserDetailsService` inyectado (`usuarioService`) y el bean `BCryptPasswordEncoder` para configurar cómo Spring Security autenticará a los usuarios.

<details><summary>Más información</summary>

<p>

El método `configure(AuthenticationManagerBuilder auth)` es un método proporcionado por la clase `WebSecurityConfigurerAdapter` de Spring Security. Este método es utilizado para configurar el `AuthenticationManager`, que es responsable de autenticar a los usuarios en la aplicación.

Cuando defines una clase que extiende `WebSecurityConfigurerAdapter`, puedes sobrescribir el método `configure(AuthenticationManagerBuilder auth)` para personalizar cómo se autentican los usuarios. Dentro de este método, puedes configurar el `AuthenticationManager` con diferentes esquemas de autenticación, como autenticación basada en memoria, autenticación con base de datos, autenticación LDAP, autenticación con proveedores externos y muchos más.

A continuación, se muestra un ejemplo de cómo podrías implementar el método `configure(AuthenticationManagerBuilder auth)`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Autowired
    private UserDetailsService userDetailsService;

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        // Autenticación basada en memoria (para fines de demostración)
        auth.inMemoryAuthentication()
            .withUser("user").password("{noop}password").roles("USER")
            .and()
            .withUser("admin").password("{noop}password").roles("USER", "ADMIN");

        // Autenticación basada en una base de datos (usando un servicio de UserDetailsService)
        auth.userDetailsService(userDetailsService);

        // Otras configuraciones de autenticación también pueden ir aquí, como LDAP, OAuth, etc.
    }

    // Otras configuraciones de seguridad de Spring Security pueden ir aquí...
}
```

En este ejemplo, estamos configurando el `AuthenticationManager` para la autenticación en memoria con dos usuarios: "user" con el rol "USER" y "admin" con los roles "USER" y "ADMIN". También se muestra cómo se puede configurar la autenticación utilizando un servicio de `UserDetailsService`, que es una interfaz proporcionada por Spring Security para cargar detalles de usuario desde una fuente de datos personalizada, como una base de datos.

Es importante tener en cuenta que el formato del hash de contraseña utilizado aquí (`{noop}password`) es para fines de demostración y no es seguro para un entorno de producción. En un entorno real, deberías utilizar un algoritmo de hashing seguro, como BCrypt, para almacenar las contraseñas de los usuarios de manera segura.

En resumen, el método `configure(AuthenticationManagerBuilder auth)` en una clase que extiende `WebSecurityConfigurerAdapter` es utilizado para configurar el `AuthenticationManager`, lo que permite personalizar cómo los usuarios son autenticados en tu aplicación Spring Security.

</p>
</details>

   

6. **Método `authenticationManager()`**: Se sobrescribe este método para exponer el `AuthenticationManager` como un bean en el contexto de Spring. Esto permite que otros componentes de la aplicación accedan al `AuthenticationManager`, por ejemplo, en el proceso de autenticación de usuarios.

7. **Método `configure(HttpSecurity http)`**: Se sobrescribe este método para configurar la autorización. En este caso, se configura para que todas las solicitudes entrantes requieran autenticación (`authenticated()`) y se deshabilita la protección CSRF (`csrf().disable()`). Además, se establece la política de administración de sesiones como STATELESS, lo que significa que no se mantendrán sesiones en el servidor.

En resumen, esta clase `SpringSecurityConfig` configura la seguridad para proteger la aplicación. Los métodos están protegidos con seguridad a nivel de método habilitada mediante la anotación `@EnableGlobalMethodSecurity`, lo que permite utilizar anotaciones como `@Secured`, `@PreAuthorize`, etc., para definir los permisos necesarios para acceder a métodos específicos. La autenticación se maneja utilizando el `UserDetailsService` y las contraseñas se codifican con el algoritmo BCrypt mediante el bean `BCryptPasswordEncoder`. La configuración general de seguridad para las solicitudes HTTP se define en el método `configure(HttpSecurity http)`.


<details><summary>Mostrar código</summary>

<p>   
    
```java

package com.demo.demo.auth;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.config.annotation.authentication.builders.AuthenticationManagerBuilder;
import org.springframework.security.config.annotation.method.configuration.EnableGlobalMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

@EnableGlobalMethodSecurity(securedEnabled=true)
@Configuration
public class SpringSecurityConfig extends WebSecurityConfigurerAdapter {

	@Autowired
	private UserDetailsService usuarioService;
	
	@Bean
	public BCryptPasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder();
	}

	@Override
	@Autowired
	protected void configure(AuthenticationManagerBuilder auth) throws Exception {
		auth.userDetailsService(this.usuarioService).passwordEncoder(passwordEncoder());
	}

	@Bean("authenticationManager")
	@Override
	protected AuthenticationManager authenticationManager() throws Exception {
		return super.authenticationManager();
	}
	
	@Override
	public void configure(HttpSecurity http) throws Exception {
		http.authorizeRequests()
		.anyRequest().authenticated()
		.and()
		.csrf().disable()
		.sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS);
	}

}


```

</p>
</details>

<br>

### 6.5 AuthenticationManager

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/33a1a375-6780-4caf-ad12-11b478393d90)


<details><summary>Mostrar código</summary>

<p>   
    
```java
package com.demo.demo.auth;

import java.util.Arrays;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.oauth2.config.annotation.configurers.ClientDetailsServiceConfigurer;
import org.springframework.security.oauth2.config.annotation.web.configuration.AuthorizationServerConfigurerAdapter;
import org.springframework.security.oauth2.config.annotation.web.configuration.EnableAuthorizationServer;
import org.springframework.security.oauth2.config.annotation.web.configurers.AuthorizationServerEndpointsConfigurer;
import org.springframework.security.oauth2.config.annotation.web.configurers.AuthorizationServerSecurityConfigurer;
import org.springframework.security.oauth2.provider.token.TokenEnhancerChain;
import org.springframework.security.oauth2.provider.token.store.JwtAccessTokenConverter;
import org.springframework.security.oauth2.provider.token.store.JwtTokenStore;

@Configuration
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter{

	@Autowired
	private BCryptPasswordEncoder passwordEncoder;
	
	@Autowired
	@Qualifier("authenticationManager")
	private AuthenticationManager authenticationManager;
	
	@Autowired
	private InfoAdicionalToken infoAdicionalToken;

	@Override
	public void configure(AuthorizationServerSecurityConfigurer security) throws Exception {
		security.tokenKeyAccess("permitAll()")
		.checkTokenAccess("isAuthenticated()");
	}

	@Override
	public void configure(ClientDetailsServiceConfigurer clients) throws Exception {
		clients.inMemory().withClient("frontendapp")
		.secret(passwordEncoder.encode("12345"))
		.scopes("read", "write")
		.authorizedGrantTypes("password", "refresh_token")
		.accessTokenValiditySeconds(3600)
		.refreshTokenValiditySeconds(3600);
	}

	@Override
	public void configure(AuthorizationServerEndpointsConfigurer endpoints) throws Exception {
		TokenEnhancerChain tokenEnhancerChain = new TokenEnhancerChain();
		tokenEnhancerChain.setTokenEnhancers(Arrays.asList(infoAdicionalToken, accessTokenConverter()));
		
		endpoints.authenticationManager(authenticationManager)
		.tokenStore(tokenStore())
		.accessTokenConverter(accessTokenConverter())
		.tokenEnhancer(tokenEnhancerChain);
	}

	@Bean
	public JwtTokenStore tokenStore() {
		return new JwtTokenStore(accessTokenConverter());
	}

	@Bean
	public JwtAccessTokenConverter accessTokenConverter() {
		JwtAccessTokenConverter jwtAccessTokenConverter = new JwtAccessTokenConverter();
		jwtAccessTokenConverter.setSigningKey(JwtConfig.LLAVE_SECRETA);		
		return jwtAccessTokenConverter;
	}
	

}


```

</p>
</details>

Este código muestra una configuración de un servidor de autorización (Authorization Server) en una aplicación Spring Boot con Spring Security y OAuth2 habilitado. El servidor de autorización es responsable de emitir tokens de acceso para que los clientes puedan acceder a los recursos protegidos de la aplicación. A continuación, se explica cada parte del código:

1. **Anotaciones `@Configuration` y `@EnableAuthorizationServer`**: La clase está anotada con `@Configuration`, lo que indica que es una clase de configuración de Spring, y con `@EnableAuthorizationServer`, lo que habilita la funcionalidad de servidor de autorización en la aplicación.

2. **Inyección de Dependencia**: Se inyecta una instancia de `BCryptPasswordEncoder`, que se utilizará para codificar la contraseña del cliente que solicita el token.

3. **Inyección de Dependencia del `AuthenticationManager`**: Se inyecta una instancia de `AuthenticationManager`, que se utilizará para autenticar las solicitudes de los clientes que solicitan el token.

4. **Inyección de Dependencia de `InfoAdicionalToken`**: Se inyecta una instancia de `InfoAdicionalToken`, que es una clase personalizada que extiende `TokenEnhancer` y se utiliza para agregar información adicional al token de acceso.

5. **Método `configure(AuthorizationServerSecurityConfigurer security)`**: Se sobrescribe este método para configurar la seguridad del servidor de autorización. En este caso, se configura para permitir el acceso al endpoint de obtención del token (`/oauth/token`) sin autenticación (`permitAll()`), pero se requiere autenticación para verificar la validez de un token (`/oauth/check_token`).

6. **Método `configure(ClientDetailsServiceConfigurer clients)`**: Se sobrescribe este método para configurar los clientes autorizados que pueden solicitar tokens de acceso. En este caso, se configura un cliente en memoria llamado "angularapp" con una contraseña codificada con `BCryptPasswordEncoder`, y se especifican los alcances (`scopes`) y los tipos de concesión autorizados para ese cliente (`password` y `refresh_token`).

7. **Método `configure(AuthorizationServerEndpointsConfigurer endpoints)`**: Se sobrescribe este método para configurar los puntos finales del servidor de autorización. Aquí, se configura el `AuthenticationManager`, el `TokenStore`, el `AccessTokenConverter` y el `TokenEnhancer`. Se utiliza un `JwtTokenStore` con el `AccessTokenConverter` para almacenar los tokens de acceso como JWT (JSON Web Tokens).

8. **Bean `JwtTokenStore`**: Se define un bean llamado `tokenStore` que devuelve una instancia de `JwtTokenStore`, que es un `TokenStore` que almacena los tokens de acceso como JWT.

9. **Bean `JwtAccessTokenConverter`**: Se define un bean llamado `accessTokenConverter` que devuelve una instancia de `JwtAccessTokenConverter`, que es un `AccessTokenConverter` que se utiliza para convertir los tokens de acceso entre formato JWT y formato normal.

En resumen, esta clase `AuthorizationServerConfig` configura un servidor de autorización OAuth2 con Spring Security. Se especifica cómo se emiten los tokens de acceso, qué clientes están autorizados para solicitar tokens y cómo se manejan los puntos finales para autenticar las solicitudes y emitir los tokens. También se utiliza JWT para almacenar los tokens de acceso y se agrega información adicional al token utilizando la clase `InfoAdicionalToken`.

<br>

### 6.6 Password encriptados

Esto nos va permitir usar BCryptPasswordEncoder para genera password ecriptados para actulizarlo en la tabla de usuario

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/ab0195b4-22a3-46c4-90e0-1b7fe2b00845)

Se actualiza los password de los usuarios que se definieron en el import.sql

![image](https://github.com/crodrigr/spring-boot-angular-confenalco/assets/31961588/367d3dfc-ea75-4b13-bf4e-ff3442f2fd90)



## 7 Validar autorización 

Colocar los decoradores de autorización en los endpoint para que valide con el token y role del usuario

**ClienteController**

```Java
package com.webservice.uts.controllers;

import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

import javax.validation.Valid;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.dao.DataAccessException;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.access.annotation.Secured;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;



import com.webservice.uts.models.services.IClienteService;
import com.webservice.uts.models.entites.Cliente;
import com.webservice.uts.models.entites.Region;



@CrossOrigin(origins = { "http://localhost:4200"})
@RestController
@RequestMapping("/api")
public class ClienteRestController {

	@Autowired
	private IClienteService clienteService;
	
	@GetMapping("/clientes")
	public List<Cliente> index(){
		return clienteService.findAll();	
	}
	
	@Secured({"ROLE_ADMIN","ROLE_USER"})
	@GetMapping("/cliente/{id}")
	public Cliente show(@PathVariable Long id){
		return clienteService.findById(id);
	}
	
	@Secured({"ROLE_ADMIN"})
	@PostMapping("/clientes")
	public ResponseEntity<?> create(@Valid @RequestBody Cliente cliente, BindingResult result){
		
		Cliente clienteNew=null;
		
		Map<String, Object> response=new HashMap<>();
		
		if(result.hasErrors()) {		
			List<String> errors= result.getFieldErrors()
					.stream()
					.map(err -> "El campo " +err.getField() +" "+err.getDefaultMessage())
			        .collect(Collectors.toList());	
		
		response.put("errors",errors);
		 return new ResponseEntity<Map<String,Object>>(response,HttpStatus.BAD_REQUEST);
		
		}
		
		try {
			clienteNew= this.clienteService.save(cliente);
		}catch(DataAccessException e) {
		  response.put("mensaje", "Error al realizar el insert en la base de datos");
		  response.put("error", e.getMessage().concat(": ").concat(e.getMostSpecificCause().getMessage()));	
		  return new ResponseEntity<Map<String,Object>>(response,HttpStatus.INTERNAL_SERVER_ERROR);
		}
		response.put("mensaje","El cliente ha sido creado con éxito!");
		response.put("cliente", clienteNew);
		
		return new ResponseEntity<Map<String,Object>>(response,HttpStatus.CREATED);
		
		
		
		
	}
	
	@Secured({"ROLE_ADMIN"})
	@PutMapping("/cliente/{id}")	
	public ResponseEntity<?> update(@Valid @RequestBody Cliente cliente,BindingResult result,@PathVariable  Long id){
		
		Cliente currentCliente=this.clienteService.findById(id);
		
		Cliente updateCliente=null;
		
        Map<String, Object> response=new HashMap<>();
		
		if(result.hasErrors()) {		
			List<String> errors= result.getFieldErrors()
					.stream()
					.map(err -> "El campo " +err.getField() +" "+err.getDefaultMessage())
			        .collect(Collectors.toList());	
		
		response.put("errors",errors);
		 return new ResponseEntity<Map<String,Object>>(response,HttpStatus.BAD_REQUEST);
		
		}
		
		if(currentCliente==null){
			response.put("mensaje", "Error: no se puede editar, el cliente ID: ".concat(id.toString())
					.concat(" no existe en la base de datos"));
			return new ResponseEntity<Map<String,Object>>(response,HttpStatus.NOT_FOUND);		   
			
		}
		
		try{
			currentCliente.setNombre(cliente.getNombre());
			currentCliente.setApellido(cliente.getApellido());
			currentCliente.setEmail(cliente.getEmail());
			updateCliente=this.clienteService.save(currentCliente);
			
		}catch(DataAccessException e){
			response.put("mensaje", "Error al actulizar en la base de datos");
			response.put("error", e.getMessage().concat(": ").concat(e.getMostSpecificCause().getMessage()));	
			return new ResponseEntity<Map<String,Object>>(response,HttpStatus.INTERNAL_SERVER_ERROR);
			
		}
		response.put("mensaje","El cliente ha sido actulizado con éxito!");
		response.put("cliente", updateCliente);		
		return new ResponseEntity<Map<String,Object>>(response,HttpStatus.CREATED);	
		
	}
	
	@Secured({"ROLE_ADMIN"})
	@DeleteMapping("/clientes/{id}")
	@ResponseStatus(HttpStatus.NO_CONTENT)
	public ResponseEntity<?> delete(@PathVariable Long id){
		
		Map<String, Object> response=new HashMap<>();		
		try {
			
			Cliente cliente=this.clienteService.findById(id);
		    this.clienteService.delete(cliente);
		
		}catch(DataAccessException e){
			 response.put("mensaje", "Error al eliminar el cliente en la base de datos");
			 response.put("error", e.getMessage().concat(": ").concat(e.getMostSpecificCause().getMessage()));	
			 return new ResponseEntity<Map<String,Object>>(response,HttpStatus.INTERNAL_SERVER_ERROR);			
		}
		
		 response.put("mensaje", "El cliente eliminado con éxito");		 
		 return new ResponseEntity<Map<String,Object>>(response,HttpStatus.OK);
		
	}
	
	@Secured("ROLE_ADMIN")
	@GetMapping("/clientes/regiones")
	public List<Region> listarRegiones(){
		return clienteService.findAllRegiones();
	}
	
	
	
}

```

**FacturaController**
```Java
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseStatus;
import org.springframework.web.bind.annotation.RestController;

import com.webservice.uts.models.entites.Factura;
import com.webservice.uts.models.entites.Producto;
import com.webservice.uts.models.services.IClienteService;

import org.springframework.http.HttpStatus;
import org.springframework.security.access.annotation.Secured;



@CrossOrigin(origins = { "http://localhost:4200" })
@RestController
@RequestMapping("/api")
public class FacturaRestController {
	
	@Autowired
	private IClienteService clienteService;
	
	@Secured({"ROLE_ADMIN", "ROLE_USER"})
	@GetMapping("/facturas/{id}")
	@ResponseStatus(HttpStatus.OK)
	public Factura show(@PathVariable Long id) {
		return clienteService.findFacturaById(id);
	}

	
	@Secured({"ROLE_ADMIN", "ROLE_USER"})
	@GetMapping("/facturas")
	@ResponseStatus(HttpStatus.OK)
	public List<Factura> index() {
		return clienteService.findFacturaAll();
	}
	
	@Secured({"ROLE_ADMIN"})
	@DeleteMapping("/facturas/{id}")
	@ResponseStatus(HttpStatus.NO_CONTENT)
	public void delete(@PathVariable Long id) {
		clienteService.deleteFacturaById(id);
	}
	
	@Secured({"ROLE_ADMIN"})
	@GetMapping("/facturas/filtrar-productos/{term}")
	@ResponseStatus(HttpStatus.OK)
	public List<Producto> filtrarProductos(@PathVariable String term){
		return clienteService.findProductoByNombre(term);
	}
	
	@Secured({"ROLE_ADMIN"})
	@PostMapping("/facturas")
	@ResponseStatus(HttpStatus.CREATED)
	public Factura crear(@RequestBody Factura factura) {
		return clienteService.saveFactura(factura);
	}
	
	
	

}


```

## 8 Login postman

![image](https://user-images.githubusercontent.com/31961588/161362171-62837efa-4b60-473a-a078-fb34e5ee4f1f.png)


![image](https://user-images.githubusercontent.com/31961588/161362190-16b51d10-5626-4463-b5f5-4fbd18f2630e.png)


![image](https://user-images.githubusercontent.com/31961588/161362210-baf1fe3b-9a55-4116-84ed-401c08ea68ac.png)

![image](https://user-images.githubusercontent.com/31961588/161362237-e47e29e4-91da-4340-8bc9-a74cb6c54c4e.png)

![image](https://user-images.githubusercontent.com/31961588/161362262-88579de4-5260-4c8f-b6f8-6524ea364d2e.png)

![image](https://user-images.githubusercontent.com/31961588/161362315-9531eac4-d30b-4da4-9e31-46f371eaba06.png)






