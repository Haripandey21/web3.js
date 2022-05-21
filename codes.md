
## 1. Interacting with Ganache using Web3.js 
```bash
Commands related to Web3.js

To install web3 - 
npm install --save web3

To import web3 - 
let Web3 =require("web3");

To connect with Ganache -
let web3 = new Web3(new Web3.providers.HttpProvider("HTTP://127.0.0.1:7545")); [Remember that the ganache must be running]

To get the balance of an account -
web3.eth.getBalance("paste the address of the account inside it").then(console.log);

To convert wei into ether - 
web3.eth.getBalance("paste the address of the account inside it").then(function(result) {console.log(web3.utils.fromWei(result,"ether"));})  

To transfer ether from one account to another - 
web3.eth.sendTransaction({from:"paste the address of the account inside it",to:"paste the address of the account inside it",value:web3.utils.toWei("1","ether")});4

```
## 2. Interacting with Smart Contract using Web3.js
```bash
Commands related to Web3.js

To install web3 - 
npm install --save web3

To import web3 - 
let Web3 =require("web3");

To connect with Ganache - 
let web3 = new Web3(new Web3.providers.HttpProvider("HTTP://127.0.0.1:7545")); [Remember that the ganache must be running]

To get the balance of an account -
web3.eth.getBalance("paste the address of the account inside it").then(console.log);

To convert wei into ether - 
web3.eth.getBalance("paste the address of the account inside it").then(function(result) {console.log(web3.utils.fromWei(result,"ether"));})  

To transfer ether from one account to another - 
web3.eth.sendTransaction({from:"paste the address of the account inside it",to:"paste the address of the account inside it",value:web3.utils.toWei("1","ether")});4

```
## 3. Compilation of Smart Contract using web3.js 
```bash
Compilation of Smart Contract using web3.js

solc = require("solc");
// file system - read and write files to your computer
fs = require("fs");
// web3 interface
Web3 = require("web3");
// setup a http provider
web3 = new Web3(new Web3.providers.HttpProvider("http://127.0.0.1:7545"));
// reading the file contents of the smart  contract
fileContent = fs.readFileSync("demo.sol").toString();
console.log(fileContent);
// create an input structure for my solidity compiler
var input = {
  language: "Solidity",
  sources: {
    "demo.sol": {
      content: fileContent,
    },
  },

  settings: {
    outputSelection: {
      "*": {
        "*": ["*"],
      },
    },
  },
};

var output = JSON.parse(solc.compile(JSON.stringify(input)));
console.log("Output: ", output);

ABI = output.contracts["demo.sol"]["demo"].abi;
bytecode = output.contracts["demo.sol"]["demo"].evm.bytecode.object;
console.log("Bytecode: ", bytecode);
console.log("ABI: ", ABI);


```
## 4. Deployment of Smart Contract using web3.js
```bash
solc = require("solc");

// file system - read and write files to your computer
fs = require("fs");

// ganache - local blockchain

// web3 interface
Web3 = require("web3");

// setup a http provider
web3 = new Web3(new Web3.providers.HttpProvider("http://127.0.0.1:7545"));

// reading the file contents of the smart  contract

fileContent = fs.readFileSync("demo.sol").toString();
console.log(fileContent);

// create an input structure for my solidity complier
var input = {
  language: "Solidity",
  sources: {
    "demo.sol": {
      content: fileContent,
    },
  },

  settings: {
    outputSelection: {
      "*": {
        "*": ["*"],
      },
    },
  },
};

var output = JSON.parse(solc.compile(JSON.stringify(input)));
console.log("Output: ", output);

ABI = output.contracts["demo.sol"]["demo"].abi;
bytecode = output.contracts["demo.sol"]["demo"].evm.bytecode.object;
console.log("Bytecode: ", bytecode);
console.log("ABI: ", ABI);

contract = new web3.eth.Contract(ABI);
let defaultAccount;
web3.eth.getAccounts().then((accounts) => {
  console.log("Accounts:", accounts); //it will show all the ganache accounts

  defaultAccount = accounts[0];
  console.log("Default Account:", defaultAccount);  //to deploy the contract from default Account
  contract
    .deploy({ data: bytecode })
    .send({ from: defaultAccount, gas: 470000 })
    .on("receipt", (receipt) => { //event,transactions,contract address will be returned by blockchain
      console.log("Contract Address:", receipt.contractAddress);
    })
    .then((demoContract) => {
      demoContract.methods.x().call((err, data) => {
        console.log("Initial Value:", data);
      });
    });
  
});


```
## Note : For now, we don't need to Compile and Deploy contracts using web3.js(described above)
         No need to code from scratch in web3.js ..things are getting much easier with Truffle.
         So,use " TRUFFLE "
