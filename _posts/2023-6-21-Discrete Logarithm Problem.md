---
layout: post
title: Discrete Logarithm Problem
tags: [crypto]
---

### Discrete Logarithm Problem

# Introducción
Algunos métodos criptográficos como Diffie-Hellman, ElGamal o DSA basan su seguridad en el "problema del logaritmo discreto". El problema del logaritmo discreto es un problema matemático fundamental en criptografía y se refiere a la dificultad de encontrar la solución de una ecuación exponencial en un grupo cíclico finito.

## Grupo cíclico finito
Decimos que un grupo finito $G$ es cíclico cuando $\exists$ $g \in G$ tal que $\forall x \in G$, se cumple que $\exists k \in \mathbb{N}$ tal que $g^k = x$. Diremos que $g$ es el generador de $G$. Por ejemplo, si el grupo es $5\mathbb{Z}^*$ y el generador es $2$, entonces el logaritmo discreto de $1$ es $4$ porque $2^4 ≡ 24 ≡ 1 (mod 5)$.

## Problema del logaritmo discreto
El problema del logaritmo discreto se define como: dado un grupo $G$, un generador $g$ del grupo y un elemento $h$ de $G$, encontrar el logaritmo discreto en base $g$ de $h$ en el grupo $G$. El problema del logaritmo discreto no siempre es complicado, hay que tener en cuenta que la dificultad para encontrar logaritmos discretos depende de los grupos. Por ejemplo, una elección popular de grupos para criptosistemas basados en logaritmos discretos es $p\mathbb{Z}^*$, donde $p$ es un número primo. Sin embargo, si $p−1$ es un producto de primos pequeños, entonces el algoritmo de Pohlig-Hellman puede resolver eficientemente el problema del logaritmo discreto en este grupo. Por esta razón, siempre queremos que $p$ sea un número primo seguro al usar $p\mathbb{Z}^*$ como base de criptosistemas basados en logaritmos discretos. Un primo seguro es un número primo que cumple la propiedad de ser igual a $2q+1$, donde $q$ es un número primo grande. Esto garantiza que $p-1 = 2q$ tenga un factor primo grande, lo que dificulta que el algoritmo de Pohlig-Hellman resuelva fácilmente el problema del logaritmo discreto. Incluso si $p$ es un primo seguro, existe un algoritmo subexponencial llamado cálculo de índices. Esto significa que p debe ser muy grande (generalmente al menos 1024 bits) para hacer que los criptosistemas sean seguros.

