---
layout: post
title:  "Tradução do Whitepaper do Ethereum para Português"
date:   2017-08-28 20:00:00 +0003
categories: pt-br ethereum
---

[Link para a versão original (em inglês)](https://github.com/ethereum/wiki/wiki/White-Paper)

https://github.com/ethereum/wiki/wiki/%5BPortuguese%5D-White-Paper


Uma Próxima Geração de Plataforma para Aplicações Descentralizadas e Contratos Inteligentes
-----------------------------------------------------------------------------------------

O desenvolvimento do Bitcoin, realizado por Satoshi Nakamoto entre 2008 e 2009, frequentemente 
tem sido celebrado como uma revolução financeira e monetária, é o primeiro exemplo
de um ativo digital que não possui nem lastro ou valor intrínseco e nem controlador ou emissor 
centralizado. No entanto, outra parte - provavelmente mais importante - desse experimento 
é sua subjacente tecnologia de cadeia de blocos, utilizada como ferramenta de seu consenso 
distribuído e que vem rapidamente atraindo atenção para esse outro aspecto do Bitcoin. Entre as
alternativas para aplicações da tecnologia de cadeia de blocos estão incluídas
o uso de ativos digitais baseados em cadeia de blocos para representar moedas customizadas e 
instrumentos financeiros ("moedas coloridas"), o domínio de uma propriedade inteligente de 
um dispositivo físico, ativos não-fungíveis como nomes de domínios (Namecoin), assim como
aplicações mais complexas que envolvam ativos digitais diretamente controlados
por um trecho de código que implemente regras arbitrárias, conhecidas como Contratos Inteligentes, 
ou mesmo organizações autônomas e descentralizadas baseadas em uma cadeia de blocos (OADs). 
A proposta do Ethereum é prover uma cadeia de blocos com uma linguagem de programação 
Turing-completa nativa, que pode ser usada para criar "contratos" capazes de registrar funções 
arbitrárias de transição de estado, permitindo aos usuários criar 
qualquer um dos sistemas descritos anteriormente, bem como outros sistemas que nós não
tenhamos sequer imaginado, simplesmente escrevendo sua lógica em poucas linhas de código.


Sumário
-------

...

Introdução ao Bitcoin e Conceitos Relevantes
--------------------------------------------
The concept of decentralized digital currency, as well as alternative applications like property registries, has been around for decades. The anonymous e-cash protocols of the 1980s and the 1990s were mostly reliant on a cryptographic primitive known as Chaumian Blinding.[8] Chaumian Blinding provided these new currencies with high degrees of privacy, but their underlying protocols largely failed to gain traction because of their reliance on a centralized intermediary. In 1998, Wei Dai's b-money[9] became the first proposal to introduce the idea of creating money through solving computational puzzles as well as decentralized consensus, but the proposal was scant on details as to how decentralized consensus could actually be implemented. In 2005, Hal Finney introduced a concept of reusable proofs of work,[10] a system which uses ideas from b-money together with Adam Back's computationally difficult Hashcash[11] puzzles to create a concept for a cryptocurrency, but once again fell short of the ideal by relying on trusted computing as a backend. In 2009, a decentralized currency was for the first time implemented in practice by Satoshi Nakamoto,[1c][1d] combining established primitives for managing ownership through public key cryptography with a consensus algorithm for keeping track of who owns coins, known as "proof of work."