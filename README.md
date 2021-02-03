# Blockchain_homework

![BlockChain Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/blockchain.PNG)[Information-age,2019]

## Summary:

 In this homework we were asked to set up a custom testnet blockchain for our employer at ZBank, who had interest in the possibilities of what blockchain technologies could do for the company and customers together.

 I have provided step-by-step instructions on how to setup this custom network for ZBank and demonstrated a test transaction between two differemt test accounts.


 ## Instructions:

Before we get started you should decide which command tool you would be most comfortable with using, `Anaconda Prompt` or `Git Bash`, both can be used. I myself chose `Git Bash`.

### 1.
* To start this project we will make sure we are in our directory that has our "Go Ethereum Tools". There we will create our two test accounts that we will demonstrate test transactions on later. We can do this by running the command `./geth --datadir node1 account new` for the first account, and `./geth --datadir node2 account new` for the second account. --If you are using Anaconda you will need to drop the `./` in the commands above.

![Creating Account 1](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating-Account1.PNG)
![Creating Account 2](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating-Account2.PNG)

* Save the public and private keys for both accounts in a notepad. We will need this information for later. See example below.

![Save Both Account Keys!](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Save-Public-Account-Keys)

### 2.
* Once both test accounts are created we will setup our genesis block to run our network by runnning the command `./puppeth`, followed by naming your network.

![Creating Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating%20Network.PNG)

* Next, you will need to choose the `Clique (Proof of Authority)` consensus algorithm by following these steps:
    * "Configure New Genesis" by entering `2`
    * "Create New Genesis From Scratch" by entering `1`
    * "Clique - Proof-Of-Authority" by entering `2`

![Proof Of Authoriy Consensus](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Choosing-Clique-Proof-of-Authority.PNG)

* Right after, you will be asked "how many seconds should blocks take?" You can just put the default `15` seconds for this.

* The next two steps, paste BOTH public keys for both accounts that you saved earlier for "Which accounts are allowed to seal?" AND "Which accounts should be pre-funded?" Leave off the "0x" at the beginning. See example below.

* Enter `no` when you are asked to pre-fund the pre-compiled accounts.

![Accounts To Be Sealed & Pre-funded](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Selecting-Accounts-to-be-sealed-and-prefunded.PNG)

* You will need to create a chain/network ID and remember this. For example: `1234`

![Create A Network ID](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Selecting-Network-ID.PNG)

* You will be brought to the beginning. Now we will export the genesis you just created by following these steps:
    * "Manage Existing Genesis" by entering `2`
    * "Export Genesis Configuration" by entering `2`
    * Save the genesis to the current directory by pressing ENTER'
        - This will fail to create two of the files, but you only need `networkname.json`.
        - You can delete the `networkname-harmony.json` file.

![Exporting Genesis](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Exporting-Genesis.PNG)

### 3.
* Next we get to initialize the nodes to the new network! (You may need to delete the current 'geth' folder in each node before running each command)
    * `./geth --datadir node1 init networkname.json` <-- insert your network name
    * `./geth --datadir node2 init networkname.json` <-- insert your network name

![Initializing Node 1 To Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Initializing-Nodes-to-Network.PNG)
![Initializing Node 2 To Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Initializing-Nodes-to-Network2.PNG)


### 4.
Great! Now the nodes are ready to start mining blocks!

* For the first node, we will need to run the command:
    - `./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --minerthreads 1 --rpc --allow-insecure-unlock` replacing 'SEALER_ONE_ADDRESS' with the Account 1 public key, leaving off the "0x"
    - Be sure to copy/save the "enode" from the first node, you will need this for the second node to allow them to talk to each other.

![Starting Node 1](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Starting-Node-1.PNG)

* Open a second terminal to start the second node:
    - `./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock` replacing 'SEALER_TWO_ADDRESS' with the Account 2 public key, leaving off the "0x"
    - Paste the "enode" you copy/saved in place of "SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303"
    - For Example `./geth --datadir node2 --unlock "5F598a85923776f946F66d711ad98E3b84D38a07" --mine --port 30304 --bootnodes "enode://3773f47fbe7e1a477cc74ee4ee82d51e77ab4e3e672c140ed26f379a017aba3f341b88db2fda9bf48d75def84214da33e4dd64ce4ed39d3c5b509b9da3424046@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock`

![Starting Node 2](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Starting-Node-2.PNG)

* Be sure to enter your password(s) you saved to unlock each account on each node. It will prompt you for it, and you may not see it.

![Unlocked Account](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Unlocked-Account-on-Node-1.PNG)

* Fantastic! You should see both nodes producing and mining new blocks!!!

* Next, We will need to create a custom network connected to our nodes in MyCrypto.

* Open the MyCrypto app, then click `Change Network` at the bottom left, followed by selecting `+ add custom node`

* You will need to use a custom network, and include the chain ID, and use ETH as the currency.
    * Type ETH in the Currency box
    * In the Chain ID box, type the chain id you generated during genesis creation
    * In the URL box type:`http://127.0.0.1:8545`.  This points to the default RPC port on your local machine
    * Finally, click `Save & Use Custom Node`

![Setting Up Custome Node In MyCrypto](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Setup-Your-Custom-Node.PNG)

![Connected To Custom Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating-Custom-Network-in-MyCrypto.png)


* Once the custom network has been established and connect, go to your `View & Send` tab on the left of MyCrypto. There you will click on the button `Keystore File`.

![Keystore File Log-In](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Log-Into-Wallet-Using-Keystore-File-From-Node-1.png)

* Click on the "Select Wallet File", and navigate to where you saved you Keystore for Node 1.

![Select Saved Keystore](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Select-Keystore-From-Node1-Folder.png)

* Then type in your password that you saved

![Enter Saved Password](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Type-In-Password.png)

* Now that you have gained access to your account you can see your account address & balance of ETH on the right. You are able send ETH to your Account 2 address from your Account 1 address (current) by entering Account 2 address into the `To Address` bar. See example below.

![Account Balance/Sending Transaction](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Account-Balance-In-Account-1-Sending-Money-To-Account-2.png)


* A confirmatioh will appear after you hit `Send Transaction` allowing you to double-check the information of your transaction. Confirm, and hit `Send `
![Confirmation Of Information](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Confirmation.png)

* A TX Hash (Transaction Hash) will appear at the bottom after you hit `Send` allowing you to check the status of your transaction by clicking `Check TX Status`.

![Checking Status Of TX Hash](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Check-Transaction-Status-With-TX-Hash.png)

* By clicking `Check TX Status` you can see your transaction "Pending". It may take a few moments to get mined.

![Transaction Pending!](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Pending-Transaction.png)

* You can check your network of nodes to see if your transaction has successfully been mined and processed.

![Check Mining Process In Networks](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Transaction-Has-Been-Mined-And-Sealed-With-New-Block.png)

* Finally after watching your transaction being mined, you can refresh your transaction in MyCrypto, and you can see it has successfully been processed.

![Transaction Successful!](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Transaction-Successful.png)


* Congratulations, you just created a blockchain and sent a transaction!!!

![YAY! CONGRATS!!!](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Congrats.png)[Crowdfundinsider,2021]


## Sources:
[Crowdfundinsider,2021](https://www.crowdfundinsider.com/2021/01/171079-defi-tokens-like-snx-uniswaps-uni-aave-yearn-finances-yfi-are-now-also-rallying-with-bitcoin-and-ethereum-report/)

[Information-age,2019](https://www.information-age.com/five-blockchain-use-cases-123484558/)

