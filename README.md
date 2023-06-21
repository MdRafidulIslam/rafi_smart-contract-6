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


![six1](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/c97b6970-d177-4449-b979-b2170581e7df)

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


![six2](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/825b5838-2ced-4804-9acd-46351f8919f1)

Figure2: Again we click on ```createrafiSimplestorage``` button transaction will occur that means contract will be deployed and if we typed '0' at the field of <br> ```rafisimplestorageArray``` button and see that at '0' index a new address of the contract have been assinged.



<br><br>



### Contract Interacting with other contract

To call a function from the rafiSimplestorage.sol file in the rafiStorageFactory.sol file, we need the contract's address and ABI<br> (Application Binary Interface). The ABI specifies how our code can interact with the contract, including its inputs, outputs, and<br> available functionalities.




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


![six4](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/fca854a7-5250-44f1-bdb1-e51e41a8df96)

Figure4: here at ```rafStore``` button field we typed '1' which is ```rafisimplestorageIndex``` and 65 which is ```rafisimplestorageNumber``` and that is we are<br>
storing number '65' at '1' index of this contract which is ```rafiSimplestorage```

![six5](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/afc5ec1b-e823-437b-9263-0a7228aa3743)

Figure5: here we have two contracts ```rafiSimplestorage.sol``` that will store variables and another one is ```rafiStorageFactory.sol``` contract that<br>
will act as a manager of ```rafiSimplestorage``` contract which will deploy and interact with it.


<br><br>




### Inheritence and overrides

here we will create a child contract of ```rafisimplestorage``` contract which is ```rafiChildstorage``` contract where it will inherit all <br>
the functionality of ```rafiSimplestorage``` contract<br>

by creating a new solidity file ```rafiChildstorage.sol``` file we will write the following code

```
//SPDX-License-Identifier:MIT

pragma solidity ^0.8.0;

import "./rafiSimplestorage.sol";

contract rafiChildstorage is rafiSimplestorage {

}

```


Then we will get the following output:

![six6](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/f52322db-a919-415c-9bcd-5a0ac27fbfc6)

figure6: here we see ```rafiChildstorage``` contract deployed all functions of ```rafiSimplestorage``` contract

In ```rafiChildstorage``` contract we want to do something that we want to add '65' to any number we give it<br>
We can do it by overriding the functions and for that two keywords we will use 'virtual' and 'override'.

In order to override function of parent contract by child contratc we have to do the following<br>


![six7](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/e865fe1a-242a-43a0-a1db-894690c459b3)

Figure7: we have to 'virtual' keyword at store fuunction of parent contract. the code is given below:



![six8](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/317ea00d-7bbe-402d-887b-33d61786586d)


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

![six9](https://github.com/MdRafidulIslam/rafi_smart-contract-6/assets/86659473/4bb0c566-c6f0-4964-86ff-1d4a8712b4b9)
Figure9: Here we will get the following output when we deploy the ```rafiChildstorage``` contract
