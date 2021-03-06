# How to launch test-network

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

### [ Overview ](#over)
  * [About Full node](#fullnode)
  * [About Validator node](#vNode)
  * [About Orchestrator](#Orchestrator)
  * [About Eth](#Eth)
  * [About Smart contracts](#SC)




<a name="pre"></a>
##  Prerequisite

<br />

* Redhat Machine with config--- <br /> <br />
* Installed git.  <br /> <br />
<a name="installD"></a>
### Install all dependencies before deploy testchain <br />  <br /> 
 
* Clone repo in your Redhat machine.  <br /> <br />
* Come in ``` repoName(market)/deploy/redhat-testchain-deployment ```.  <br /> <br />
* To install dependencies please run the bin.sh script with administrator privilege using ``` sudo bash bin.sh ```  <br /> <br />
<a name="step1"></a>
## Running with one validator, orchestrator and etherum node <br /> <br />
<a name="step1.1"></a>
### To start your test chain with one validator <br /> <br />
* For stating test chain with one validator use init.sh file which is present in ``` /deploy/redhat-testchain-deployment/master-validator ``` . <br /> <br />
* Run this command ``` bash init.sh ``` in ``` market/deploy/redhat-testchain-deployment/master-validator ```. <br /> <br />
* This will start a testchain with one validator. <br /> <br />
<a name="step1.2"></a>
### To run/launch Ethereum node <br /> <br />
#### There is two ways to run/launch ethereum node. <br /> <br />
1. For launch eth node with rinkeby network. <br /> <br />
    * Open new terminal or use screen command like screen -S {Name of screen}. <br /> <br />
    * Run this command ``` geth --rinkeby --syncmode "light" --rpc --rpcport "8545" ``` . <br /> <br />
    * Wait 2-4 min. it will syncing of block. <br /> <br />
2. For launch your own etherum network. <br /> <br />
    * Now we will start a Ethereum testchain with our validator's Ethereum private-key. To start the Ethereum testchain follow this [Launch your own etherum network](#step4) ,copy the ETHGensis file present in $HOME/market/deploy/redhat-testchain-deployment/assests in your machine to machine in which you want to start Ethereum testchain. <br /> <br />

<a name="step1.3"></a>
### Deploy the smart contract <br /> <br />
* first open the folder where contracts are placed ``` cd $HOME/gravity/solidity ``` $HOME is root directory in my cases. <br /> <br />
* Now deploy gravity contract and save it in contract file in our home directory. <br /> <br />
* You have to change ``` COSMOS-RPC ``` ``` ex: http://localhost:26657 ``` , ``` ETH-RPC ``` ``` ex: http://"Your-eth-testchain-IP":8545 ``` endpoints and your ``` ETH_PRIVATE_KEY ``` accordingly. <br /> <br />
``` npx ts-node \
  contract-deployer.ts \
   --cosmos-node="$COSMOS-RPC" \
   --eth-node="$ETH-RPC" \
   --eth-privkey="$ETH_PRIVATE_KEY" \
   --contract=artifacts/contracts/Gravity.sol/Gravity.json \
   --test-mode=false > $HOME/contracts
``` 
<br /> 

* You can check the contract information using ``` cat $HOME/contracts ``` . make sure run this command from your root/base directory. <br /> <br />
<b> NOTE </b> - Save these information safe you'll need them to start the orchestrator. <br /> <br />
<a name="step1.4"></a>
### Start the orchestrator <br /> <br />
* You have to edit the ``` cosoms-phrase ```, ``` COSMOS-GRPC ex: http://localhost:9090 ```,``` ETH-RPC ex: http://"Your-eth-testchain-IP":8545 ```, ``` ethereum- key and gravity-contract-address ``` accordingly. <br /> <br />
* <b> NOTE - </b> Make sure this ethereum account have some ether. <br /> <br />
```
    gbt orchestrator \
         --cosmos-phrase="YOUR_ORCHESTRATOR_MNEMONIC" \
         --cosmos-grpc="$cosmos-grpc" \
         --ethereum-key="$ethereum-key" \
         --ethereum-rpc="$ethereum-rpc" \
         --fees="1stake" \
         --gravity-contract-address="0x330122273ffF8A31E8B5EAF2099cbFF881c9eEB7"
```
<br />

<b> NOTE - Now your testchain is up and running with one validator, orchestrator and etherum node. </b>  <br /> <br />
<a name="step1.5"></a>
### Important Notes <br /> <br />
* Your Gravity directory will be named as per your testchain name. <br /> <br />
* You can find all required information regarding validator, orchestrator and ethereum inside that folder. <br /> <br />
* Folder structure is ``` ~/"YOUR-TESTCHAIN-NAME"/gravity ```  <br /> <br />
* You have to pass some basic information to the other validators so that they can join your testchain. <br /> <br />
    * Testchain Name. <br /> <br />
    * Your node-id. You can get using this command ``` gravity $GRAVITY_HOME_FLAG tendermint show-node-id ```.  <br /> <br />
    * Your orchestrator ``` mnemonic ``` (We are passing this mnemonic so that the next validator can have some token from us to start testing,        this can be changed in future by using faucet to provide tokens). <br /> <br />
    * Your machine ``` public ip ``` on which testchain is hosted. <br /> <br />
    * Deployed ``` Gravity-contract address ```. <br /> <br />
    * If you have your own etherum testnet then ``` ETHGenesis.json ``` file and ``` machine-public-ip ``` which you have used to start        the ethereum testchain network. <br /> <br />
    * Ethereum-RPC address. <br /> <br />
    * Make sure following port open ``` 26657/tcp 26656/tcp 9090/tcp 1317/tcp 8545/tcp 30303/tcp 30303/udp ``` .  <br /> <br />
    * GRAVITY-RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":26657 ```  <br /> <br />
    * GRVAITY_GRPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":9090 ```   <br /> <br />
    * ETHEREUM_RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":8545 ```   <br /> <br />

<a name="step2"></a>
## Join a gravity testchain with one validator and one orchestrator <br /> <br />

<a name="step2.1"></a>
### Start a full Node <br /> <br />
* First, we have to join the testchain as a full node. <br /> <br />
* Run the following .sh file to start a full node. <br /> <br />
* To run this script you require ``` node-id ``` and ``` ip ``` of any validator of the chain to add it as a seed to connect to.<br>
``` bash init.sh ```  <br /> <br />
* Now we have a full node connected to testchain and syncing, but still this node is not a validator node. If you want to make it a vaidator wait for it to get completely synced with the chain then follow below steps. <br /> <br />

<a name="step2.2"></a>
### Make full node a validator node <br /> <br />
* To make this node a validator node we have to perform a create-validator transaction. <br /> <br />

* Run the ``` makeValidator.sh ``` shell script present at ``` /deploy/redhat-testchain-deployment/peer-validators ``` to make this node a validator. <br /> <br />
* To run this script you need a ``` mnemonic ``` of any orchestrator from the chain so that some tokens can be transffered to your validator. <br /> <br />
``` bash makeValidator.sh ```   <br /> <br />
* If everything goes well you will see the orchestrator key as output as well as the transactions. Then it will ask you to confirm the create-validator transaction and as soon as you confirm it a transaction log is generated and your full node will become a validator in chain. <br /> <br />
* To confirm whether you have joined the testchain as a validator or not go the ``` "GRAVITY-RPC"/validators ``` on any browser and you can find your validator-address in the validtor-set.  <br /> <br />



<a name="step2.3"></a>
### Start orchestrator <br /> <br />
* Now we have to start an orchestrator. <br /> <br />
* first we have to generate some delegator keys <br /> <br />
 ``` gbt init
gbt keys register-orchestrator-address --validator-phrase "$YOUR_VALIDATOR_MNEMONIC" --fees=1footoken 
```
<br />

* It will generate a ``` cosmos address, mnemonic, an ethereum address and it's private key ```. Please save these information safe because we are going to use these in future as our delegator. <br /> <br />
* Now you have to fund some tokens to you delegator for that run the following command. <br /> <br />
``` gravity --home YOUR_GRAVITY_DATA_DIR tx bank send $(gravity --home YOUR_GRAVITY_DATA_DIR keys show -a orch --keyring-backend test) $YOUR_DELEGATOR_COSMOS_ADDRESS 1000000stake --chain-id testchain --keyring-backend test -y

gravity --home YOUR_GRAVITY_DATA_DIR tx bank send $(gravity --home YOUR_GRAVITY_DATA_DIR keys show -a orch --keyring-backend test) $YOUR_DELEGATOR_COSMOS_ADDRESS 1000000footoken --chain-id testchain --keyring-backend test -y
```
<br />

* Now you have to start a ethereum full node for the running ethereum testchain, if you want to go with rinkeby ``` geth --rinkeby --syncmode "light" --rpc --rpcport "8545" ``` or to start with your own etherum testchain follow this [Launch your own etherum network](#step4) then only move to next step. <br /> <br />
* You also have to fund some tokens to the generated Eth-account, you can use metamask for this purpose. <br /> <br />
* Now, run the following command to start orchestrator. <br /> <br />
* You have to edit the ``` cosoms-phrase, cosmos-grpc ex: http://localhost:9090, ethereum-rpc ex: http://"Your-eth-testchain-IP":8545, ethereum-key and gravity-contract-address ``` accordingly. <br /> <br />
```
gbt orchestrator \
        --cosmos-phrase="the-mnemonic-of-delegator-which-you-have-saved" \
        --cosmos-grpc="$cosmos-grpc" \
        --ethereum-key="private-key-of-the-delegator-which-you-have-saved" \
        --ethereum-rpc="$ethereum-rpc" \
        --fees="1stake" \
        --gravity-contract-address="0x330122273ffF8A31E8B5EAF2099cbFF881c9eEB7"
```
<br />

<a name="step2.4"></a>
### Important Notes <br /> <br />
* Your Gravity directory will be named as per your testchain name. <br /> <br />
* You can find all required information regarding validator, orchestrator and ethereum inside that folder. <br /> <br />
* This is "YOUR_GRAVITY_DATA_DIR" ``` ~/"YOUR-TESTCHAIN-NAME"/gravity ``` <br /> <br />
* GRAVITY-RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":26657 ``` <br /> <br />
* GRVAITY_GRPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":9090 ``` <br /> <br />
* ETHEREUM_RPC : ``` http://"YOUR_MACHINE_PUBLIC_IP":8545 ``` <br /> <br />



 

<a name="step4"></a>
## Launch your own etherum network <br /> <br />
<a name="step4.1"></a>
### Start a ethereum testchain <br /> <br />
* You'll need the ETHGenesis.json file to start the testchain. <br /> <br />
* Now run the following command to initialize the genesis block from where to start mining. <br /> <br />
``` geth --identity "GravityEthereum" \
    --nodiscover \
    --networkid 15 init ETHGenesis.json
```
<br />

* Now we'll start the chain. <br /> <br />
* Please add your ``` ETH-ADRESS ```(this address can also be found in your ETHGenesis.json file) at place of ethereum address. <br /> <br/>
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
<br />

* Now your ethereum testchain is up and running. <br /> <br />

<a name="step4.2"></a>
### Add any node as a peer-node in this network <br /> <br />
* This node will be our admin node so we'll add peers to this node. <br /> <br />
* attach the ``` geth.ipc ``` <br /> <br />
```
geth attach ~/.ethereum/geth.ipc
```
<br />

* Use the ``` enode ``` to add any node as peer-node, update ``` enode ``` and ``` ip ``` accordingly. <br /> <br />
```
admin.addPeer("enode://26f7b8...92e@[$ip]:30303?discport=0")
```
<br />

<a name="step4.3"></a>
### Start a ethereum testchain full-node <br /> <br />
* Use the same ``` ETHGenesis.json ``` file which you have used to start the testchain. <br /> <br />
* Now run the following command to initialize the genesis block from where to start mining. <br /> <br />
```
geth --identity "GravityEthereum" --networkid 15 init ETHGenesis.json
```
<br />

* Start the testchain and save logs to a file. <br /> <br />
```
geth --rpc --rpcport "8545" --networkid 15 console 2>> myEth2.log
```
<br />

* Now we have to attach the geth.ipc. <br /> <br />
```
geth attach ~/.ethereum/geth.ipc
```
<br />

* Now view the enode info with following command. <br /> <br />
```
admin.nodeInfo.enode
```
<br />

* Send this ``` enode ``` and your ``` MACHINE_PUBLIC_IP ``` to the master so that this node can be added as a peernode. <br /> <br />
* Check whether you are added as peer-node or not in the testchain by running the following command in ``` geth.ipc ```. <br /> <br />
```
admin.peers
```
<br />

<a name="step3"></a>
## Testing deployed Network or Gravity <br /> <br />
Now that we've made it this far it's time to actually play around with the bridge. <br /> <br />
* This first command will send some ERC20 tokens to an address of your choice on the Gravity testchain. <br /> <br />
* Notice that the Ethereum key is pre-filled. This address has both some test ETH and a large balance of ERC20 tokens from the contracts     listed here. <br /> <br />
```
0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 - ERC20A
0x63c8eA8431ED11c0c5c4bD5BBb312bA76b07EF46 - ERC20B
0x6c3A3437fe6966973901Db5429d7FD520f99F13a - ERC20C
```
<br />

* Note that the 'amount' field for this command is now in whole coins rather than wei like the previous testnets <br /> <br />

``` 
gbt client eth-to-cosmos \
        --ethereum-key "0xb1bab011e03a9862664706fc3bbaa1b16651528e5f0e7fbfcbfdd8be302a13e7" \
        --gravity-contract-address "0xFA2f45c5C8AcddFfbA0E5228bDf7E8B8f4fD2E84" \
        --token-contract-address "any of the three values above" \
        --amount=100 \
        --destination "any Cosmos address, I suggest your delegate Cosmos address"
        --ethereum-rpc "http://"Your-eth-testchain-IP":8545"
```
<br />

* You should see a message like this on your Orchestrator. The details of course will be different but it means that your Orchestrator has observed the event on Ethereum and sent the details into the Cosmos chain! <br /> <br />
```
[2021-08-17T06:13:37Z INFO  orchestrator::ethereum_event_watcher] Oracle observed batch with nonce 1, contract 0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687, and event nonce 3
```
<br />

* Once the event has been observed we can check our balance on the Cosmos side. We will see some peggy tokens in our balance. We have a good bit of code in flight right now so the module renaming from 'Peggy' to 'Gravity' has been put on hold until we're feature complete. <br /> <br />

```
althea query bank balances <any cosmos address>
```
<br />

Now that we have some tokens on the Althea chain we can try sending them back to Ethereum. Remember to use the Cosmos phrase for the address you actually sent the tokens to. Alternately you can send Cosmos native tokens with this command. <br /><br />

The denom of a bridged token will be <br /> <br />

```
gravity0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 

``` 
<br />

```
gbt client cosmos-to-eth \
         --cosmos-phrase "the phrase containing the Gravity bridged tokens (delegate keys mnemonic)" 
         --amount 5000000000000gravity0xB1b8E75893d22BC2b05b0C976FF06b4569B4a687 
         --fees 100footoken 
         --eth-destination "any eth address, try your delegate eth address"
```
<br />

* You should see a message like this on your Orchestrator. The details of course will be different but it means that your Orchestrator has observed the event on Ethereum and sent the details into the Cosmos chain! <br /> <br />

``` 

[2021-08-17T07:28:09Z INFO  orchestrator::ethereum_event_watcher] Oracle observed deposit with sender 0xBf660843528035a5A4921534E156a27e64B231fE, destination cosmos1w049un5qc6c7466lxllf89mhpfnzkl3d2l9epm, amount 100000000000000000000, and event nonce 4

```
<br />

<a name="over"></a>
##  Overview <br /> <br />
<a name="fullnode"></a>
### About full node <br /> <br />
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in ??1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal. <br /> <br />

<a name="vNode"></a>
### About Validator node <br /> <br />
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in ??1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal. <br /> <br />

<a name="Orchestrator"></a>
### About Orchestrator <br /> <br />
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in ??1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal. <br /> <br />

<a name="Eth"></a>
### About Eth <br /> <br />
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in ??1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal. <br /> <br />

<a name="SC"></a>
### About Smart contracts <br /> <br />
Get Your Free Will Today And Leave More Than A Memory. Get Yours Today! Support A Charity In Your Will And Change The Future. Request Your Offer Code Today! 503 UK Local Services. We Help 368K Children. Over 150 Years Old. Gift Aid Your Donation. UK-Based Charity. 85p in ??1 Transform Lives. Types: One-Off Donations, Monthly Donations, Give A Charity Gift, Vulnerable Child Appeal. <br /> <br />








