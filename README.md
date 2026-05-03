# Trabajar con una base de datos relacional utilizando el ecosistema Spring (junio de 2015)

El objetivo de este proyecto es estudiar y comparar diferentes arquitecturas de acceso a datos en una aplicación Java basada en el ecosistema **Spring**, concretamente **Spring JDBC** y **Spring JPA**, cuando se aplican a una base de datos relacional.

Los materiales teóricos y didácticos relacionados están disponibles aquí:  
👉 https://stahe.github.io/es-spring-database-juin-2015/

---

## Objetivos del proyecto

- Comprender una **arquitectura de aplicación en capas**
- Comparar dos enfoques de acceso a datos:
  - JDBC «clásico»
  - JPA (Java Persistence API)
- Medir y comparar el **rendimiento** de ambas soluciones
- Examinar los retos de la **portabilidad entre SGBD**

---

## Arquitectura general

La aplicación se basa en una arquitectura en capas, donde el flujo de ejecución va de izquierda a derecha:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000007080000017A09403716.png)


### Función de las capas

#### Capa de interfaz de usuario (UI)
- Punto de entrada de la aplicación
- Recibe las acciones del usuario
- Muestra los resultados

#### Capa de negocio (Business Layer)
- Implementa **reglas de negocio**
- Procesa datos procedentes de:
  - la base de datos (a través de DAO)
  - el usuario (a través de la interfaz de usuario)
- Puede devolver o persistir resultados

#### Capa DAO (objeto de acceso a datos)
- Expone una **interfaz de acceso a datos de negocio**
- Oculta los detalles técnicos del acceso a la base de datos
- Depende de la tecnología utilizada (JDBC o JPA)

#### Capa JDBC
- Interfaz estándar para acceder a bases de datos relacionales
- Independiente del SGBD (a través de controladores JDBC)
- Permite un buen rendimiento, pero una portabilidad limitada en la práctica

---

## Evolución hacia JPA

Desde mediados de la década de 2000, la arquitectura puede evolucionar de la siguiente manera:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

### Características específicas de JPA

- La capa **JPA** genera consultas SQL
- La capa DAO:
  - ya no contiene SQL
  - manipula objetos persistentes
- Ventajas:
  - Mejor portabilidad entre SGBD's
  - Abstracción del SQL propietario
- Desventajas:
  - Rendimiento generalmente inferior al de JDBC

JPA formaliza conceptos introducidos anteriormente por marcos como **Hibernate**.

---

## Comparación entre JDBC y JPA

El proyecto implementa **dos implementaciones DAO distintas**:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006E10000016947159BE8.png)


### Restricciones comunes

- `DAO1` y `DAO2` implementan la **misma interfaz `IDAO`**
- Las pruebas unitarias son **idénticas** para ambas implementaciones
- Objetivo: comparar la **funcionalidad** y el **rendimiento**

---

## Pruebas y rendimiento

- Las pruebas se realizan utilizando **JUnit**
- Se utiliza una única clase de prueba (`JUnitTestsDao`)
- Los resultados nos permiten:
  - verificar el cumplimiento funcional
  - comparar los tiempos de ejecución de JDBC frente a JPA

---

## Portabilidad del SGBD

Aunque JDBC tiene como objetivo la máxima portabilidad:
- el SQL propietario;
- las estrategias de generación de claves primarias;
- las palabras reservadas específicas;

limitan esta portabilidad en la práctica.

En este proyecto, las arquitecturas JDBC y JPA se portaron a **seis DBMS diferentes**, lo que requirió configuraciones específicas para cada DBMS.

---

## Conclusión

Este proyecto ilustra:
- las compensaciones entre **rendimiento** y **abstracción**;
- las decisiones arquitectónicas relacionadas con el acceso a los datos;
- la contribución de Spring a la estructuración y la capacidad de prueba de las aplicaciones;

Sirve como recurso educativo para adquirir una comprensión práctica de JDBC, JPA y sus usos comparativos dentro de una arquitectura Spring.

Serge Tahé, junio de 2015
---
