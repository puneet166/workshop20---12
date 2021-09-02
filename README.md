### [ Overview ](#over)
  * [About Full node](#fullnode)
  * [About Validator node](#vNode)
  * [About Orchestrator](#Orchestrator)
  * [About Eth](#Eth)
  * [About Smart contracts](#SC)
### [Prerequisite](#pre)
  * [Install all dependencies before deploy testchain](#installD)
### [Running with one validator, orchestrator and etherum node](#step1)
  * [To start your test chain with one validator](#step1.1)
  * [To run/launch Ethereum node](#step1.2)
  * [Deploy the smart contract](#step1.3)
  * [Start the orchestrator](#step1.4)
  * [Important Notes](#step1.5)
### [Join a gravity testchain with one validator and one orchestrator](#step2)
  * [Start a full Node](#step2.1)
  * [Make full node a validator node](#step2.2)
  * [Start orchestrator](#step2.3)
  * [Important Notes](#step2.4)

### [Launch your own etherum network](#step4)
  * [Start a ethereum testchain](#step4.1)
  * [Add any node as a peer-node in this network](#step4.2)
  * [Start a ethereum testchain full-node](#step4.3)
  
### [Testing deployed Network](#step3)




<a name="over"></a>
##  Overview
<a name="fullnode"></a>
### About full node
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in £1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal.

<a name="vNode"></a>
### About Validator node
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in £1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal.

<a name="Orchestrator"></a>
### About Orchestrator
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in £1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal.

<a name="Eth"></a>
### About Eth
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in £1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal.

<a name="SC"></a>
### About Smart contracts
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in £1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal.

<a name="pre"></a>
##  Prerequisite
* Redhat Machine with config---
* Installed git.
<a name="installD"></a>
### Install all dependencies before deploy testchain
* Clone repo in your Redhat machine.
* Come in ``` repoName(market)/deploy/redhat-testchain-deployment ```.
* To install dependencies please run the bin.sh script with administrator privilege using ``` sudo bash bin.sh ```
<a name="step1"></a>
## Running with one validator, orchestrator and etherum node
<a name="step1.1"></a>
### To start your test chain with one validator
* For stating test chain with one validator use init.sh file which is present in ``` /deploy/redhat-testchain-deployment/master-validator ``` .
* Run this command ``` bash init.sh ``` in ``` market/deploy/redhat-testchain-deployment/master-validator ```.
* This will start a testchain with one validator.
<a name="step1.2"></a>
### To run/launch Ethereum node
#### There is two ways to run/launch ethereum node.
1. For launch eth node with rinkeby network.
    * Open new terminal or use screen command like screen -S {Name of screen}.
    * Run this command ``` geth --rinkeby --syncmode "light" --rpc --rpcport "8545" ``` .
    * Wait 2-4 min. it will syncing of block.
2. For launch your own etherum network.
    * Now we will start a Ethereum testchain with our validator's Ethereum private-key. To start the Ethereum testchain follow this [Launch your own etherum network](#step4) ,copy the ETHGensis file present in $HOME/market/deploy/redhat-testchain-deployment/assests in your machine to machine in which you want to start Ethereum testchain.

<a name="step1.3"></a>
### Deploy the smart contract
* first open the folder where contracts are placed ``` cd $HOME/gravity/solidity ``` $HOME is root directory in my cases.
* Now deploy gravity contract and save it in contract file in our home directory.
* You have to change ``` COSMOS-RPC ``` ``` ex: http://localhost:26657 ``` , ``` ETH-RPC ``` ``` ex: http://"Your-eth-testchain-IP":8545 ``` endpoints and your ``` ETH_PRIVATE_KEY ``` accordingly.
``` npx ts-node \
  contract-deployer.ts \
   --cosmos-node="$COSMOS-RPC" \
   --eth-node="$ETH-RPC" \
   --eth-privkey="$ETH_PRIVATE_KEY" \
   --contract=artifacts/contracts/Gravity.sol/Gravity.json \
   --test-mode=false > $HOME/contracts
```
* You can check the contract information using ``` cat $HOME/contracts ``` . make sure run this command from your root/base directory.<br>
<b> NOTE </b> - Save these information safe you'll need them to start the orchestrator.
<a name="step1.4"></a>
### Start the orchestrator
* You have to edit the ``` cosoms-phrase ```, ``` COSMOS-GRPC ex: http://localhost:9090 ```,``` ETH-RPC ex: http://"Your-eth-testchain-IP":8545 ```, ``` ethereum- key and gravity-contract-address ``` accordingly.
* <b> NOTE - </b> Make sure this ethereum account have some ether.
```
    gbt orchestrator \
         --cosmos-phrase="YOUR_ORCHESTRATOR_MNEMONIC" \
         --cosmos-grpc="$cosmos-grpc" \
         --ethereum-key="$ethereum-key" \
         --ethereum-rpc="$ethereum-rpc" \
         --fees="1stake" \
         --gravity-contract-address="0x330122273ffF8A31E8B5EAF2099cbFF881c9eEB7"
```
<b> NOTE - Now your testchain is up and running with one validator, orchestrator and etherum node. </b>
<a name="step1.5"></a>
### Important Notes
* Your Gravity directory will be named as per your testchain name.
* You can find all required information regarding validator, orchestrator and ethereum inside that folder.
* Folder structure is ``` ~/"YOUR-TESTCHAIN-NAME"/gravity ```
* You have to pass some basic information to the other validators so that they can join your testchain.
    * Testchain Name.
    * Your node-id. You can get using this command ``` gravity $GRAVITY_HOME_FLAG tendermint show-node-id ```.
    * Your orchestrator ``` mnemonic ``` (We are passing this mnemonic so that the next validator can have some token from us to start testing,        this can be changed in future by using faucet to provide tokens).
    * Your machine ``` public ip ``` on which testchain is hosted.
    * Deployed ``` Gravity-contract address ```.
    * If you have your own etherum testnet then ``` ETHGenesis.json ``` file and ``` machine-public-ip ``` which you have used to start        the ethereum testchain network.
    * Ethereum-RPC address.
    * Make sure following port open ``` 26657/tcp 26656/tcp 9090/tcp 1317/tcp 8545/tcp 30303/tcp 30303/udp ``` .
    * GRAVITY-RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":26657 ```
    * GRVAITY_GRPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":9090 ```
    * ETHEREUM_RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":8545 ```

<a name="step2"></a>
## Join a gravity testchain with one validator and one orchestrator

<a name="step2.1"></a>
### Start a full Node
* First, we have to join the testchain as a full node.
* Run the following .sh file to start a full node.
* To run this script you require ``` node-id ``` and ``` ip ``` of any validator of the chain to add it as a seed to connect to.<br>
``` bash init.sh ```
* Now we have a full node connected to testchain and syncing, but still this node is not a validator node. If you want to make it a vaidator wait for it to get completely synced with the chain then follow below steps.

<a name="step2.2"></a>
### Make full node a validator node
* To make this node a validator node we have to perform a create-validator transaction.

* Run the ``` makeValidator.sh ``` shell script present at ``` /deploy/redhat-testchain-deployment/peer-validators ``` to make this node a validator.
* To run this script you need a ``` mnemonic ``` of any orchestrator from the chain so that some tokens can be transffered to your validator. <br>
``` bash makeValidator.sh ```
* If everything goes well you will see the orchestrator key as output as well as the transactions. Then it will ask you to confirm the create-validator transaction and as soon as you confirm it a transaction log is generated and your full node will become a validator in chain.
* To confirm whether you have joined the testchain as a validator or not go the ``` "GRAVITY-RPC"/validators ``` on any browser and you can find your validator-address in the validtor-set.



<a name="step2.3"></a>
### Start orchestrator
* Now we have to start an orchestrator.
* first we have to generate some delegator keys <br>
 ``` gbt init
gbt keys register-orchestrator-address --validator-phrase "$YOUR_VALIDATOR_MNEMONIC" --fees=1footoken 
```
* It will generate a ``` cosmos address, mnemonic, an ethereum address and it's private key ```. Please save these information safe because we are going to use these in future as our delegator.
* Now you have to fund some tokens to you delegator for that run the following command. <br>
``` gravity --home YOUR_GRAVITY_DATA_DIR tx bank send $(gravity --home YOUR_GRAVITY_DATA_DIR keys show -a orch --keyring-backend test) $YOUR_DELEGATOR_COSMOS_ADDRESS 1000000stake --chain-id testchain --keyring-backend test -y

gravity --home YOUR_GRAVITY_DATA_DIR tx bank send $(gravity --home YOUR_GRAVITY_DATA_DIR keys show -a orch --keyring-backend test) $YOUR_DELEGATOR_COSMOS_ADDRESS 1000000footoken --chain-id testchain --keyring-backend test -y
```
* Now you have to start a ethereum full node for the running ethereum testchain, if you want to go with rinkeby ``` geth --rinkeby --syncmode "light" --rpc --rpcport "8545" ``` or to start with your own etherum testchain follow this [Launch your own etherum network](#step4) then only move to next step.
* You also have to fund some tokens to the generated Eth-account, you can use metamask for this purpose.
* Now, run the following command to start orchestrator.
* You have to edit the ``` cosoms-phrase, cosmos-grpc ex: http://localhost:9090, ethereum-rpc ex: http://"Your-eth-testchain-IP":8545, ethereum-key and gravity-contract-address ``` accordingly.
```
gbt orchestrator \
        --cosmos-phrase="the-mnemonic-of-delegator-which-you-have-saved" \
        --cosmos-grpc="$cosmos-grpc" \
        --ethereum-key="private-key-of-the-delegator-which-you-have-saved" \
        --ethereum-rpc="$ethereum-rpc" \
        --fees="1stake" \
        --gravity-contract-address="0x330122273ffF8A31E8B5EAF2099cbFF881c9eEB7"
```

<a name="step2.4"></a>
### Important Notes
* Your Gravity directory will be named as per your testchain name.
* You can find all required information regarding validator, orchestrator and ethereum inside that folder.
* This is "YOUR_GRAVITY_DATA_DIR" ``` ~/"YOUR-TESTCHAIN-NAME"/gravity ```
* GRAVITY-RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":26657 ```
* GRVAITY_GRPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":9090 ```
* ETHEREUM_RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":8545 ```



 

<a name="step4"></a>
## Launch your own etherum network
<a name="step4.1"></a>
### Start a ethereum testchain
* You'll need the ETHGenesis.json file to start the testchain.
* Now run the following command to initialize the genesis block from where to start mining.
``` geth --identity "GravityEthereum" \
    --nodiscover \
    --networkid 15 init ETHGenesis.json
```
* Now we'll start the chain.
* Please add your ``` ETH-ADRESS ```(this address can also be found in your ETHGenesis.json file) at place of ethereum address.
``` geth --identity "GravityEthereum" --nodiscover \
                               --networkid 15 \
                               --mine \
                               --http \
                               --http.port "8545" \
                               --http.addr "0.0.0.0" \
                               --http.corsdomain "*" \
                               --http.vhosts "*" \
                               --miner.threads=1 \
                               --nousb \
                               --verbosity=5 \
                               --miner.etherbase="$ETHEREUM_ADDRESS"
```
* Now your ethereum testchain is up and running.

<a name="step4.2"></a>
### Add any node as a peer-node in this network
* This node will be our admin node so we'll add peers to this node.
* attach the ``` geth.ipc ``` <br>
```
geth attach ~/.ethereum/geth.ipc
```
* Use the ``` enode ``` to add any node as peer-node, update ``` enode ``` and ``` ip ``` accordingly.<br>
```
admin.addPeer("enode://26f7b8...92e@[$ip]:30303?discport=0")
```





<a name="step4.3"></a>
### Start a ethereum testchain full-node
* Use the same ``` ETHGenesis.json ``` file which you have used to start the testchain.
* Now run the following command to initialize the genesis block from where to start mining. <br>
```
geth --identity "GravityEthereum" --networkid 15 init ETHGenesis.json
```
* Start the testchain and save logs to a file. <br>
```
geth --rpc --rpcport "8545" --networkid 15 console 2>> myEth2.log
```
* Now we have to attach the geth.ipc. <br>
```
geth attach ~/.ethereum/geth.ipc
```
* Now view the enode info with following command.
```
admin.nodeInfo.enode
```
* Send this ``` enode ``` and your ``` MACHINE_PUBLIC_IP ``` to the master so that this node can be added as a peernode.
* Check whether you are added as peer-node or not in the testchain by running the following command in ``` geth.ipc ```. <br>
```
admin.peers
```











<a name="step3"></a>
## Testing deployed Network or Gravity
Now that we've made it this far it's time to actually play around with the bridge.
* This first command will send some ERC20 tokens to an address of your choice on the Gravity testchain.
* Notice that the Ethereum key is pre-filled. This address has both some test ETH and a large balance of ERC20 tokens from the contracts     listed here.
```
0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 - ERC20A
0x63c8eA8431ED11c0c5c4bD5BBb312bA76b07EF46 - ERC20B
0x6c3A3437fe6966973901Db5429d7FD520f99F13a - ERC20C
```
* Note that the 'amount' field for this command is now in whole coins rather than wei like the previous testnets

``` 
gbt client eth-to-cosmos \
        --ethereum-key "0xb1bab011e03a9862664706fc3bbaa1b16651528e5f0e7fbfcbfdd8be302a13e7" \
        --gravity-contract-address "0xFA2f45c5C8AcddFfbA0E5228bDf7E8B8f4fD2E84" \
        --token-contract-address "any of the three values above" \
        --amount=100 \
        --destination "any Cosmos address, I suggest your delegate Cosmos address"
        --ethereum-rpc "http://"Your-eth-testchain-IP":8545"
```
* You should see a message like this on your Orchestrator. The details of course will be different but it means that your Orchestrator has observed the event on Ethereum and sent the details into the Cosmos chain!
```
[2021-08-17T06:13:37Z INFO  orchestrator::ethereum_event_watcher] Oracle observed batch with nonce 1, contract 0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687, and event nonce 3
```
* Once the event has been observed we can check our balance on the Cosmos side. We will see some peggy tokens in our balance. We have a good bit of code in flight right now so the module renaming from 'Peggy' to 'Gravity' has been put on hold until we're feature complete.

```
althea query bank balances <any cosmos address>
```
Now that we have some tokens on the Althea chain we can try sending them back to Ethereum. Remember to use the Cosmos phrase for the address you actually sent the tokens to. Alternately you can send Cosmos native tokens with this command.

The denom of a bridged token will be

```
gravity0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 

``` 


```
gbt client cosmos-to-eth \
         --cosmos-phrase "the phrase containing the Gravity bridged tokens (delegate keys mnemonic)" 
         --amount 5000000000000gravity0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 
         --fees 100footoken 
         --eth-destination "any eth address, try your delegate eth address"
```

* You should see a message like this on your Orchestrator. The details of course will be different but it means that your Orchestrator has observed the event on Ethereum and sent the details into the Cosmos chain! <br>

``` 

[2021-08-17T07:28:09Z INFO  orchestrator::ethereum_event_watcher] Oracle observed deposit with sender 0xBf660843528035a5A4921534E156a27e64B231fE, destination cosmos1w049un5qc6c7466lxllf89mhpfnzkl3d2l9epm, amount 100000000000000000000, and event nonce 4

```









