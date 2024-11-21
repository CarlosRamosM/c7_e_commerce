# 0002: Eligiendo arquitectura - Estilo de paquetes

* Status: Proposed
* Deciders:
  * [Domingo Suarez Torres](domingo@circulosiete.com)
  * [Carlos Ramos Montoya](ramos.montoya.carlos@gmail.com)
* Date: 2024-11-16

## Context and Problem Statement

Una vez que se acordo el estilo arquitectonico ha utilizar para __C7 E-Commerce__, ahora es necesaria la elección de una diseño de arquitectura (estructura de paquetes), que nos permita como equipo de desarrollo escribir, modificar, mejorar el código fuente que soportará la solución de nuestro software.

## Decision Drivers <!-- optional -->

* __Refleje una clara separación de responsabilidades entre las diversas capas de desarrollo__
* __Partición del modelo de negocio sobre partición técnica__
* __Facilite la ubicación de clases según sus responsabilidades__

## Considered Options

* :books: __MCV__:
  * Estilo modelo vista controlador, separa la lógica de la aplicación de la lógica del modelo de datos (base de datos).
* :ocean: __Clean Architecture__
  * Estructurar aplicaciones de forma que la lógica de negocio esté protegida de los detalles de infraestructura y de implementación, creando una separación clara entre capas.
* :cyclone: __Onion Architecture__
  * Centrada en mantener el dominio central independiente de los detalles externos, aunque la arquitectura limpia a veces incluye una capa adicional de "entidades" puras, fuera del dominio de la aplicación.
* :snowflake: __Hexagonal Architecture__
  * Es un concepto similar con __Clean Architecture__ en cuanto al desacoplamiento de dependencias externas. La diferencia principal es que la arquitectura hexagonal se enfoca más explícitamente en la comunicación a través de puertos (interfaces) con adaptadores para conectarse a las tecnologías externas.

## Decision Outcome

En función de la elección realizada sobre el estilo arquitectonico [(SBA)](/IS/adr/doc/adr/0001-eligiendo-estilo-de-arquitectura.md) de nuestro sistema, se ha llegado al acuerdo que la arquitectura de paquetes que más se ajusta a los objetivos principales en la solución de nuestro sistema es:

* :ocean: __Clean Architecture__

Esto nos ayudara a tener diferentes proyectos que actuaran como modulos del sistema global C7 E-Commerce.

* __Inventory__
* __Orders__
* __Invoice__

Cada uno de los proyectos anteriores podrán ser tomados como unidaddes independientes para su desarrollo y posteriormente despliegue en la infractuctura seleccionada.

Con la elección de __"Clean Architecture"__, podemos organizar los paquetes de los proyectos de la siguiente manera:

>Robert C. Martin: [Clean Code Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

```plaintext
com.c7.ecommerce.(bounded_context)  //bounded_context sera sustituido por el nombre del modulo (inventory, orders, invoice)
│
├── domain            // Núcleo de la lógica de negocio
│   ├── model         // Entidades y objetos de dominio
│   ├── repository    // Interfaces para acceso a datos
│   └── service       // Lógica de dominio compleja (opcional)
│
├── application       // Lógica del dominio de negocio
│   ├── exceptions    // Excepciones custom sobre los casos de uso
│   ├── usecase       // Interfaces funcionales de Casos de uso
|   │   ├── impl      // Implementaciones de casos de uso
│   └── service       // Contratos de integración de servicios en capas externas
│
├── infrastructure    // Implementaciones técnicas (bases de datos, APIs, etc.)
│   ├── repository    // Implementaciones especificas de los repositorios
│   ├── controller    // Controladores REST
│   └── configuration // Configuración técnica (Spring, etc.)
│   └── integration   // Implementaciones especificas con sistemas externos
│

```

### Positive Consequences <!-- optional -->

Agregar nuevas características al proyecto, eliminar o modificar características, validar, corregir errores, probar, manejar errores y entregar el proyecto se vuelven más fáciles con una arquitectura limpia.

* :heavy_check_mark: __Modularidad y mantenibilidad:__
La Arquitectura Limpia promueve la modularidad separando las preocupaciones en distintas capas. Esto hace que el código base sea más fácil de mantener y facilita las actualizaciones o cambios en componentes específicos sin afectar a toda la aplicación.
* :heavy_check_mark: __Comprobabilidad:__
La separación de responsabilidades facilita las pruebas unitarias. La lógica empresarial de la capa central puede probarse independientemente de las dependencias externas, lo que permite realizar pruebas más sólidas y fiables.
* :heavy_check_mark: __Independencia de los marcos:__
La lógica empresarial central no está estrechamente vinculada a marcos de trabajo o bibliotecas específicos. Esta independencia facilita el cambio o la actualización de frameworks sin afectar a la funcionalidad central.
* :heavy_check_mark: __Flexibilidad:__
La Arquitectura Limpia proporciona flexibilidad en la elección de tecnologías para las diferentes capas. Por ejemplo, se puede cambiar entre diferentes frameworks web, bases de datos o frameworks de interfaz de usuario sin grandes cambios en la lógica de negocio central.
* :heavy_check_mark: __Escalabilidad:__
La estructura modular de la Arquitectura Limpia permite una mejor escalabilidad. Es más fácil escalar distintas partes de la aplicación de forma independiente, y los equipos pueden trabajar en capas específicas sin interferir con otras.

### Negative Consequences <!-- optional -->

* :x: __Complejidad:__
Implementar una Arquitectura Limpia puede introducir una complejidad adicional, especialmente en las fases iniciales de desarrollo. La separación de preocupaciones puede dar lugar a más archivos y directorios, lo que podría resultar abrumador para los proyectos más pequeños.
* :x: __Curva de aprendizaje:__
Los desarrolladores que no conocen la Arquitectura Limpia pueden enfrentarse a una curva de aprendizaje. Comprender los principios y aplicar correctamente la arquitectura puede requerir tiempo y esfuerzo.
* :x: __Boilerplate:__
La Arquitectura Limpia puede implicar escribir más código repetitivo, sobre todo en la asignación de datos entre capas. Esto podría aumentar el tiempo de desarrollo, aunque se argumenta que las ventajas de mantenimiento compensan este inconveniente.
* :x: __Sobre-ingeniería para proyectos sencillos:__
La Arquitectura Limpia puede ser excesiva para proyectos sencillos o pequeños en los que las ventajas de la separación y la modularidad no son tan pronunciadas. En estos casos, una arquitectura más sencilla puede ser más adecuada.
* :x: __Sobrecarga de rendimiento:__
Las capas y abstracciones adicionales de "Clean Architecture" podrían introducir cierta sobrecarga de rendimiento. En aplicaciones en las que el rendimiento es crítico, podría ser necesario un estudio y una optimización cuidadosos.
