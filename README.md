# Blockchain_homework

## Summary:

 In this homework we were asked to set up a custom testnet blockchain for our employer at ZBank, who had interest in the possibilities of what blockchain technologies could do for the company and customers together.

 I have provided step-by-step instructions on how to setup this custom network for ZBank and demonstrated a test transaction between two differemt test accounts.


 ## Instructions:

Before we get started you should decide which command tool you would be most comfortable with using, `Anaconda Prompt` or `Git Bash`, both can be used. I myself chose `Git Bash`.

* To start this project we will make sure we are in our directory that has our "Go Ethereum Tools". There we will create our two test accounts that we will demonstrate test transactions on later. We can do this by running the command `./geth --datadir node1 account new` for the first account, and `./geth --datadir node2 account new` for the second account. --If you are using Anaconda you will need to drop the `./` in the commands above.

![Creating Account 1](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating-Account1.PNG)
![Creating Account 2](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating-Account2.PNG)

* To start this project we will make sure we are in our directory that has our "Go Ethereum Tools". There we will setup our genesis by runnning the command `./puppeth`, followed by naming your network.

![Creating Network](https://github.com/RobertTroutman/Blockchain_homework/blob/main/Screeenshots/Creating%20Network.PNG)

* 