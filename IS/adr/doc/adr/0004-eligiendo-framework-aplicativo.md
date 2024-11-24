# 0004: Eligiendo Framework Aplicativo

* Status: Proposed
* Deciders:
  * [Domingo Suarez Torres](domingo@circulosiete.com)
  * [Carlos Ramos Montoya](ramos.montoya.carlos@gmail.com)
* Date: 2024-11-23

## Context and Problem Statement

Para el desarrollo de **C7 E-Commerce**, se ve la necesidad de contar con un framework que facilite la implementación de una arquitectura limpia y ofrezca soporte para diversos protocolos de comunicación:

* **HTTP:** Para comunicación REST.
* **gRPC:** Para servicios internos de alto rendimiento.  
* **Mensajería:**
  * AMQP (RabbitMQ)
  * Kafka

## Decision Drivers

* Sea ampliamente adoptado.
* Cuente con una comunidad activa.
* Cuente con una aplica documentación.

## Considered Options

* Spring Framework
* Quarkus
* Micronaut
* Dropwizard

## Decision Outcome

Se ha decidido utilizar **Spring Framework** como framework aplicativo para desarrollar la **C7 E-Commerce**.

Spring Framework proporciona un conjunto de herramientas (Spring Boot) robustas y preconfiguradas que permiten desarrollar rápidamente aplicaciones basadas en Java, alineándose perfectamente con los principios de la arquitectura limpia y soportando los protocolos requeridos.

### Positive Consequences

* :heavy_check_mark: Productividad acelerada gracias a las herramientas preconfiguradas

* :heavy_check_mark: Soporte integrado para múltiples protocolos.

* :heavy_check_mark: Alineación con los principios de la arquitectura limpia.

* :heavy_check_mark: Reducción del tiempo de desarrollo inicial.
* :heavy_check_mark: Facilidad de integración con sistemas externos.  
* :heavy_check_mark: Comunidad activa que asegura soporte y actualizaciones frecuentes.  

### Negative Consequences

* :x: Curva de aprendizaje inicial para desarrolladores que no estén familiarizados con Spring.
* :x: La configuración y uso de gRPC puede requerir bibliotecas adicionales, ya que no está soportado de manera nativa por el core de Spring.
* :x: Tiempo de arranque de la aplicación.
* :x: Uso de recursos ligeramente superiores comparado con alternativas como Quarkus o Micronaut.

## Pros and Cons of the Options

### Quarkus

* :heavy_check_mark: Arranque rápido y bajo consumo de memoria.  
* :x: Comunidad más pequeña en comparación con Spring Framework.
* :x: Menor integración nativa con herramientas como Kafka o RabbitMQ.

### Micronaut

* :heavy_check_mark: Buen soporte para microservicios y bajo overhead.  
* :x: Menor flexibilidad para proyectos de gran escala.
* :x: Menos ejemplos de implementación para gRPC.

### Dropwizard

* :heavy_check_mark: Simplicidad y ligereza.  
* :x: Enfoque principal en REST.
* :x: Doporte limitado para otros protocolos como Kafka o gRPC.

## Links

* [Spring Framework](https://docs.spring.io/spring-framework/reference/index.html)
* [Spring Boot](https://docs.spring.io/spring-boot/index.html)
