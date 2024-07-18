+++
author = "Emanuele Civini" 
title = "Schnorr identification protocol over Curve25519" 
date = 2024-07-17
tags = ["cryptography", "identification", "Schnorr", "Curve25519"]
math = true
+++

Schnorr identification is a simple protocol that lets a verifier verify the identity of a prover and is secure against eavesdropping attacks under the discrete logarithm assumption.

## What is an identity?

Given a cyclic group $G$ of prime order $q$ with generator $g \in G$, an identity is given by the public key of a key pair owned by the prover, which is generated as follows:

- secret key is a random element $\alpha \in \mathbb{Z}_{q}$
- public key is the group element $u = g^{\alpha} \in G$

## How does it work?

Schnorr identification is an interactive protocol divided in four phases, where a Prover $P$ and a verifier $V$ exchange information with each other.
In the first phase, prover $P$ computes a new key pair that will be used in conjunction with its identity. To do so, it computes a random $\alpha_{t} \leftarrow \mathbb{Z_{q}}$, then it derives
$u_{t} = g^{\alpha_{t}}$ and lastly it sends $u_{t}$ to $V$. In the second phase, the verifier $V$ generates and sends to the prover $P$ a random challenge, which is an element $c \in C$, where $C$ is a subset of $\mathbb{Z_{q}}$.
In the third step, the prover $P$ computes and sends $\alpha_{z} \leftarrow \alpha_{t} + \alpha c \in \mathbb{Z_{q}}$ to the verifier $V$. In the last step, the verifier $V$ outputs $accept$ if $g^{\alpha_{z}} = u_{t} u^{c}$, $reject$ otherwise.  
The algorithm is correct because, since $u_{t} = g^{\alpha_{t}}$ and $\alpha_{z} = \alpha_{t} + \alpha c$, we have:
$$
g^{\alpha_{z}} = g^{\alpha_{t} + \alpha c} = g^{\alpha_{z}} \cdot (g^{\alpha})^{c} = u_{t} \cdot u^{c}
$$

Therefore the protocol outputs $accept$ if both the prover and the verifier are correct.

## Implementation

The algorithm described above is taken from the book [Applied Cryptography](https://toc.cryptobook.us/) and I decided to implement it in Rust, using Curve25519 as a group and thus $\mathbb{Z}/l\mathbb{Z}$ instead of $\mathbb{Z}_{q}$. Because of this, I had to use EC multiplication with a scalar instead of exponentiation, and EC addition instead of multiplication. The source code can be found [on my Github](https://github.com/ecivini/schnorr-id) and is not meant to be production ready (also because of the limited use cases), rather more a personal experiment.
