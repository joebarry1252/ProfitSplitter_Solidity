## 20_solidity

# Background
Your new startup has created its own Ethereum-compatible blockchain to help connect financial institutions, and the team wants to build smart contracts to automate some company finances to make everyone's lives easier, increase transparency, and to make accounting and auditing practically automatic!
Fortunately, you've been learning how to program smart contracts with Solidity! What you will be doing this assignment is creating a ProfitSplitter contract. 

Pay your Associate-level employees quickly and easily.

At the top of your contract, you will need to define the following public variables:


employee_one -- The address of the first employee. Make sure to set this to payable.


employee_two -- Another address payable that represents the second employee.


employee_three -- The third address payable that represents the third employee.


Create a constructor function that accepts:


address payable _one


address payable _two


address payable _three


Within the constructor, set the employee addresses to equal the parameter values. This will allow you to avoid hardcoding the employee addresses.
Next, create the following functions:


balance -- This function should be set to public view returns(uint), and must return the contract's current balance. Since we should always be sending Ether to the beneficiaries, this function should always return 0. If it does not, the deposit function is not handling the remainders properly and should be fixed. This will serve as a test function of sorts.


deposit -- This function should set to public payable check, ensuring that only the owner can call the function.


In this function, perform the following steps:


Set a uint amount to equal msg.value / 3; in order to calculate the split value of the Ether.


Transfer the amount to employee_one.


Repeat the steps for employee_two and employee_three.


Since uint only contains positive whole numbers, and Solidity does not fully support float/decimals, we must deal with a potential remainder at the end of this function since amount will discard the remainder during division.


We may either have 1 or 2 wei leftover, so transfer the msg.value - amount * 3 back to msg.sender. This will re-multiply the amount by 3, then subtract it from the msg.value to account for any leftover wei, and send it back to Human Resources.






Create a fallback function using function() external payable, and call the deposit function from within it. This will ensure that the logic in deposit executes if Ether is sent directly to the contract. This is important to prevent Ether from being locked in the contract since we don't have a withdraw function in this use-case.



Test the contract
In the Deploy tab in Remix, deploy the contract to your local Ganache chain by connecting to Injected Web3 and ensuring MetaMask is pointed to localhost:8545.
You will need to fill in the constructor parameters with your designated employee addresses.
Test the deposit function by sending various values. Keep an eye on the employee balances as you send different amounts of Ether to the contract and ensure the logic is executing properly.