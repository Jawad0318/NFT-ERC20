#sample ERC-721 Token NFT Project
To setup a Hardhat project, Open up a terminal and execute these commands

```shell
mkdir NFT-Tutorial
cd  NFT-Tutorial
npm init --yes
npm install --save-dev hardhat @nomicfoundation/hardhat-toolbox
```

In the same directory where you installed Hardhat run:

```shell
npx hardhat
```

Let's install some OpenZeppelin contracts so we can get access to the ERC-721 contracts. In your terminal, execute the following command
Compile the contract, open up a terminal and execute these commands

```shell
npx hardhat compile
```

Let's deploy the contract to goerli test network. To do this, we'll write a deployment script and then configure the network. First, create a new file/replace the default file named deploy.js under the scripts folder, and write the following code there:

check out the code in the repository for more understanding
