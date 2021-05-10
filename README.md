# Subindo um contrato na Tron

## 1º instalar o Tronbox e o dotenv

### mais informações sobre o tronbox estão no [site para desenvolvedores da Tron](https://developers.tron.network/docs/tron-box-user-guide)

```
npm install -g tronbox
```

#

## 2º inicializar o Tronbox

Em um diretório vazio execute o comando abaixo

```
tronbox init
```

#

## 3º Instalar o dotenv

```
npm install dotenv
```

#

## 4º Colocar o contrato no diretório contracts e importa-lo em /migrations/2_deploy_contracts.js

Será necessario instanciar o contrato no arquivo js.

Ex.:

```
var ContratoExemplo = artifacts.require("./ContratoExemplo");

module.exports = function(deployer) {
  // deployer.deploy(ContratoExemplo, "Mensagem de descricao");
};
```

#

## 5º Colocar credenciais num arquivo .env

O arquivo tronbox.js importa a chave privada para fazer o upload dos contratos na Tron.

Exemplo de arquivo .env:

```
PRIVATE_KEY_MAINNET=4E7FECCB71207B867C495B51A9758B104B1D4422088A87F4978BE64636656243
PRIVATE_KEY_SHASTA=da146374a75310b9666e834ee4ad0866d6f4035967bfc76217c5a495fff9f0d0
```

## 6º alterar o arquivo tronbox.js para usar o .env

Adicionar a linha

```
require('dotenv').config();
```

No inicio do arquivo tronbox

## 7º (Opcional) Alterar configurações do tronbox.js

Caso queira-se, pode-se mudar o limite de gasto dos contratos. Mais informações no [guia para desenvolvedores da Tron](https://developers.tron.network/docs/tron-box-contract-deployment)

#

## 8º Compilar os contratos

Execute o comando abaixo

```
tronbox compile --compile-all
```

#

## 9º Subir os contratos na rede

Execute o comando abaixo. REDE deve ser substituido pelo nome de alguma configuração já definida em tronbox.js

```
tronbox migrate --network REDE
```

ex.:

```
tronbox migrate --network shasta
```

Ao executar, será informado o endereço do contrato em base58 e em hex.

## 10º (Opcional) Recompilar e Reenviar

Caso houver alteração nos contratos será preciso recompilar e subir-los novamente. Execute os comandos abaixo. REDE deve ser substituido pelo nome de alguma configuração já definida em tronbox.js

```
tronbox compile

tronbox migrate --reset --network REDE
```
