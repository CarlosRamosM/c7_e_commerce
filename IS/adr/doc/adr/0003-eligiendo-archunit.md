# 0003: Uso de ArchUnit para validar reglas de arquitectura

* Status: Proposed
* Deciders:
  * [Domingo Suarez Torres](domingo@circulosiete.com)
  * [Carlos Ramos Montoya](ramos.montoya.carlos@gmail.com)
* Date: 2024-11-23

## Context and Problem Statement

Para validar y garantizar que dentro del proyecto se sigan las reglas establecidas por el estilo arquitectonico eligido para el desarrollo del software, es necesario contar con un mecanismo de validación automatizada de dichas reglas.

Hoy en día se suele realizar esta tarea de manera manual al momento de revisar los **PRs** generados por los equipos de desarrollo, lo cual puede llevar a omisiones por el **reviewer** del **PR**, esto puede tener como resultado romper/ensuciar la salud de del proyecto.

## Decision Drivers

* **Automatizar la validación de las reglas de arquitectura.**
* **Minimizar lo más posible riesgos de contaminar el proyecto.**
* **Reducir el tiempo de revisión de los PRs.**

## Considered Options

* ArchUnit
* SonarQube
* Custom scripts
* Revisiones manuales

## Decision Outcome

**[ArchUnit](https://www.archunit.org/):** Biblioteca de Java, para definir y validar las reglas de arquitectura mediante test case, los cuales se escriben como código.

### Positive Consequences

* :heavy_check_mark: Permite escribir pruebas arquitectónicas como código.
* :heavy_check_mark: La pruebas son fácil de integrar en el pipeline de pruebas existente.
* :heavy_check_mark: Las validaciones se realizab de manera automática.

### Negative Consequences

* :x: Curva de aprendizaje.
* :x: Aunque las pruebas se escriben similar a JUnit, se puede caer en errores si no se conoce el API de la librería.

## Pros and Cons of the Options <!-- optional -->

### SonarQube

* :heavy_check_mark: Detecta violaciones de estándares y patrones en el código, incluyendo algunas reglas arquitectónicas.
* :x: Más enfocado en análisis de código estático que en validaciones específicas de arquitectura.
* :x: Carece de la flexibilidad que ofrece ArchUnit para definir reglas personalizadas.

### Custom scripts

* :heavy_check_mark: Total control sobre las validaciones.  
* :x: Mayor esfuerzo de desarrollo y mantenimiento.
* :x: Requiere reinventar funcionalidades que ya están disponibles en ArchUnit.

### Revisiones manuales

* :heavy_check_mark: No requiere herramientas externas.  
* :x: Propenso a errores humanos.
* :x: Difícil de escalar en un equipo grande.

### Links

* [Getting Started](https://www.archunit.org/getting-started)
