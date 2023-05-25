## Rafidul_SmartContract6
### Contract deploying Contract
Composability refers to the capability of contracts to interact with each other. Smart Contracts can easily interact with one another, making them composable. In the context of DeFi, complex financial products can seamlessly interact with each other due to their on-chain code availability.<br>
```
//SPDX-License-Identifier:MIT
pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiStoragefactory {

    rafiSimplestorage public rafisimplestorage; //here we have created a global variable

    function createrafiSimplestorage() public{
        rafisimplestorage = new rafiSimplestorage();
       //here `new` keyword is used to let the solidiy know that we are going to deploy new rafiSimplestorage()

    } // This is a function to deploy our rafiSimplestorage contract

}
```
here in the above code of ```rafiStorageFactory.sol```the line  ```import ./rafiSimplestorage.sol``` is exact the same as the copy paste of ```rafiSimplestorage.sol``` file<br>
i.e it takes the path of ```rafiSimplestorage.sol``` and paste all code of this file at ```rafiStorageFactory.sol```


!![w16](https://user-images.githubusercontent.com/89090776/231071349-512178a6-c6e7-4fa0-af93-8e68b5f32cc5.jpg)
Figure1: here we see that that the contract ```contract rafiStoragefactory``` have deployed contract ```contract rafiSimplestorage```.

When a contract of a file deploy contract of another file the solidity version of both file must be compatible i.e if version of of a file is ^0.8.0 other <br>
must not be ^0.7.0<br>


Here we have worked with array

```
//SPDX-License-Identifier:MIT
pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiStoragefactory {

    rafiSimplestorage[] public rafisimplestorageArray; ////here we have created an array to store addresses of the contracts


    function createrafiSimplestorage() public{
        rafiSimplestorage rafisimplestorage = new rafiSimplestorage();// here we save it as a memory variable
       //here `new` keyword is used to let the solidiy know that we are going to deploy new rafiSimplestorage()


       rafisimplestorageArray.push(rafisimplestorage);// adding rafisimplestorage variable to rafisimplestorageArray



    } // This is a function to deploy our rafiSimplestorage contract

}

```


![w19](https://user-images.githubusercontent.com/89090776/231094487-f568517d-ca21-4724-91ec-20c90317206f.jpg)
Figure2: Again we click on ```createrafiSimplestorage``` button transaction will occur that means contract will be deployed and if we typed '0' at the field of <br> ```rafisimplestorageArray``` button and see that at '0' index a new address of the contract have been assinged.



<br><br>



### Contract Interacting with other contract

To call a function from the rafiSimplestorage.sol file in the rafiStorageFactory.sol file, we need the contract's address and ABI<br> (Application Binary Interface). The ABI specifies how our code can interact with the contract, including its inputs, outputs, and<br> available functionalities.




Figure3: In the above these are ABI

We will get addresses at ```rafiSimplestorage[] public rafisimplestorageArray;``` and ABI because of this line ```import "./rafiSimplestorage.sol";```


```
//SPDX-License-Identifier:MIT
pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiStoragefactory {

    rafiSimplestorage[] public rafisimplestorageArray; //here we have created an array to store addresses of the contracts

    function createrafiSimplestorage() public{
        rafiSimplestorage rafisimplestorage = new rafiSimplestorage();// here we save it as a memory variable
       //here `new` keyword is used to let the solidiy know that we are going to deploy new rafiSimplestorage()


       rafisimplestorageArray.push(rafisimplestorage);// adding rafisimplestorage variable to rafisimplestorageArray



    } // This is a function to deploy our rafiSimplestorage contract
   
    //below we have called function from ```rafisimplestoarge``` contract and store values from this ```rafistoragefactory``` contract


    function rafStore(uint256 _rafisimplestorageIndex,uint256 _rafisimplestorageNumber) public {

        rafiSimplestorage rafisimplestorage =  rafisimplestorageArray[_rafisimplestorageIndex];  //We are saving rafiSimplestorage contract object at 'rafisimplestorageIndex' to our 'rafisimplestorage' variable

        rafisimplestorage.store(_rafisimplestorageNumber);// Calling the store function of 'rafiSimplestorage' contract

    }

    //Below we will create a function that gonna read from 'rafisimplestorage' contract

    function rfGet(uint256 _rafisimplestorageIndex) public view returns(uint256) {
        rafiSimplestorage rafisimplestorage =  rafisimplestorageArray[_rafisimplestorageIndex];

        return rafisimplestorage.retrieve();// to get the number we stored at the previous function

    }

}

```

After deploying the above code we will get the following output



Figure4: here at ```rafStore``` button field we typed '1' which is ```rafisimplestorageIndex``` and 65 which is ```rafisimplestorageNumber``` and that is we are<br>
storing number '65' at '1' index of this contract which is ```rafiSimplestorage```


Figure5: here we have two contracts ```rafiSimplestorage.sol``` that will store variables and another one is ```rafiStorageFactory.sol``` contract that<br>
will act as a manager of ```rafiSimplestorage``` contract which will deploy and interact with it.


<br><br>




### Inheritence and overrides

here we will create a child contract of ```rafisimplestorage``` contract which is ```rafiExtrastorage``` contract where it will inherit all <br>
the functionality of ```rafiSimplestorage``` contract<br>

by creating a new solidity file ```rafiExtrastorage.sol``` file we will write the following code

```
//SPDX-License-Identifier:MIT

pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiExtrastorage is rafiSimplestorage {

}

```


Then we will get the following output:


figure6: here we see ```rafiChildstorage``` contract deployed all functions of ```rafiSimplestorage``` contract

In ```rafiChildstorage``` contract we want to do something that we want to add '5' to any number we give it<br>
We can do it by overriding the functions and for that two keywords we will use 'virtual' and 'override'.

In order to override function of parent contract by child contratc we have to do the following<br>



Figure7: we have to 'virtual' keyword at store fuunction of parent contract. the code is given below:




Figure8: then we have to 'override' keyword to the inherited 'store' function of the child contract. The code is given below:

```
//SPDX-License-Identifier:MIT

pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiChildstorage is rafiSimplestorage {

    function store(uint256 _goodNumber) public override  {
      goodNumber = _goodNumber + 65 ;

}

}


```


Figure9: Here we will get the following output when we deploy the ```rafiChildstorage``` contract
