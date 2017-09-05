---
layout: post
title:  "Tradução do Whitepaper do Ethereum para Português"
date:   2017-08-28 20:00:00 +0003
categories: pt-br ethereum
---

[Link para a versão original (em inglês)](https://github.com/ethereum/wiki/wiki/White-Paper)

### Uma Próxima Geração de Plataforma para Aplicações Descentralizadas e Contratos Inteligentes

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


### Sumário

* [Introdução ao Bitcoin e Conceitos Relevantes](#introduction-to-bitcoin-and-existing-concepts)
    * [História](#history)
    * [Bitcoin As A State Transition System](#bitcoin-as-a-state-transition-system)
    * [Mining](#mining)
    * [Merkle Trees](#merkle-trees)
    * [Alternative Blockchain Applications](#alternative-blockchain-applications)
    * [Scripting](#scripting)
* [Ethereum](#ethereum)
    * [Ethereum Accounts](#ethereum-accounts)
    * [Messages and Transactions](#messages-and-transactions)
    * [Ethereum State Transition Function](#ethereum-state-transition-function)
    * [Code Execution](#code-execution)
    * [Blockchain and Mining](#blockchain-and-mining)
* [Applications](#applications)
    * [Token Systems](#token-systems)
    * [Financial derivatives](#financial-derivatives-and-stable-value-currencies)
    * [Identity and Reputation Systems](#identity-and-reputation-systems)
    * [Decentralized File Storage](#decentralized-file-storage)
    * [Decentralized Autonomous Organizations](#decentralized-autonomous-organizations)
    * [Further Applications](#further-applications)
* [Miscellanea And Concerns](#miscellanea-and-concerns)
    * [Modified GHOST Implementation](#modified-ghost-implementation)
    * [Fees](#fees)
    * [Computation And Turing-Completeness](#computation-and-turing-completeness)
    * [Currency And Issuance](#currency-and-issuance)
    * [Mining Centralization](#mining-centralization)
    * [Escalabilidade](#scalability)
* [Conclusão](#conclusion)
* [Notes, References and Further Reading](#notes-references-and-further-reading)


## Introdução ao Bitcoin e Conceitos Relevantes


### História

O conceito de moeda digital descentralizada, bem como suas aplicações no 
registro de propriedades, existe há décadas. Os protocolos anônimos de e-cash 
dos anos 80 e 90 eram muito dependentes de uma criptografia primitiva conhecida
como Chaumian Blinding. Essa criptografia viabilizava moedas com alto grau de 
privacidade, mas seus protocolos simplesmente não ganhavam relevância por 
confiarem em um intermediário centralizado. Em 1998, o b-money, de Wei Dai, foi 
o primeiro a propor emissão de dinheiro através da resolução de problemas 
computacionais e consenso descentralizado, mas apresentou poucos detalhes sobre 
como poderia ser implementado esse consenso. Em 2005, Hal Finney introduziu o 
conceito de provas de trabalho reutilizáveis, um sistema que utiliza ideias do 
b-money e os problemas computacionais complexos do Hashcash de Adam Back,
criando então um conceito de criptomoeda, mas mais uma vez estando aquém do 
ideal, pois dependia de computação confiável como backend. Em 2009, pela 
primeira vez uma moeda descentralizada foi implementada por Satoshi Nakamoto, 
combinando princípios de gestão de propriedade através criptografia de chave 
pública com um algoritmo de consenso que mantém o registro de quem possui o 
dinheiro, chamado "prova de trabalho".

O mecanismo por trás da prova de trabalho foi um importante avanço, pois 
solucionou dois problemas simultaneamente. Primeiramente, ele apresentou um 
simples e relativamente efetivo algoritmo de consenso, permitindo que os nós de 
uma rede concordassem coletivamente sobre um conjunto de atualizações do estado 
do livro-contábil do Bitcoin. Finalmente, ele liberou o ingresso a esse 
processo consensual, solucionando um problema político para decidir quem tem 
influência no consenso, previnindo simultaneamente ataques Sybil. A prova de 
trabalho substitui tanto a barreira formal para a participação, quanto a 
exigência de estar registrado como uma entidade única em uma lista particular, 
utilizando uma barreira mais econômica: o peso de um único nó no processo 
consensual de votação é diretamente proporcional a seu poder computacional. 
Desde então, uma abordagem alternativa chamada "prova de participação" tem sido 
proposta, onde o peso do nó é proporcional ao saldo de criptomoedas possuidas 
por ele. A discussão sobre os relativos méritos das duas abordagens vai além do 
escopo desse artigo, mas é importante ter em conta que ambas podem ser 
empregadas para estruturar uma criptomoeda.

### Bitcoin As A State Transition System


traduzir a FIGURA

https://github.com/ethereum/wiki/wiki/White-Paper#bitcoin-as-a-state-transition-system