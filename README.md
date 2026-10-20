# Predicción del abandono de clientes (churn) con Big Data

Trabajo de Fin de Máster del **Máster en Big Data: Arquitectura, Análisis y Data Science** (Universidad Nebrija / Tokio School), entregado en febrero de 2026.

## El problema

Una empresa de servicios por suscripción pierde clientes en todos sus planes: el abandono supera el 50 % en los tres tipos de suscripción y llega a casi el 100 % en los contratos mensuales. El objetivo es **anticipar qué clientes van a darse de baja** y entender **qué factores lo provocan**, para que la empresa pueda actuar antes de perderlos.

El dataset tiene **10.000 clientes** sin valores nulos y 12 variables: edad, género, antigüedad, frecuencia de uso, llamadas a soporte, retrasos en el pago, tipo de suscripción, duración del contrato, gasto total, días desde la última interacción y si el cliente abandonó el servicio.

## Qué hice

1. **Clasificación de los datos:** tipifiqué cada variable (numérica o texto) y decidí cómo tratarla antes de modelar.
2. **Consultas con Cassandra:** levanté Cassandra con Docker, creé el keyspace y la tabla, cargué el CSV e indexé las columnas de consulta. Resultado: 3.233 suscripciones básicas, de las que 1.250 son anuales.
3. **Análisis exploratorio y descriptivo con PySpark:** analicé la distribución de clientes y el porcentaje de churn por tipo de suscripción y por duración de contrato, y codifiqué las variables categóricas con `StringIndexer`.
4. **Análisis de correlación:** las variables más relacionadas con el abandono son las llamadas a soporte (−0,58), el gasto total (0,42), la duración del contrato (−0,36) y los retrasos en el pago (−0,32).
5. **Modelo predictivo:** entrené un **Random Forest** con búsqueda de hiperparámetros, implementado de dos formas: con **scikit-learn** y con **MLlib de PySpark**.

## Resultados

En el conjunto de test, el modelo alcanza un **AUC de 0,99**. La matriz de confusión muestra 1.157 verdaderos negativos, 815 verdaderos positivos, 24 falsos positivos y ningún falso negativo: detecta a todos los clientes que se dieron de baja.

La variable más importante para el modelo son las **llamadas a soporte**, lo que apunta a problemas de uso o fallos del producto. El tipo de suscripción, la antigüedad y la frecuencia de uso apenas aportan.

**Conclusión de negocio:** la prioridad no es pasar clientes de Basic a Premium, sino resolver las causas del abandono (experiencia de soporte y percepción de precio) y llevar los contratos cortos hacia compromisos anuales.

## Tecnologías

Python · PySpark (Spark SQL y MLlib) · scikit-learn · Apache Cassandra · Docker · Google Colab

## Documentos

| Archivo | Contenido |
|---|---|
| [`informe_JosueJuan_Hormiga_Benitez.pdf`](informe_JosueJuan_Hormiga_Benitez.pdf) | Memoria completa con el análisis y las conclusiones |
| [`tecnico_JosueJuan_Hormiga_Benitez.pdf`](tecnico_JosueJuan_Hormiga_Benitez.pdf) | Documento técnico con el código y los comandos paso a paso |
| [`presentacion_JosueJuan_Hormiga_Benitez.pdf`](presentacion_JosueJuan_Hormiga_Benitez.pdf) | Presentación del trabajo |

## Autor

**Josué Hormiga Benítez**

- LinkedIn: [Josué Juan Hormiga Benítez](https://www.linkedin.com/in/josu%C3%A9-juan-hormiga-ben%C3%ADtez-098499334/)
- GitHub: [@josuehormigabenitez22-cmd](https://github.com/josuehormigabenitez22-cmd)
