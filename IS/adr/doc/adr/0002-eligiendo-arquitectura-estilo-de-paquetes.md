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

Con la elección de "Clean Architecture", podemos organizar los paquetes de los proyectos de la siguiente manera:

```plaintext
com.c7.ecommerce.(bounded_context)  //bounded_context sera sustituido por el nombre (inventory, orders, invoice)
│
├── domain            // Núcleo de la lógica de negocio
│   ├── model         // Entidades y objetos de dominio
│   ├── repository    // Interfaces para acceso a datos
│   └── service       // Lógica de dominio compleja (opcional)
│
├── application       // Casos de uso (orquestan la lógica del dominio)
│   ├── usecase       // Implementaciones de casos de uso
│   └── port          // Interfaces para interactuar con las capas externas
│
├── infrastructure    // Implementaciones técnicas (bases de datos, APIs, etc.)
│   ├── repository    // Implementaciones de los repositorios
│   ├── messaging     // Integración con mensajería o eventos
│   └── configuration // Configuración técnica (Spring, etc.)
│
└── adapters          // Adaptadores para interfaces de usuario
    ├── rest          // Controladores REST

```

### Positive Consequences <!-- optional -->

* [e.g., improvement of quality attribute satisfaction, follow-up decisions required, …]
* …

### Negative Consequences <!-- optional -->

* [e.g., compromising quality attribute, follow-up decisions required, …]
* …

## Pros and Cons of the Options <!-- optional -->

### [option 1]

[example | description | pointer to more information | …] <!-- optional -->

* Good, because [argument a]
* Good, because [argument b]
* Bad, because [argument c]
* … <!-- numbers of pros and cons can vary -->

### [option 2]

[example | description | pointer to more information | …] <!-- optional -->

* Good, because [argument a]
* Good, because [argument b]
* Bad, because [argument c]
* … <!-- numbers of pros and cons can vary -->

### [option 3]

[example | description | pointer to more information | …] <!-- optional -->

* Good, because [argument a]
* Good, because [argument b]
* Bad, because [argument c]
* … <!-- numbers of pros and cons can vary -->

## Links <!-- optional -->

* … <!-- numbers of links can vary -->
