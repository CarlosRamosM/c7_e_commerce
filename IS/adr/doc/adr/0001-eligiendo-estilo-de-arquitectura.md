# 0001: Eligiendo estilo de arquitectura

* Status: Proposed
* Deciders:
  * [Domingo Suarez Torres](domingo@circulosiete.com)
  * [Carlos Ramos Montoya](ramos.montoya.carlos@gmail.com)
* Date: 2024-11-16

## Context and Problem Statement

Derivado del curso: Arquitectura Java Modernas, es necesario poner en practica lo visto en el curso, por lo que se ha vuelto necesario elegir el estilo arquitectonico que será utilizado para el proyecto de código de nuestro software.

Para dar solución a **C7 E-Commerce**, es necesario contar con una arquitectura que permita ofrecer un servicio robusto y confiable, tanto para los usuarios: Cliente y Proveedor (usuarios internos de la plataforma), de igual manera es importante que la arquitectura permita la facil integración y comunición dentre los modulos que componen el modelo de negocio.

* **Inventario**
* **Pedidos**
* **Facturación**

## Decision Drivers

* **Fácil desarrollo**
* **Fácil evolución**
* **Escalabilidad**
* **Tolerante a fallos**

## Considered Options

* **Monolito**:
![Monolito](/IS/adr/doc/resources/imgs/monolito.png)
  * Beneficios
    * :heavy_check_mark: Fácil de usar
    * :heavy_check_mark: Costo
    * :heavy_check_mark: Confiable
  * Contras
    * :x: Partición técnica sobre partición de dominio
    * :x: Poco ágil
    * :x: Díficil de escalar
    * :x: Poca elastidad
    * :x: Requiere de gobierno
    * :x: Difícil de evolucionar
* **Micro Servicios**:
![Micro Servicios](/IS/adr/doc/resources/imgs/ms.jpg)
  * Beneficios
    * :heavy_check_mark: Ágil
    * :heavy_check_mark: Fácil de desplegar
    * :heavy_check_mark: Fácil de escalar
    * :heavy_check_mark: Tolerante a fallos
    * :heavy_check_mark: Fácil de evolucionar
    * :heavy_check_mark: Partición de dominio
  * Contras
    * :x: Difíl de usar
    * :x: Costo elevado (nivel organización, equipo técnico)
    * :x: Agrupar equipos con diferentes habilidades
* **Basa en Servicios (SBA)**:
![SBA](/IS/adr/doc/resources/imgs/sba.jpg)
  * Beneficios
    * :heavy_check_mark: Ágil
    * :heavy_check_mark: Fácil de evolucionar
    * :heavy_check_mark: Fácil de escalar
    * :heavy_check_mark: Tolerante a fallos
    * :heavy_check_mark: Partición de dominio (a nivel modular)
    * :heavy_check_mark: Bajo costo (organización, costo)
  * Contras
    * :x: Conocimiento y comprensión del equipo de desarrollo
    * :x: Agrupar equipos con diferentes habilidades

## Decision Outcome

1. El estilo de arquitectura seleccionado es **SBA** (Basada en servicios), tomando la idea de mantener separados los modelos de datos del estilo de arquitectura de MS (Microservicios).

2. El modelo de datos será dividido por modulo y no por funcionalidad (a diferencia de MS que propone la división por funcionalidad).

3. La capa de servicios será entendida como unidades de negocio, por lo que cada una de ellas puede actuar independiente al resto de las unidades de negocio.

### Positive Consequences <!-- optional -->

* :heavy_check_mark: Facíl de adoptar por el equipo de desarrollo
* :heavy_check_mark: Facíl de escalar
* :heavy_check_mark: Tolerante a fallos
* :heavy_check_mark: Partición de dominio (a nivel modular)

### Negative Consequences <!-- optional -->

* :x: Conocimiento y comprensión del equipo de desarrollo
* :x: Agrupar equipos con diferentes habilidades
