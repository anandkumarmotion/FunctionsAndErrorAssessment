
# ErrorHandlingContract
This is a sample smart contract that shows how errors are handled in solidity using require(), assert(), and revert() statements.

## Description
This program is a simple contract written in Solidity, a programming language used for developing smart contracts on the Ethereum blockchain.The contract provides three functions, each demonstrating a different error handling method.

1.placeOrder():- This function will help you to order pizza but if their is not sufficient amount in your balance than with the use of require() function and error message will be printed on the screen.

2. delivered():- This function will help you to deliver the pizza to the require address.But if the address is not correct or the order has not been placed by the particular address than using the assert() function the condition will be checked and error message will be printed on the screen.

3. rejectOrder():- This function will be used to reject the order by the user and if the the conditions are not valid or the user already rejected the order than using the revert function error message will be printed on the screen.

## Getting Started

### Installing
To run this program, you can use Remix, an online Solidity IDE. To get started, go to the Remix website at https://remix.ethereum.org/.

### Executing program
1. Now after opening the link you will click on the "File Explorer" option on the extreme left of the screen,then click on "create new file".
2. Save the file with .sol extension (For Eg. ErrorHandling.sol).
3. Copy paste the following code on your remix platform.

```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract burgerPlacing {
    uint public CountOrder;
    mapping(uint => address) public orderOwners;
    mapping(uint => uint) public orderBurger;
    mapping(uint => bool) public isDelivered;
    mapping(uint => bool) public isRejected;
    
    event OrderDelivered(uint orderNumber, address client);
    event OrderRejected(uint orderNumber, address client);
    

    // REQUIRE FUNCTION()
    function placeOrder(uint SelectBurger) public payable returns(uint) {
        require(msg.value >= 1, "The Required Payment not met!");
        CountOrder++;
        orderOwners[CountOrder] = msg.sender;
        orderBurger[CountOrder] = SelectBurger;
        return CountOrder;
    }
    
    // ASSERT FUNCTION()
    function delivered(uint orderNumber) public {
    assert(orderOwners[orderNumber] == msg.sender && !isDelivered[orderNumber]);
    
    isDelivered[orderNumber] = true;
    emit OrderDelivered(orderNumber, msg.sender);
    }
```
4. To compile the code click on the "Solidity Compiler" option on the left hand side. Before compiling check the compiler option is ^0.8.0,then click on the "compile" button.
5. Once the code is compiled click on the "Deploy and run Transaction" button on the left side of the screen. And click on "Deploy" button.

## Usage
### require()
Parameters():- msg.value >= 1, "The Required Payment not met!" (2 Paramters with condition and a string)
Returns:- "Invalid candidate"-> If the user does not have enough amount in the wallet.
           CountOrder++;; -> Will be Added to Total Orders.
           orderOwners[CountOrder] = msg.sender; -> Order will be added to particular address from whom the order has been placed.
           orderBurger[CountOrder] = SelectBurger; -> Array of mapping that stores the selected burger for each order. 

### assert()
Parameters():- orderOwners[orderNumber] == msg.sender && !isDelivered[orderNumber] (1 Parmeter which Ensure order owner and undelivered order.)
Returns:- isDelivered[orderNumber] = true; -> Makes the condition true for the burger has been delivered.

### revert()
Parameters():- "Order does not exist or has already been rejected" (1 Parameter with a string)
Returns:- isRejected[orderNumber] = true; -> If rejected 1st time than it makes the mapping value true;

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
