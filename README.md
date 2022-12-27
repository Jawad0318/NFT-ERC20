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

```shell
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

// Import the openzepplin contracts
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

// NFTee is  ERC721 signifies that the contract we are creating imports ERC721 and follows ERC721 contract from openzeppelin
contract NFTee is ERC721 {

    constructor() ERC721("NFTee", "ITM") {
        // mint an NFT to yourself
        _mint(msg.sender, 1);
    }
}
```

Compile the contract, open up a terminal and execute these commands

```shell
npx hardhat compile
```

Let's deploy the contract to goerli test network. To do this, we'll write a deployment script and then configure the network. First, create a new file/replace the default file named deploy.js under the scripts folder, and write the following code there:

```shell
// Import ethers from Hardhat package
const { ethers } = require("hardhat");

async function main() {
  /*
A ContractFactory in ethers.js is an abstraction used to deploy new smart contracts,
so nftContract here is a factory for instances of our NFTee contract.
*/
  const nftContract = await ethers.getContractFactory("NFTee");

  // here we deploy the contract
  const deployedNFTContract = await nftContract.deploy();

  // wait for the contract to deploy
  await deployedNFTContract.deployed();

  // print the address of the deployed contract
  console.log("NFT Contract Address:", deployedNFTContract.address);
}

// Call the main function and catch if there is any error
main()
  .then(() => process.exit(0))
  .catch((error) => {
    console.error(error);
    process.exit(1);
  });
```

To get your private key, you need to export it from Metamask. Open Metamask, click on the three dots, click on Account Details and then Export Private Key. MAKE SURE YOU ARE USING A TEST ACCOUNT THAT DOES NOT HAVE MAINNET FUNDS FOR THIS. Add this Private Key below in your .env file for PRIVATE_KEY variable.

```shell
QUICKNODE_HTTP_URL="add-quicknode-http-provider-url-here"

PRIVATE_KEY="add-the-private-key-here"
```

Now we would install dotenv package to be able to import the env file and use it in our config. In your terminal, execute these commands.

```shell
npm install dotenv
```

Now open the hardhat.config.js file, we would add the goerli network here so that we can deploy our contract to the Goerli network. Replace all the lines in the hardhat.config.js file with the given below lines

```shell
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config({ path: ".env" });

const QUICKNODE_HTTP_URL = process.env.QUICKNODE_HTTP_URL;
const PRIVATE_KEY = process.env.PRIVATE_KEY;

module.exports = {
  solidity: "0.8.9",
  networks: {
    goerli: {
      url: QUICKNODE_HTTP_URL,
      accounts: [PRIVATE_KEY],
    },
  },
};
```

To deploy in your terminal type:

```
npx hardhat run scripts/deploy.js --network goerli
```
