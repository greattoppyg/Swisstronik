**DEPLOY A SIMPLE CONTRACT USING HARDHAT**

cd $HOME
Create a folder
mkdir Swiss
cd Swiss
sudo apt-get remove -y nodejs
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash && export NVM_DIR="/usr/local/share/nvm"; [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"; [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"; source ~/.bashrc; nvm install --lts; nvm use --lts

npm install --save-dev hardhat
npm install --save-dev @nomicfoundation/hardhat-toolbox
npx hardhat
Press Enter then again Enter then y and again y
rm hardhat.config.js
nano hardhat.config.js
Now paste these things in hardhat.config.js file, also make sure to input your private key
require("@nomicfoundation/hardhat-toolbox");

module.exports = {
  solidity: "0.8.19",
  networks: {
    swisstronik: {
      url: "https://json-rpc.testnet.swisstronik.com/",
      accounts: ["0xd5..."], //Your private key starting with "0x"
    },
  },
};
Use W, A, S, D Key to move your cursor
To save this file use Ctrl+X then Y and then press Enter
cd contracts
rm Lock.sol
nano Lock.sol
Now paste these codes in the above file (Lock.sol)
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.19;

contract Swisstronik {
    string private message;

    constructor(string memory _message) payable{
        message = _message;
    }

    function setMessage(string memory _message) public {
        message = _message;
    }

    function getMessage() public view returns(string memory){
        return message;
    }
}
To save this file use Ctrl+X then Y and then press Enter
Now use the below command to compile ur contract file (Lock.sol)
npx hardhat compile
cd ..
mkdir scripts && cd scripts
nano deploy.js
Paste these codes in deploy.js file
const hre = require("hardhat");

async function main() {

  const contract = await hre.ethers.deployContract("Swisstronik", ["Hello Swisstronik!!"]);

  await contract.waitForDeployment();

  console.log(`Swisstronik contract deployed to ${contract.target}`);
}
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
To save this file use Ctrl+X then Y and then press Enter
cd
cd Swiss
npx hardhat run scripts/deploy.js --network swisstronik
