---
layout: post
title: Notas. State of the art of secure ECC implementations (2010)
categories: [notes]
tags: [ecc, sc]
---

### State-of-the-art of secure ECC implementations: a survey on known side-channel attacks and countermeasures*
\* Notas del paper:  https://www.esat.kuleuven.be/cosic/publications/article-1461.pdf
hoka
# Introducción
Suponemos que, además de conocer los inputs i outputs de una operación criptografica, el atacante puede obtener iformación a través de "canales laterales". Entonces, es posible que sea capaz de conseguir la clave sin "romper" el algoritmo cryptográfico.

Objetivos: 
- "Overview" de los distintos ataques que aplican a curvas elípticas.
- Sistematización de un método para elegir contramedidas durante el diseño de un producto.

## Implementaciones y ataques físicos
Los ataques buscaran explotar una de estas dos:
- La relación existente entre los datos/operaciones y el leakage físico que produzcan.
- La relación entre los datos que hipotéticamente se esten tratando y los datos que realmente se tratan.

##  Ataques pasivos y contramedidas

El siguiente esquema muestra la relación entre las distintas contramedidas y ataques. Tener en cuenta que algunas contramedidas protegen ante algunos ataques pero, a la vez, lo hacen vulnerable ante otros.

![](/images/contramedidasECC.png)
