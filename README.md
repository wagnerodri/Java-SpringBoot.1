# Java-SpringBoot.1

# Projeto web services com Spring Boot e JPA / Hibernate 

[![NPM](https://img.shields.io/npm/l/react)](https://github.com/wagnerodri/Java-SpringBoot.1/blob/main/LICENSE)

# Objetivos 
 Criar projeto Spring Boot Java 
 Implementar modelo de domínio 
 Estruturar camadas lógicas: resource, service, repository 
 Configurar banco de dados de teste (H2) 
 Povoar o banco de dados 
 CRUD - Create, Retrieve, Update, Delete 
 Tratamento de exceções 

# Layout 
![1.PGN](https://github.com/wagnerodri/Java-SpringBoot.1/blob/main/1.PNG)

# Domian Model

![2.PGN](https://github.com/wagnerodri/Java-SpringBoot.1/blob/main/2..PNG)

# Domian Instance

![3.PGN](https://github.com/wagnerodri/Java-SpringBoot.1/blob/main/3..PNG)

# Layout Layers

![4.PGN](https://github.com/wagnerodri/Java-SpringBoot.1/blob/main/4..PNG)

# Project created 

# Checklist: 
 Spring Initializr 
o Maven 
o Java 17 
o Packing JAR 
o Dependencies: Spring Web

# User entity and resource 

# Basic entity checklist: 
 Basic attributes 
 Associations (instantiate collections) 
 Constructors 
 Getters & Setters (collections: only get) 
 hashCode & equals 
 Serializable 
H2 database, test profile, JPA 

# Checklist: 

 JPA & H2 dependencies 
 application.properties 
 application-test.properties 
 Entity: JPA mapping

# Dependencies: 

<dependency> 
<groupId>org.springframework.boot</groupId> 
<artifactId>spring-boot-starter-data-jpa</artifactId> 
</dependency> 
<dependency> 
<groupId>com.h2database</groupId> 
<artifactId>h2</artifactId> 
<scope>runtime</scope> 
</dependency> 

# application.properties: 

spring.profiles.active=test 
spring.jpa.open-in-view=true 

# application-test.properties:

# DATASOURCE 
spring.datasource.driverClassName=org.h2.Driver 
spring.datasource.url=jdbc:h2:mem:testdb 
spring.datasource.username=sa 
spring.datasource.password= 
# H2 CLIENT 
spring.h2.console.enabled=true 
spring.h2.console.path=/h2-console 
# JPA, SQL 
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect 
spring.jpa.defer-datasource-initialization=true 
spring.jpa.show-sql=true 
spring.jpa.properties.hibernate.format_sql=true

# JPA repository, dependency injection, database seeding  

# Checklist: 
 UserRepository extends JPARepository<User, Long> 
 Configuration class for "test" profile 
 @Autowired UserRepository 
 Instantiate objects in memory 
 Persist objects 


# Objects: 
User u1 = new User(null, "Maria Brown", "maria@gmail.com", "988888888", "123456"); 
User u2 = new User(null, "Alex Green", "alex@gmail.com", "977777777", "123456");

# Service layer, component registration 
 # Order, Instant, ISO 8601 

# Basic new entity checklist: 
 Entity 
o "To many" association, lazy loading, JsonIgnore 
 Repository 
 Seed 
 Service 
 Resource 
# Objects: 
Order o1 = new Order(null, Instant.parse("2019-06-20T19:53:07Z"), u1); 
Order o2 = new Order(null, Instant.parse("2019-07-21T03:42:10Z"), u2); 
Order o3 = new Order(null, Instant.parse("2019-07-22T15:21:22Z"), u1); 

# OrderStatus enum 

# Category 

# Objects: 
Category cat1 = new Category(null, "Electronics"); 
Category cat2 = new Category(null, "Books"); 
Category cat3 = new Category(null, "Computers"); 

# Product 
# Objects: 
Product p1 = new Product(null, "The Lord of the Rings", "Lorem ipsum dolor sit amet, consectetur.", 90.5, ""); 
Product p2 = new Product(null, "Smart TV", "Nulla eu imperdiet purus. Maecenas ante.", 2190.0, ""); 
Product p3 = new Product(null, "Macbook Pro", "Nam eleifend maximus tortor, at mollis.", 1250.0, ""); 
Product p4 = new Product(null, "PC Gamer", "Donec aliquet odio ac rhoncus cursus.", 1200.0, ""); 
Product p5 = new Product(null, "Rails for Dummies", "Cras fringilla convallis sem vel faucibus.", 100.99, "");



# Many-to-many association with JoinTable 
# OrderItem, many-to-many association with extra attributes 


# Checklist: 
 OrderItemPK 
 OrderItem 
 Order one-to-many association 
 Seed 
# Objects: 
OrderItem oi1 = new OrderItem(o1, p1, 2, p1.getPrice()); 
OrderItem oi2 = new OrderItem(o1, p3, 1, p3.getPrice()); 
OrderItem oi3 = new OrderItem(o2, p3, 2, p3.getPrice()); 
OrderItem oi4 = new OrderItem(o3, p5, 2, p5.getPrice());


Product-OrderItem one-to-many association 
Payment, one-to-one association 
Subtotal & Total methods 

# User insert 
# Checklist: 
 UserService 
 UserResource 
 
# Test: 
{ 
    "name": "Bob Brown", 
    "email": "bob@gmail.com", 
    "phone": "977557755", 
    "password": "123456" 
} 
 
User delete 
 
# Checklist: 
 UserService 
 UserResource 
 
 
User update 
 
Checklist: 
 UserService 
 UserResource 
 
# Test: 
{ 
    "name": "Bob Brown", 
    "email": "bob@gmail.com", 
    "phone": "977557755" 
} 
 
# Exception handling - findById 
 
# Checklist: 
 NEW CLASS: services.exceptions.ResourceNotFoundException 
 NEW CLASS: resources.exceptions.StandardError 
 NEW CLASS: resources.exceptions.ResourceExceptionHandler 
 UserService


Exception handling - delete 

# Checklist: 
 NEW CLASS: services.exceptions.DatabaseException 
 ResourceExceptionHandler 
 UserService 
o EmptyResultDataAccessException 
o DataIntegrityViolationException 

# Exception handling - update 

# Checklist: 
 UserService 
o EntityNotFoundException 
