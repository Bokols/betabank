# Descripción del Proyecto: Predicción de la Pérdida de Clientes Usando Modelos de Aprendizaje Automático

## Introducción

En este proyecto, nuestro objetivo es predecir la pérdida de clientes (la probabilidad de que un cliente abandone el banco) para el Banco Beta. El objetivo principal es construir un modelo de aprendizaje automático capaz de predecir con precisión si un cliente abandonará o no el banco, basándose en diversas características como datos demográficos, información de cuentas y comportamiento del cliente. Lograr un alto rendimiento en términos de precisión de predicción y minimizar los falsos negativos (clientes predichos para quedarse pero que en realidad se irán) es crucial para los esfuerzos de retención de clientes. Exploramos varios modelos, incluidos la regresión logística, los árboles de decisión y técnicas para manejar clases desequilibradas, como el sobremuestreo, el submuestreo y el balanceo de clases.

### Definición del Problema

El desafío de predecir la pérdida de clientes en una institución financiera es vital para mitigar pérdidas mediante la atención proactiva a la insatisfacción del cliente. El conjunto de datos se caracteriza por un desequilibrio en las clases, donde el número de clientes que se van (pérdida) es significativamente menor que el de los que permanecen. Este desequilibrio complica el proceso de predicción y a menudo conduce a modelos sesgados que predicen la clase mayoritaria de manera más precisa.

## Resumen de los Hallazgos

A lo largo de este proyecto, experimentamos con diferentes modelos de aprendizaje automático y estrategias para manejar el desequilibrio de clases, evaluando los modelos en función de métricas clave como la precisión y la puntuación F1. A continuación, se presenta un resumen de los hallazgos para cada enfoque adoptado.

### 1. Regresión Logística

Inicialmente aplicamos **Regresión Logística** al problema. Este modelo se entrenó con las características proporcionadas y la variable objetivo, con un enfoque en clasificar si un cliente abandonaría o no el banco.

- **Resultados de Validación:** 
   - Precisión: 80.2%
   - Puntuación F1: 0.33

- **Resultados de Prueba:** 
   - Precisión: 79.15%
   - Puntuación F1: 0.27

A pesar de tener una precisión razonable, la puntuación F1 fue significativamente más baja, lo que indica que el modelo no estaba prediciendo eficazmente la clase minoritaria (clientes que abandonan). Este resultado destacó la necesidad de un modelo más sofisticado o la aplicación de técnicas para abordar el desequilibrio de clases.

### 2. Árbol de Decisión con Ponderación de Clases

Luego, aplicamos un **Clasificador de Árbol de Decisión** con ponderación de clases configurada como "balanceada". Esta técnica se eligió porque los árboles de decisión suelen ser efectivos para problemas de clasificación, y ajustar las ponderaciones de clases ayuda a equilibrar la importancia de ambas clases en el entrenamiento.

Probamos varios valores de **max_depth** para el árbol de decisión, que variaban de 1 a 8.

- **Modelo con Mejor Rendimiento (max_depth=5):**
   - **Resultados de Validación:** 
     - Precisión: 81.05%
     - Puntuación F1: 0.60
   - **Resultados de Prueba:**
     - Precisión: 79.8%
     - Puntuación F1: 0.58

El uso de un árbol de decisión con ponderación de clases mejoró la puntuación F1, pero aún no alcanzó la puntuación objetivo de 0.59 para el conjunto de prueba. Sin embargo, este modelo mostró resultados prometedores al equilibrar las clases y predecir la pérdida de clientes.

### 3. Sobremuestreo (Upsampling)

Para abordar aún más el desequilibrio de clases, aplicamos **sobremuestreo (upsampling)** a los datos de entrenamiento. Esta técnica consistió en replicar la clase minoritaria (clientes que se van) para equilibrar la distribución de clases. Experimentamos con un factor de repetición de 5, lo que significó que la clase minoritaria se sobreamplió cinco veces para igualar el tamaño de la clase mayoritaria.

- **Resultados con Entrenamiento Sobremuestreado:**
   - **Resultados de Validación:** 
     - Puntuación F1: 0.59
   - **Resultados de Prueba:**
     - Puntuación F1: 0.60

Aunque este método mejoró ligeramente la puntuación F1 en los datos de prueba, el rendimiento no superó sustancialmente al árbol de decisión con ponderación de clases. Sin embargo, el enfoque de sobremuestreo aumentó el equilibrio general en el conjunto de datos.

### 4. Submuestreo (Downsampling)

Finalmente, empleamos **submuestreo (downsampling)** como un enfoque alternativo para manejar el desequilibrio de clases. Esta técnica reduce la cantidad de muestras de la clase mayoritaria para lograr un conjunto de datos más equilibrado. Aplicamos una fracción de 0.25 a la clase mayoritaria, mientras que manteníamos intacta la clase minoritaria.

- **Resultados con Entrenamiento Submuestreado:**
   - **Resultados de Validación:** 
     - Puntuación F1: 0.59
   - **Resultados de Prueba:**
     - Puntuación F1: 0.60

El submuestreo ayudó a alcanzar la puntuación F1 objetivo de 0.59 para el conjunto de validación y 0.60 para el conjunto de prueba, convirtiéndolo en el método más exitoso para lograr el equilibrio deseado entre precisión y recall.

### 5. Evaluación ROC-AUC

Para evaluar la capacidad del modelo para discriminar entre clientes que se van y los que permanecen, calculamos la **puntuación ROC-AUC**, que mide la capacidad del modelo para clasificar correctamente las predicciones en todos los umbrales de clasificación.

- **Puntuación ROC-AUC de Validación:** 0.82
- **Puntuación ROC-AUC de Prueba:** 0.83

Una puntuación AUC-ROC superior a 0.8 indica que el modelo está funcionando bien en la discriminación entre los casos de pérdida y no pérdida. Estos resultados demostraron que el modelo tiene un fuerte poder discriminatorio, lo que lo hace adecuado para identificar clientes en riesgo de abandonar.

## Conclusión

En conclusión, el **Clasificador de Árbol de Decisión** con **ponderación de clases** y **submuestreo** surgió como el modelo de mejor rendimiento para predecir la pérdida de clientes en el Banco Beta. El modelo final alcanzó:

- **Puntuación F1:** 0.60 (en el conjunto de prueba)
- **Puntuación ROC-AUC:** 0.83 (en el conjunto de prueba)

Estos resultados indican que el modelo puede predecir eficazmente la pérdida de clientes y proporcionar valiosos conocimientos para estrategias proactivas de retención. Aunque la puntuación F1 no es perfecta, cumple con el objetivo del proyecto de mejorar las predicciones de retención de clientes. Un ajuste adicional del modelo y la exploración de técnicas más avanzadas, como modelos de conjunto o aprendizaje profundo, podrían ofrecer incluso mejores resultados en el futuro.

Los conocimientos obtenidos de este modelo pueden ser utilizados por el Banco Beta para identificar clientes en riesgo, lo que permitirá al banco intervenir y mejorar la satisfacción del cliente, minimizando así la pérdida de clientes y mejorando la retención.
