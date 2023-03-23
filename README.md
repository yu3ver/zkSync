# zkSync Era - деплой смарт-контракта

![zkSync Era - деплой смарт-контракта](https://miro.medium.com/v2/resize:fit:720/format:webp/0*5zGUwCCEO86p2dSw.jpeg)

Гайд актуален, советуем в ZkSync на своих кошельках задеплоить несколько смарт-контрактов + Добавили видео-гайд по деплою. Подробный гайд как деплоить смарт-контракт на любой платформе (MacOs, Windows) без использования серверов.

zkSync — ZK rollup, надежный протокол, который использует криптографические доказательства достоверности для обеспечения масштабируемых и недорогих транзакций в Ethereum.

Недавно вышла новость о том, что zkSync перенесли старт на Q1-Q2 2023 года. Поэтому нужно поспешить успеть поактивничать кто ещё этого не сделал.

Для начала рекомендуем потестировать протокол в основной сети. Детали мы расписали в гайде 👇


Testnet zkSync — время проявить активность еще есть! Ждем Retrodrop

    Обязательно подпишись на нас в Telegram мы публикуем там больше возможностей и отвечаем в чате на все вопросы. Так же, мы постоянно проводим розыгрыши в Discord

В этой статье мы будем деплоить смарт-контракт на любой платформе (MacOs, Windows) без использования серверов.

    Для начала качаем (или запускаем) VSC code — https://code.visualstudio.com/, с установкой проблем не должно быть.

2. Добавляем в свой MetaMask сеть zkSync ERA — [https://chainlist.org](https://chainlist.org/?search=zkSync+Era+test&testnets=true)

![Добавляем в свой MetaMask сеть zkSync ERA](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*xPvjJFn303Aoa_8njh1B7Q.png)

![Добавляем в свой MetaMask сеть zkSync ERA](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*83jcPCOan_o6LI9x7FpbCw.png)

3. Чтобы потом не ждать, пока будем разбираться с кодом, запрашиваем тестовые токены, до момента деплоя они как раз должны прийти на MetaMask.

Запрашиваем токены тут — https://goerli.portal.zksync.io/faucet


![Запрашиваем токены](https://miro.medium.com/v2/resize:fit:640/format:webp/1*D6aJSu22ZQZWUsw0x-jSSw.png)

![Запрашиваем токены](https://miro.medium.com/v2/resize:fit:640/format:webp/1*CkKbv_ZnMny1AXRc-_L96A.png)


Если не хватает токенов для комиссии, то можно взять закинуть с сети goerli — https://goerli.portal.zksync.io/bridge

![Бридж токенов](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*Rz-ni2MCvhHvk1agZGqXRQ.png)

4. Также нам понадобится [Node.Js](https://nodejs.org/en), заходим на сайт Node.js, качаем и устанавливаем(просто кликайте далее при установке), после чего заходим в VSC code, и закрываем его.

![Node.Js](https://miro.medium.com/v2/resize:fit:720/format:webp/1*NwevlCwf_a-xf6rBCZODng.png)

5. Создаём на рабочем столе папку, назовём её “ZkSync” для удобства. После чего заходим в VSC code который мы скачали и открываем там нами созданную папку.

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*m7YVp4Bu9eagp_WTlxmvxw.png)

6. И начинаем вводить в терминале(снизу) команды(если терминал не отображается, тянем за синюю полоску):

![терминал](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*wCA6yJKYO2Xh0rgIy4FeWw.png)

![терминал](https://user-images.githubusercontent.com/1020509/227019034-1af6cdfe-3fb5-41af-a266-8bad98d2c5bc.png)


```jsx
npm init --y
npm install
npm add -D install --save-dev hardhat
npx hardhat
```

Выбираем Create a TypeScript project, затем “Enter” и несколько раз “У”. После чего продолжаем вводить команды:

```jsx
mkdir greeter
cd greeter
npm install
npm init -y
npm add -D i typescript
npm add -D i ts-node
npm add -D i @types/node
npm add -D i ethers@^5.7.2
```

Просто вставляйте команды по одной ничего не меняя, продолжаем:

```jsx
cd ..
npm add -D i zksync-web3@^0.13.4
cd greeter
npm add -D i @ethersproject/hash
npm add -D i @ethersproject/web
npm add -D i @matterlabs/hardhat-zksync-solc
npm add -D i @matterlabs/hardhat-zksync-deploy
```

Создаём папку с названием как на скрине “hardhat.config.ts” в папке “greeter”:  

![hardhat.config.ts](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*cFZ1_XOTDHom_VqGFGSxsA.png)


И в этот файл вставляем данный код и сохраняем CTRL+S:

```jsx
import "@matterlabs/hardhat-zksync-deploy";
import "@matterlabs/hardhat-zksync-solc";

module.exports = {
  zksolc: {
    version: "1.3.1",
    compilerSource: "binary",
    settings: {},
  },
  defaultNetwork: "zkTestnet",
  networks: {
    zkTestnet: {
      url: "https://zksync2-testnet.zksync.dev", // URL of the zkSync network RPC
      ethNetwork: "goerli", // Can also be the RPC URL of the Ethereum network (e.g. https://goerli.infura.io/v3/<API_KEY>)
      zksync: true,
    },
  },
  solidity: {
    version: "0.8.17",
  },
};
```

![hardhat-zksync-deploy](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*Rmchjs1cpmE2ZZ58PaXI2g.png)

После чего продолжаем в ТЕРМИНАЛ вставлять дальше команды:

```jsx
mkdir contracts
mkdir deploy
```

Дальше, в папке “greeter” открываем папку “contracts” и создаем файл под названием “Greeter.sol” и вставляем туда код(и смотрим на подсказку скрин ниже):

```jsx
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.0;

contract Greeter {
    string private greeting;

    constructor(string memory _greeting) {
        greeting = _greeting;
    }

    function greet() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _greeting) public {
        greeting = _greeting;
    }
}
```

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*YMuIXdWA-qFyvOlpzk0SvQ.png)

И выполняем в ТЕРМИНАЛЕ команду:

```jsx
npx hardhat compile
```

И видим как на скрине “Successfully compiled 1 Solidity file” - значит всё делаем правильно. Дальше, в папке “greeter” открываем папку “deploy” и создаем файл под названием “deploy.ts” и вставляем туда код:


![](https://miro.medium.com/v2/resize:fit:640/format:webp/1*A7VrZe6oTqulVCOi5TVF_w.png)


```jsx
import { utils, Wallet } from "zksync-web3";
import * as ethers from "ethers";
import { HardhatRuntimeEnvironment } from "hardhat/types";
import { Deployer } from "@matterlabs/hardhat-zksync-deploy";

// An example of a deploy script that will deploy and call a simple contract.
export default async function (hre: HardhatRuntimeEnvironment) {
  console.log(`Running deploy script for the Greeter contract`);

  // Initialize the wallet.
  const wallet = new Wallet("<WALLET-PRIVATE-KEY>");

  // Create deployer object and load the artifact of the contract we want to deploy.
  const deployer = new Deployer(hre, wallet);
  const artifact = await deployer.loadArtifact("Greeter");

  // Deposit some funds to L2 in order to be able to perform L2 transactions.
  const depositAmount = ethers.utils.parseEther("0.001");
  const depositHandle = await deployer.zkWallet.deposit({
    to: deployer.zkWallet.address,
    token: utils.ETH_ADDRESS,
    amount: depositAmount,
  });
  // Wait until the deposit is processed on zkSync
  await depositHandle.wait();

  // Deploy this contract. The returned object will be of a `Contract` type, similarly to ones in `ethers`.
  // `greeting` is an argument for contract constructor.
  const greeting = "Hi there!";
  const greeterContract = await deployer.deploy(artifact, [greeting]);

  // Show the contract info.
  const contractAddress = greeterContract.address;
  console.log(`${artifact.contractName} was deployed to ${contractAddress}`);

  // Call the deployed contract.
  const greetingFromContract = await greeterContract.greet();
  if (greetingFromContract == greeting) {
    console.log(`Contract greets us with ${greeting}!`);
  } else {
    console.error(`Contract said something unexpected: ${greetingFromContract}`);
  }

  // Edit the greeting of the contract
  const newGreeting = "Hey guys";
  const setNewGreetingHandle = await greeterContract.setGreeting(newGreeting);
  await setNewGreetingHandle.wait();

  const newGreetingFromContract = await greeterContract.greet();
  if (newGreetingFromContract == newGreeting) {
    console.log(`Contract greets us with ${newGreeting}!`);
  } else {
    console.error(`Contract said something unexpected: ${newGreetingFromContract}`);
  }
}
```

После вставки кода в нее нужно вставить приватный ключ от МетаМаска с тестовыми токенами, чтобы выглядело так: const wallet = new Wallet(“4362462424624624”);), смотрим пример:

![](https://miro.medium.com/v2/resize:fit:4800/format:webp/1*dZvGKDwGsIGxsTvKEOTHaA.png)

После чего запускаем последнюю команду в ТЕРМИНАЛЕ и почти заканчиваем деплой

```jsx
npx hardhat deploy-zksync
```

На этом все, немного ждем и получаем такой вывод:

После этого можно пойти в эксплорер и увидеть транзакции, т.к. после команды деплоя сразу происходит еще и взаимодействие с контрактом https://goerli.explorer.zksync.io/

Если вы занимаетесь мультиаккингом, чтобы не делать на каждом аккаунте новые пункты, просто заменяем ПРИВАТНЫЙ КЛЮЧ метамаска и вставляем последнюю команду в консоли выше.

ВСЕМ СПАСИБО, хорошего вам деплоя.
