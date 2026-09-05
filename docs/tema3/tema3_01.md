# MODELO LÓGICO. MODELO RELACIONAL. DISEÑO Y NORMALIZACIÓN DE LA BBDD RELACIONALES

## RESULTADOS DE APRENDIZAJE

**RA6** Diseña modelos relacionales normalizados interpretando diagramas entidad/relación

## CRITERIOS DE EVALUACIÓN

* **RA6.a.** Se han utilizado herramientas gráficas para representar el diseño lógico.
* **RA6.b.** Se han identificado las tablas del diseño lógico.
* **RA6.c.** Se han identificado los campos que forman parte de las tablas del diseño lógico.
* **RA6.d.** Se han analizado las relaciones entre las tablas del diseño lógico.
* **RA6.e** Se han identificado los campos clave.
* **RA6.f** Se han aplicado reglas de integridad.
* **RA6.g** Se han aplicado reglas de normalización.

**NÚMERO DE SESIONES:** 10

## INTRODUCCIÓN

En la unidad anterior se ha obtenido un esquema conceptual empleando el Modelo Entidad/Relación. Dicho esquema corresponde al ámbito conceptual, al mundo de las ideas. Ahora vamos a desarrollar el **Diseño de los Datos**.

La fase de análisis de los datos se centra en qué datos debe recordar la aplicación. En cambio, la fase de diseño de datos da un paso más en el acercamiento a la solución. Trata de encontrar cómo organizar la información para que pueda ser manejada por el ordenador.

El diseño de los datos consta de dos partes: diseño de estructuras en las que se almacenarán los datos y diseño de consultas, donde se recogerán los accesos que se realicen sobre los datos. Al esquema de la BD obtenido en el diseño se le denomina esquema lógico de datos. Existen diferentes modelos lógicos para desarrollar el esquema lógico de la BD. Nosotros emplearemos el más utilizado, el Modelo Relacional (MR).

La teoría del Modelo Relacional se desarrolló hacia 1970 de la mano de *E. Codd*, que propuso también tres lenguajes de definición y manipulación de datos basados en el Álgebra de conjuntos y el Cálculo de predicados de primer orden. Desde entonces, el Modelo Relacional se ha impuesto claramente sobre sus inmediatos predecesores, el Jerárquico y el Red, por  su sencillez y por la aparición de un lenguaje de definición de datos, el SQL (Standard Query Language), de fuerte aceptación como lenguaje de manipulación de datos.

Al encontrarnos en la fase de diseño lógico, el modelo de datos que utilicemos influirá directamente en el tipo de BD y SGBD a utilizar posteriormente. Por tanto, si utilizamos durante el diseño lógico el modelo relacional será porque después utilizaremos un **SGBD relacional** (y por tanto, una **BD relacional**). Así, al tratar las principales características del modelo relacional estaremos también tratando las de las BD relacionales.

Veremos las normas a seguir para poder **transformar el modelo E/R al MR**. Este proceso también se llama Paso a Tablas.
