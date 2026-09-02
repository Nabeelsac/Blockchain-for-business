## EX.NO-1: Creating a Private Blockchain
## Name : Nather Nabeel S A C
## Register number : 212224100040
## AIM: To create a Private Blockchain, add nodes, create accounts, transfer Ether into it by creating and deploying a Smart Contract.

## PROCEDURE

Install Geth Go to https://geth.ethereum.org/ Download the Windows version. During installation, select both Geth and Development Tools.
Verify Installation Run the following command in Command Prompt:
```
geth
```
Create a Private Blockchain Directory
```
mkdir go-ethereum
cd go-ethereum
```
Create Two Nodes
```
mkdir node1
mkdir node2
```
Open VS Code
```
code .
```
Create an Account for Node1
```
cd node1
geth --datadir "./data" account new
```
Save the public address and password of Node1 in info.txt. 
7. Create an Account for Node2
```
cd ..
cd node2
geth --datadir "./data" account new
```
Save the public address and password of Node2 in info.txt. Create the Genesis Block 8. Create privateblock.json Create a file named privateblock.json inside the go-ethereum directory.

Replace Chain ID with your own unique Chain ID. Verify the Chain ID using https://chainlist.org/ Replace: Initial signer address with Node1 Address First node address with Node1 Address Second node address with Node2 Address Set the balance for both nodes as: 3000000000000000000 Configure Both Nodes 9. Initialize Node1
```
cd node1
geth --datadir ./data init ../privateblock.json
```
Initialize Node2
```
cd ../node2
geth --datadir ./data init ../privateblock.json
```
Create Bootnode 11. Create Bootnode Directory
```
mkdir bnode
cd bnode
```
Generate Bootnode Key
```
bootnode -genkey boot.key
bootnode -nodekey boot.key -verbosity 7 -addr "127.0.0.1:30301"
```
Save Enode Copy the generated Enode URL and save it in info.txt. Run the Nodes
```
Start Node1
geth --datadir "./data" \
--port 30304 \
--bootnodes "enode://YOUR_ENODE_VALUE" \
--authrpc.port 8547 \
--ipcdisable \
--allow-insecure-unlock \
--http \
--http.corsdomain="https://remix.ethereum.org" \
--http.api web3,eth,debug,personal,net \
--networkid YOUR_NETWORK_ID \
--unlock YOUR_NODE1_ADDRESS \
--password password.txt \
--mine \
--miner.etherbase YOUR_NODE1_ADDRESS
```
```
Start Node2

geth --datadir "./data" \
--port 30306 \
--bootnodes "enode://YOUR_ENODE_VALUE" \
--authrpc.port 8546 \
--networkid YOUR_NETWORK_ID \
--unlock YOUR_NODE2_ADDRESS \
--password password.txt
```
## Replace:

YOUR_ENODE_VALUE → Bootnode Enode URL YOUR_NETWORK_ID → Chain ID YOUR_NODE1_ADDRESS → Node1 Address YOUR_NODE2_ADDRESS → Node2 Address Create a password.txt file inside both node1 and node2 directories and enter the respective account password.

Deploy Smart Contract 15. Open Remix IDE https://remix.ethereum.org/

Select Environment Deploy & Run Transactions Choose Custom - External HTTP Provider
Create Smart Contract Create a new file named:
```
New.sol
```
Deploy Contract Save the file and click Deploy.

Deployment The smart contract is deployed successfully on Node1 and added to the blockchain.

## PROGRAM #Genesis file privateblock.json
```
{
    "config":{
        "chainId":8515,
        "homesteadBlock": 0,
        "eip150Block": 0,
        "eip155Block": 0,
        "eip158Block": 0,
        "byzantiumBlock": 0,
        "constantinopleBlock": 0,
        "petersburgBlock": 0,
        "istanbulBlock": 0,
        "berlinBlock": 0,
        "clique": {
          "period": 5,
          "epoch": 30000
        }
    } ,
        "difficulty": "1",
        "gasLimit": "8000000",
        "extradata": "0x000000000000000000000000000000000000000000000000000000000000000003755DDF775cD4fbe6Ef347ce22a6Ed5fbe1014F0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "alloc": {
            "03755DDF775cD4fbe6Ef347ce22a6Ed5fbe1014F": { "balance": "3000000000000000000" },
            "1cBbc951bA624b48FC6aC1A2ee8B93BbCb69F9D8": { "balance": "3000000000000000000" }
        }
 
}
6 #Smart Contract New.sol

//SPDX-License-Identifier MIT
pragma solidity ^0.8.19;
contract New{
string name;
function setName(string memory _name) public {
name= _name;
}
function getName() public view returns (string memory){
return name;
}
}
```
## OUTPUT

## Deploying Transaction in Remix

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ced04d1c-9cfd-44c9-92ee-a86b0fe2022d" />

## Contract Creation Output in Command Prompt

<img width="1600" height="899" alt="image" src="https://github.com/user-attachments/assets/ece700c8-5803-45ea-ad58-8dea0caca819" />

## RESULT:
Thus, the Private Blockchain is created, nodes are added with accounts, and Ether is transferred into it by creating and deploying Smart contract successfully
