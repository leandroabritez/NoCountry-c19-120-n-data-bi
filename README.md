# NO COUNTRY | c19-120-n-data-bi | Detección de Fraude en Transacciones Fintech

## Sobre el Proyecto

Este proyecto tiene como objetivo desarrollar un algoritmo de machine learning para detectar transacciones fraudulentas en servicios financieros. Dada la falta de conjuntos de datos públicos en el dominio de las transacciones de dinero móvil, utilizamos un conjunto de datos sintético generado por el simulador PaySim.

## Descripción del Conjunto de Datos

### Contexto

Los conjuntos de datos públicos sobre servicios financieros, especialmente en transacciones de dinero móvil, son escasos debido a la naturaleza privada de las transacciones financieras. Estos conjuntos de datos son cruciales para los investigadores, particularmente en la detección de fraudes.

PaySim aborda este problema generando un conjunto de datos sintético que refleja las operaciones normales de las transacciones e inyecta comportamientos maliciosos para evaluar el rendimiento de los métodos de detección de fraude.

### Contenido

PaySim simula transacciones de dinero móvil basadas en un mes de transacciones reales de un servicio de dinero móvil en un país africano. Los datos originales fueron proporcionados por una empresa multinacional que opera en más de 14 países.

Este conjunto de datos sintético está reducido a 1/4 del original y fue creado para Kaggle.

### Nota Importante

Las transacciones detectadas como fraude son canceladas, por lo que las columnas `oldbalanceOrg`, `newbalanceOrig`, `oldbalanceDest` y `newbalanceDest` no deben usarse para la detección de fraude.

### Encabezados del Conjunto de Datos

A continuación se presenta una explicación de las columnas del conjunto de datos:

- **step**: Mapea una unidad de tiempo en el mundo real (1 paso = 1 hora). El número total de pasos es 744 (simulación de 30 días).
- **type**: El tipo de transacción (`CASH-IN`, `CASH-OUT`, `DEBIT`, `PAYMENT`, `TRANSFER`).
- **amount**: El monto de la transacción en moneda local.
- **nameOrig**: El cliente que inició la transacción.
- **oldbalanceOrg**: El saldo inicial antes de la transacción.
- **newbalanceOrig**: El nuevo saldo después de la transacción.
- **nameDest**: El destinatario de la transacción.
- **oldbalanceDest**: El saldo inicial del destinatario antes de la transacción (información no disponible para comerciantes que comienzan con 'M').
- **newbalanceDest**: El nuevo saldo del destinatario después de la transacción (información no disponible para comerciantes que comienzan con 'M').
- **isFraud**: Indica si la transacción es fraudulenta.
- **isFlaggedFraud**: Marca transacciones superiores a 200,000 como intentos ilegales.

### Ejemplo de Fila de Datos

Ejemplo de una fila de datos con explicaciones:

1,PAYMENT,1060.31,C429214117,1089.0,28.69,M1591654462,0.0,0.0,0,0

## Stack Tecnológico

Para el desarrollo de este proyecto, utilizaremos las siguientes herramientas tecnológicas:

- **Python**: Lenguaje de programación principal para el desarrollo del algoritmo de machine learning y análisis de datos.
- **Tableau**: Herramienta de visualización de datos para crear dashboards interactivos y gráficos que ayuden a interpretar los resultados.
- **Google Colab**: Plataforma de notebooks en la nube que permite escribir y ejecutar código Python de forma colaborativa.
- **Google Cloud Platform (GCP)**: Infraestructura en la nube para almacenamiento de datos, ejecución de modelos de machine learning y despliegue de aplicaciones.
- **Trello**: Herramienta de gestión de proyectos para organizar tareas, seguimiento del progreso y colaboración en equipo.

### Antecedentes de la Investigación

Cinco archivos similares contienen diferentes escenarios, como se detalla en la tesis doctoral "Sistemas escalables y eficientes en recursos para el análisis de big data" (http://urn.kb.se/resolve?urn=urn:nbn:se:bth-12932).

Cada ejecución de PaySim utiliza semillas aleatorias para 744 pasos, representando cada hora de un mes de tiempo real, generando aproximadamente 24 millones de registros financieros en cinco categorías: `CASH-IN`, `CASH-OUT`, `DEBIT`, `PAYMENT` y `TRANSFER`.

## Agradecimientos

Este trabajo es parte del proyecto de investigación “Sistemas escalables y eficientes en recursos para el análisis de big data” financiado por la Fundación del Conocimiento (subvención: 20140032) en Suecia.

### Cita

Por favor, refiérase a este conjunto de datos utilizando la siguiente cita:

- E. A. Lopez-Rojas, A. Elmir, y S. Axelsson. "PaySim: Un simulador financiero de dinero móvil para la detección de fraudes". En: El 28º Simposio Europeo de Modelado y Simulación-EMSS, Larnaca, Chipre. 2016
