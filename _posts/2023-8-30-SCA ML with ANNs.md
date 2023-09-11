---
layout: post
title: SCA ML with ANNs
categories: [concepts]
tags: [crypto]
---

### SCA: ML with ANNs

# Tècniques 

CNNs, Autoencoders, (SVM, Random Forest)

# Introducción
En SC, la capa inicial de la red neural corresponde al numero de samples que vamos a testear mientras que la capa final corresponde a las clases de clasificación (en general, el valor de un Byte, i.e., 256 neuronas en la capa final). 
Las capas estan conectadas mediante caminos a los que se les asigna un peso, que servirá para priorizar unos caminos u otros. 
La red neuronal clasifica con una cierto probabilidad, clasificación predecida no siempre coincide con clasificación real. 

# Neural network
## Activation functions
La función activación sirve para evaluar el valor de la neurona. Ej. La función ReLu descarta las neuronas como "útil" o "no útil". El valor de las neuronas combinado con el peso de los caminos irá determinando la classificación.

## Low functions
Indica como de bueno es nuestro modelo clasificando. Lo ideal, seria que epoca a epoca, el valor de la low function mejorará (cada vez menos fallos). 


## Hyper-parameters
Algunos de los hyper-parametros que se intervienen en la clasificación son los siguientes:
- Época: abarca un único paso hacia adelante y hacia atrás a través del conjunto de entrenamiento para cada ejemplo.
- Batch size: Número de ejemplos que van juntos en un solo paso hacia adelante y hacia atrás Número de capas: Número de capas de la red neuronal
- Número de neuronas: Número de neuronas contenidas en cada capa.
- Dropout (Abandono): Porcentaje de neuronas que se olvidan aleatoriamente. Útil para evitar el sobreajuste. Se asegura que la red no está "memorizando" (a unos paths les ha puesto peso máximo y otros a peso mínimo), si esto pasa la red deja de "aprender" porque hay ciertos paths que ya no volverá a hacer. Para evitar esto, destruimos parte de "lo aprendido" para obligar a la red a provar distintos caminos constantemente. 
- Optimizador: algoritmo tipo SGD. Ejemplos: SGD, Adam, RMSprop, Adagrad, Adadelta... 
- Learning rate (Tasa de aprendizaje): Controla cuánto cambia un parámetro. Ej. 1e-3, 1e-4, 1e-5
- Batch normalization: Es una capa de la red neuronal, normaliza los valores entre 0 y 1 
- Initializer: Los valores iniciales de la red neuronal. Ej: Constante, Aleatorio, Glorot, etc. 
- Regularizer: Términos de penalización para la función de pérdida. Útil para evitar el sobreajuste. Ej: L1, L2, ortogonal
- Early stopping (parada anticipada): Número de épocas consecutivas sin mejora para detener un entrenamiento. Útil al realizar una búsqueda de hiperparámetros. Esto se utiliza sobretodo en algoritmos geneticos, ya que testeamos muchos parametros, si no ha ofrecido suficientes buenos resultados llegados a cierto punto no vale la pena seguir. 

# CNN (Convolutional Neural Network)
Las capas convolucionales tienen como objetivo extraer características localmente.
Cada capa de la red convolucional se centra en un nivel de abstracción. De más simple a más complejo.

Convolutional layer hyperparameters:
- Tamaño del filtro: Indica el tamaño del filtro.
- Número de filtros: el número de filtros en cada capa

Pooling layer hyperparameters:
- Tipo de agrupación: cómo se realiza la operación de agrupación. Agrupación media o máxima
- Tamaño de agrupación: Tamaño de la operación de agrupación
- Stride: Paso de la operación de pooling
- Relleno: relleno cero alrededor de la entrada o no.

# Training a Neural network
Posibles resultados:
- Under-fitting: No aprende, clasifica aleatoriamente. 
- Appropiate fitting: Correct training and validation accuracy value.
- Over-fitting: Too good to be true

Para entender evolución de la loss function y de training/validation accuracy: https://cs231n.github.io/neural-networks-3/

# Profiling attacks
En general, entreno la red para que aprenda ciertos "moldes" que luego testeare contra el caso real. 
Usar ANNs puede benificiar ante ciertas contramedidas: 
- Masking: Como en una traza hay información sobre el momento en que masquea y el momento en el que procesa, la red puede aprender a hacer un "high order" por si sola. 
- Shuffling
- Random Delays: No necesita las samples perfectamente alineadas, puede comprender que la misma información puede estar en distintos puntos.


# Attribution Methods
Hay distintos métodos que te permiten ver que samples te dan más información, es decir que samples son decisivas para clasificar. Puede servirte para identificar los puntos de leakage. 

# DL-LA vs T-Test
Simplifico la red al máximo, solo quiero clasificar en dos.

# CPA vs DLPA
En el CPA distinguia la clave correcta porque diferencia entre la media de ambos sets tendía a zero. Cuando esa diferencia era distinta de cero, significa que las medias son distintas, por tanto los sets son distintos, por tanto el guess era correcto.
En DLPA la lógica es la misma, cuando le de dos sets "aleatorios" la red será incapaz de aprender a clasificar, porque no existe uns "lógica" detrás de la clasificación. En cambio, si he usado el guess correcto para diferenciar los dos sets, la red aprenderá a clasificar. El guess correcto entonces será confirmado por la evolución de la accuracy cuando avanzan las épocas.  

# Autoencoders
Inicialmente, se uso para pasar imágenes de baja definición a alta definición. En SC, lo usaremos para maximizar las características propias de la traza y eliminar el ruido. Es útil como paso previo para hace ataques de CPA. 
La primera y la última capa de la red tendran el mismo tamaño.
Usos:
- Para eliminar el ruido
- Para alinear trazas
- Para eliminar masking

# SC tradicional vs ML 
| Traditional SCA |ML based SCA|
| -- | -- |
| T-TEST/HO T-TEST |DL-LA | 
|DPA/CPA/HO DPA/HOCPA |DLPA | 
|Static / Elastic align|Autoencoder Align | 
|LowPass / Moving average|Autoencoder Denoise |
|Template Attack / SVM | ANN/CNN |
|BigMac/CCAHS |Clustering Techniques
