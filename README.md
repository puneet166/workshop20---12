### [ Overview ](#over)
  * [About Full node](#fullnode)
  * [About Validator node](#vNode)
  * [About Orchestrator](#Orchestrator)
  * [About Eth](#Eth)
  * [About Smart contracts](#SC)
### [ Prequiste ](#pre)
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
##  Prequiste
* Redhat Machine with config---
* installed git.
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
* this will start a testchain with one validator.
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
* Now deploy gravity contract and save it in contract file in our home directory. (something missing here.).
* You have to change ``` COSMOS-RPC ``` ``` ex: http://localhost:26657 ``` , ``` ETH-RPC ``` ``` ex: http://"Your-eth-testchain-IP":8545 ``` endpoints and your ``` ETH_PRIVATE_KEY ``` accordingly.
``` npx ts-node \
  contract-deployer.ts \
   --cosmos-node="$COSMOS-RPC" \
   --eth-node="$ETH-RPC" \
   --eth-privkey="$ETH_PRIVATE_KEY" \
   --contract=artifacts/contracts/Gravity.sol/Gravity.json \
   --test-mode=false > $HOME/contracts
```
example - its missing.
* You can check the contract information using ``` cat $HOME/contracts ``` . make sure run this command from your root/base directory.<br>
<b> NOTE </b> - Save these information safe you'll need them to start the orchestrator.
<a name="step1.4"></a>
### Start the orchestrator
* abc1
* abc2
<a name="step1.5"></a>
### Important Notes
* abc1
* abc2




<a name="step2"></a>
## Join a gravity testchain with one validator and one orchestrator

<a name="step2.1"></a>
### Start a full Node
* abc1
* abc2
<a name="step2.2"></a>
### Make full node a validator node
* abc1
* abc2
<a name="step2.3"></a>
### Start orchestrator
* abc1
* abc2
<a name="step2.4"></a>
### Important Notes
* abc1
* abc2

<a name="step4"></a>
## Launch your own etherum network

sometext

<a name="step3"></a>
## Testing deployed Network

sometext


