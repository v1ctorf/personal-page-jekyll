---
layout: post
title:  "Tradução do Whitepaper do Ethereum para Português"
date:   2017-08-28 20:00:00 +0003
categories: pt-br ethereum
---

[Link para a versão original (em inglês)](https://github.com/ethereum/wiki/wiki/White-Paper)

### Uma Próxima Geração de Plataforma para Aplicações Descentralizadas e Contratos Inteligentes

O desenvolvimento do Bitcoin, concebido por Satoshi Nakamoto entre 2008[<sup>[1a]</sup>](http://nakamotoinstitute.org/bitcoin/)[<sup>[1b]</sup>](http://www.newyorker.com/magazine/2011/10/10/the-crypto-currency)–
2009[<sup>[1c]</sup>](https://en.bitcoin.it/wiki/Category:History)[<sup>[1d]</sup>](https://blockexplorer.com/block/000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f)
e frequentemente celebrado como uma revolução financeira e monetária, é o primeiro exemplo
de um ativo digital que não possui lastro ou valor intrínseco[<sup>[2]</sup>](https://bitcoinmagazine.com/articles/you-say-bitcoin-has-no-intrinsic-value-twenty-two-reasons-to-think-again-1399454061/) 
e nem controlador ou emissor centralizado. No entanto, outra parte - provavelmente mais importante - desse experimento 
é sua subjacente tecnologia de cadeia de blocos, utilizada como ferramenta de seu consenso 
distribuído e que vem rapidamente atraindo atenção para esse outro aspecto do Bitcoin. Entre as
alternativas para aplicações da tecnologia de cadeia de blocos estão incluídas
o uso de ativos digitais baseados em cadeia de blocos para representar moedas customizadas e 
instrumentos financeiros ("moedas coloridas")[<sup>[3]</sup>](https://docs.google.com/a/buterin.com/document/d/1AnkP_cVZTCMLIzw4DvsW6M8Q2JC0lIzrTLuoWu2z1BE/edit), 
o domínio de uma propriedade inteligente de 
um dispositivo físico[<sup>[4]</sup>](https://en.bitcoin.it/wiki/Smart_Property), 
ativos não-fungíveis como nomes de domínios (Namecoin)[<sup>[5]</sup>](http://namecoin.org), assim como
aplicações mais complexas que envolvam ativos digitais diretamente controlados
por um trecho de código que implemente regras arbitrárias, conhecidas como Contratos Inteligentes[<sup>[6]</sup>](https://en.bitcoin.it/wiki/Contracts), 
ou mesmo organizações autônomas e descentralizadas baseadas em uma cadeia de blocos (OADs). 
A proposta do Ethereum é prover uma cadeia de blocos com uma linguagem de programação 
Turing-completa nativa, que pode ser usada para criar "contratos" capazes de registrar funções 
arbitrárias de transição de estado, permitindo aos usuários criar 
qualquer um dos sistemas descritos anteriormente, bem como outros sistemas que nós não
tenhamos sequer imaginado, simplesmente escrevendo sua lógica em poucas linhas de código.


### Sumário

* [Introdução ao Bitcoin e Conceitos Relevantes](#introduction-to-bitcoin-and-existing-concepts)
    * [História](#history)
    * [Bitcoin Como Um Sistema de Transição de Estados](#bitcoin-as-a-state-transition-system)
    * [Mineração](#mining)
    * [Árvores de Merkle](#merkle-trees)
    * [Aplicações Alternativas para Blockchain](#alternative-blockchain-applications)
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
ideal, pois dependia de computação confiável como *backend*. Em 2009, pela 
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

### Bitcoin Como Um Sistema de Transição de Estados

    FIGURA

Do ponto de vista técnico, o livro-contábil de uma criptomoeda como o Bitcoin 
pode ser imaginado como um sistema de transição de estados, no qual se encontra
um "estado" que consiste no status da propriedade de todos os Bitcoin existentes
e uma "função de transição de estado" que recebe um estado e uma transação e 
exibe um novo estado como resultado. Em um sistema bancário comum, por exemplo,
esse estado é o balancete, uma transação é a requisição para movimentar `$X` de `A` 
para `B` e a função de transição de estado deduz `$X` o valor da conta de `A` e 
incrementa o valor da conta de `B` em `$X`. Em primeiro lugar, se a conta de `A` é 
menor do que `$X`, a função de transição de estado retorna um erro. Portanto, 
podemos definir:

    SUBMETER(S,TX) -> S' ou ERRO

No sistema bancário definido acima:

    SUBMETER({ Alice: $50, Bob: $50 },"enviar $20 de Alice para Bob") = { Alice: $30, Bob: $70 }

No entanto:

    SUBMETER({ Alice: $50, Bob: $50 },"enviar $70 de Alice para Bob") = ERRO 
    
O "estado" no Bitcoin é o conjunto de todas as moedas que foram mineradas, porém 
ainda não gastas (tecnicamente, "as saídas transacionais não-gastas", na sigla
em inglês, UTXO - *Unspent Transaction Outputs*). Cada UTXO possui uma denominação 
e um proprietário (definido por um endereço de 20 bytes que basicamente é uma 
chave criptográfica pública). A transação contém uma ou mais entradas, que por sua 
vez contêm uma referência para uma UTXO existente e uma assinatura criptográfica 
produzida por uma chave privada associada ao endereço de proprietário, e uma ou 
mais saídas, que por sua vez contêm uma nova UTXO a ser adicionada ao estado.

A função de transição de estado `SUBMETER(S,TX) -> S'` pode ser, *grosso modo*, 
definida da seguinte forma:

1. Para cada entrada em `TX`:
    * Se a UTXO referenciada não pertence a `S`, retorne um erro.
    * Se a assinatura fornecida não é compatível com a assinatura do proprietário da UTXO, retorne um erro.
2. Se a soma das denominações de todas as entradas da UTXO é menor do que a soma das denominações de todas as saídas da UTXO, retorne um erro.
3. Retornar `S'` com todas as entradas da UTXO removidas e todas as saídas da UTXO adicionadas.

A primeira metade do primeiro passo previne que o remetente da transação gaste
moedas que não existem. A segunda metade do primeiro passo previne que o 
remetente da transação gaste moedas alheias. O segundo passo força a 
conservação de valores. Visando pagamentos, o protocolo funciona da seguinte forma:
suponha que Alice queira enviar BTC 11,7 para Bob. Primeiramente, Alice buscará
um conjunto de UXTOs disponíveis que ela possua, cujo total é de pelo menos BTC 11,7.
Realisticamente, Alice não terá exatamente BTC 11,7; então digamos que a menor 
quantidade que ela pode ter seria `6+4+2=12`. Então, ela cria uma transação com essas 3 entradas e 2 saídas.
A primeira saída será de BTC 11,7 com endereço de Bob como proprietário e a 
segunda saída será o "troco" com os BTC 0,3 restantes. Se Alice não solicitar que o troco seja enviado 
para um endereço seu, então o minerador poderá ficar com esse valor restante.



https://github.com/ethereum/wiki/wiki/White-Paper#bitcoin-as-a-state-transition-system