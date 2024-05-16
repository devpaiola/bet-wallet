# Carteira HD Bitcoin

Este é um projeto prático para criação de uma carteira HD (Hierarchical Deterministic) para Bitcoin, utilizando JavaScript e as bibliotecas `bip32`, `bip39` e `bitcoinjs-lib`.

## Pré-requisitos

Certifique-se de ter o Node.js instalado em sua máquina. Você pode baixá-lo em [nodejs.org](https://nodejs.org/).

## Como usar

1. Clone este repositório:

git clone https://github.com/devpaiola/bet-wallet

2. Instale as dependências:

npm install

3. Execute o script para gerar uma carteira Bitcoin HD:
 node createWallet.js

 ## Entendendo o código

O arquivo index.js contém o código para criar uma carteira Bitcoin HD. Aqui está uma visão geral do que cada parte do código faz:

    Importa as bibliotecas necessárias:

    ```
    const bip32 = require('bip32')
    const bip39 = require('bip39')
    const bitcoin = require('bitcoinjs-lib')
    ```
    Define a rede (testnet para este exemplo):

    ```
    const network = bitcoin.networks.testnet
    ```

    Define o caminho de derivação da carteira HD:

    ```
    const path = `m/49'/1'/0'/0`
    ```

    Gera um mnemônico (palavras de senha) para a semente da carteira:

    ```
    let mnemonic = bip39.generateMnemonic()
    const seed = bip39.mnemonicToSeedSync(mnemonic)
    ```

    Cria a raiz da carteira HD:

    ```
    let root = bip32.fromSeed(seed, network)
    ```

    Deriva uma conta e um nó para a chave pública e privada:

    ```
    let account = root.derivePath(path)
    let node = account.derive(0).derive(0)
    ```

    Gera o endereço Bitcoin, a chave privada e exibe-os no console:

    ```
    let btcAddress = bitcoin.payments.p2pkh({
    pubkey: node.publicKey,
    network: network,
    }).address

    console.log("Carteira gerada")
    console.log("Endereço: ", btcAddress)
    console.log("Chave privada:", node.toWIF())
    console.log("Seed:", mnemonic)
    ```

## Contribuindo
Se você quiser contribuir para este projeto e torná-lo ainda melhor, fique à vontade para abrir uma issue ou enviar um pull request.

[DIO](https://web.dio.me/)