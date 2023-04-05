# `Information`
This should be a fun exercise.

## Router Protocol

<!-- <p align="center" >

<img src="https://user-images.githubusercontent.com/124175970/224509096-12e4864a-6819-4c8c-8998-41c7a96ba026.jpg" />
  </p> -->

<!-- ![router-protocol-crypto-ninjas](https://user-images.githubusercontent.com/124175970/224509096-12e4864a-6819-4c8c-8998-41c7a96ba026.jpg) -->

<img src="https://user-images.githubusercontent.com/124175970/224509096-12e4864a-6819-4c8c-8998-41c7a96ba026.jpg" width="8000000em" height="400em" />


# `Company Information`

Router Protocol is a solution introduced to address the issues hindering the usability of cross-chain liquidity migration in the DeFi ecosystem. It acts as a bridge connecting various layer 1 and layer 2 blockchains, allowing for the flow of contract-level data across them. The Router Protocol can either transfer tokens between chains or initiate operations on one chain and execute them on another.

Please check the [official documentation of Router Protocol](https://www.routerprotocol.com/)

# `Why participate in Router Student Expert Program ?`

We reward 🏅 badges to individuals who complete our assignments!

First, you need to go through the guide which will teach you the concepts required for the assignment. Then you need to complete the assignment based on the what you learnt.

The journey is divided into multiple stages, each with its own set of points. As you complete Assignment 1, you'll earn a certain number of points, and the same goes for Assignment 2, all the way up to the Final Assignment. Once you've earned a certain benchmark points, you'll receive an NFT badge as a token of your achievement.

Each assignment has its own unique set of points. For every 100 points earned, you'll receive a 🥉 Bronze Router Expert badge, for 500 points, you'll get a 🥈 Silver badge, and for 1000 points, you'll receive a coveted 🥇 Gold badge. These badges will add an extra shine to your resume and can be a golden ticket to working with us.

This initiative is perfect for those interested in pursuing a career in the web 3 space, and the badges can serve as a glowing recommendation for future opportunities. So what are you waiting for? Let's get started on the path to becoming a Router Expert! 🚀

# `Guide`

# 🧭 `Table of contents`
- [🧭 Table of contents](#-table-of-contents)
- [`What is an NFT ?`](#What-is-an-NFT-?)
- [`How to make a simple NFT ?`](#How-to-make-a-simple-NFT-?)
- [`Need for CrossChain ?`](#Need-for-CrossChain)
- [`What is a CrossChain NFT ?`](#What-is-CrossChain-NFT-?)
- [`Understanding Router CrossTalk`](#Understanding-Router-CrossTalk)
- [`CrossTalk Cheatsheet`](#Understanding-Router-CrossTalk)
- [`Initiating the Contract`](#Initiating-the-Contract)
- [`Creating state variables and the constructor`](#Creating-state-variables-and-the-constructor)
- [`Setting up the Destination Contract on the Source Contract`](#Setting-up-the-Destination-Contract-on-the-Source-Contract)
- [`Transferring tokens from a source chain to a destination chain`](#Transferring-tokens-from-a-source-chain-to-a-destination-chain)
- [`Handling a cross-chain request`](#Handling-a-cross-chain-request)
- [`Handling the acknowledgement received from destination chain`](#Handling-the-acknowledgement-received-from-destination-chain)
- [`Full Code`](#Full-Code)
- [🚀 Steps](#Steps)


## `What is an NFT ?`

![_117548721_nfts2](https://user-images.githubusercontent.com/124175970/224860849-f037eb49-0288-49b8-a922-e08015b5280a.jpg)


NFT stands for Non-Fungible Token. Think of it like a digital certificate of ownership for something unique, like a rare trading card or a piece of art. Unlike regular currency, which is fungible (meaning one unit is interchangeable with another), NFTs are unique and cannot be exchanged for something else.

NFTs are created using blockchain technology, which makes them secure and verifiable. They can represent anything that has value and uniqueness, such as digital art, music, videos, tweets, and even virtual real estate. When someone buys an NFT, they are buying the ownership rights to that specific item, which is recorded on the blockchain for everyone to see.

The value of NFTs is determined by market demand, like any other collectible item. Some NFTs have sold for millions of dollars, while others are more affordable. NFTs have gained popularity recently as a way for artists and creators to monetize their digital creations and for collectors to own a unique piece of digital history.

Here's an example of **Bored Ape** NFT series :-

![bored-ape-yacht-club-nft (1)](https://user-images.githubusercontent.com/124175970/224862305-ca762b98-a29c-4d6f-9693-9642f7c63ae1.gif)


## `How to make a simple NFT ?`

**ERC721 Standard**

![1_-Aq82tW0D4c9Xn8zHRYecw](https://user-images.githubusercontent.com/124175970/224863210-5b6262b9-e793-49ee-b1f0-1158eda92cf0.png)

ERC721 is a standard for creating non-fungible tokens on the Ethereum blockchain. The ERC721 standard is like a set of rules that all NFTs on the Ethereum blockchain must follow. Think of it like a recipe for making a cake - you need certain ingredients and instructions to make sure it turns out right.

ERC721 defines a specific set of functions that NFTs must have, like the ability to be transferred from one owner to another, the ability to check who owns a particular NFT, and the ability to create new NFTs. These functions are like different steps in the recipe.

**ERC721 Functions**

Some of the functions included in the ERC721 standard are:

**mint**: This function creates a new token and assigns it to an owner.

**transfer**: This function allows the owner of a token to transfer ownership to another address.

**balanceOf**: This function returns the number of tokens owned by a specific address.

**ownerOf**: This function returns the address of the current owner of a specific token.

**approve**: This function allows an address to approve another address to transfer ownership of a specific token.

**safeTransferFrom**: This function transfers ownership of a token from one address to another, but also includes additional safety checks to ensure the transfer is successful.

**What is OpenZeppelin ?**

Instead of writing all the code for creating an NFT from scratch, developers can use OpenZeppelin's pre-written code to make their own NFTs. This can save a lot of time and effort, and can also help ensure that the code works correctly and is secure.

It's kind of like using Lego blocks to build something - instead of making each block from scratch, you can just use pre-made blocks to build something faster and easier.

With OpenZeppelin, developers can just follow the pre-written code to create their own NFTs without having to start from scratch.

**Simple ERC721 contract using Openzeppelin**

```sh
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.9;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721Burnable.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract MyToken is ERC721, ERC721Burnable, Ownable {
    using Counters for Counters.Counter;

    Counters.Counter private _tokenIdCounter;

    constructor() ERC721("MyToken", "MTK") {}

    function _baseURI() internal pure override returns (string memory) {
        return "<paste the url here>";
    }

    function safeMint(address to) public onlyOwner {
        uint256 tokenId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, tokenId);
    }
}
```

The contract is making use of the OpenZeppelin library which includes pre-written functions that make it easier to create NFTs.

Then the name and symbol of the NFT is given as parameters to the constructor.It's using three different pre-written contracts from OpenZeppelin:

**ERC721**: This is the main contract for creating NFTs. It defines the basic functions that NFTs should have, like the ability to be owned and transferred.

**ERC721Burnable** : This is an extension of ERC721 that allows the owner of an NFT to "burn" it, or destroy it completely. This can be useful for controlling the supply of an NFT.

**Ownable** : This is another extension of ERC721 that defines an "owner" for the NFT contract. Only the owner can perform certain functions, like creating new tokens.

The code also includes a "using" statement, which tells the contract to use a library called "Counters". This library includes a function called "Counter" that's used to keep track of the number of tokens that have been created.

The constructor function is defining the name and abbreviation of the NFT. The name is "MyToken" and the abbreviation is "MTK".

The "_baseURI" function is defining the URL where people can go to find more information about the NFT (metadata). This could be either IPFS or other decentralised storage networks. For this, you can make use of tools like [NFTUP](https://nft.storage/docs/how-to/nftup/)

The "safeMint" function is used to create new tokens and assign them to a specific owner. The owner of the NFT contract is the only one who can use this function. It uses the "Counter" function from the Counters library to keep track of the number of tokens that have been created. When a new token is created, the owner can assign it to a specific address.

You can use the above code and deploy using [Remix IDE](https://www.remix.ethereum.org) and Hurray !, you've made your own NFT .

## `Need for CrossChain`

**Bitcoin**

![images](https://user-images.githubusercontent.com/124175970/224867383-360da83c-5053-4f5b-aff3-8c9d1b00942e.png)

Back in 2009, Bitcoin was created by an unknown person called Satoshi Nakamoto, introducing the concept of decentralization. It eliminated the need for a central authority or intermediary to verify transactions, making it possible for people to transact with each other directly.

**Problem with Bitcoin**

Bitcoin was not designed to support smart contracts, which limits its ability to create complex decentralized applications. 
The inability to deploy smart contracts on the Bitcoin blockchain, makes the scope of decentralization , limited to a very small area.

**Ethereum**

![ethereum-1](https://user-images.githubusercontent.com/124175970/224869429-53317c46-6407-4fa7-b52a-76e691f333e9.jpeg)

Ethereum is a blockchain, which serves as a state machine where people can deploy smart contracts, This enables people to build Dapps (Decentralised Applications on the top of Ethereum" 

**Problem with Ethereum**

Ethereum is not scalable.The cost of gas fees which one need to pay to interact with the smart contracts is quite high. This hinders the businesses of the Dapps buit on the top of Ethereum.

**L2 Solutions of Ethereum**

<img width="400" alt="image" src="https://user-images.githubusercontent.com/124175970/224869825-bfcb3ac6-e0df-40fe-96b0-ca01ccacfe0b.png">

Many L2 solutions for Ethereum are created, keeping in mind Ethereum isn't scalable. The gas fee which one need to pay in order to intereact with the smart conracts is significantly cheaper than Ethereum.

**Problem with L2 solutions of Ethereum**

L2 solutions solves the problem of scalability , but they have much lesser nodes as compared to Ethereum making them less decentralised and secure than Ethereum.

**Blockchain Trilemma**

<img width="488" alt="image" src="https://user-images.githubusercontent.com/124175970/224870341-b8750142-f1e6-43cd-abf5-607fcc6add3e.png">

So, we can clearly see, solving scalability , degrades security and decentralisation and having having more decentralisation and security results in making the chain less scalable .

This is known as Blockchain Trilemma, where it's not possible to ensure scalability, decentralisation and security at the same time . 

**Need for Crosschain**

Going CrossChain helps us leverage all these 3 features (Decentralisation + Scalabity + Security ) used for different operations performed in a single Dapp.
This is exactly , where the Router comes in ! It is an interoperability layer to connect blockchains with a goal to integrate all the blockchains within the ecosystem. 

<img width="581" alt="image" src="https://user-images.githubusercontent.com/124175970/224871477-a1f06b33-0b74-4244-9b3f-3291e246950d.png">

## `What is a CrossChain NFT ?`

CrossChain NFTs are non-fungible tokens that can exist and be traded on multiple different blockchain networks. This means that an NFT created on one blockchain network, such as Ethereum, can be moved to and traded on another blockchain network, such as Binance Smart Chain or Polygon.

Imagine you have an NFT on the Ethereum blockchain that represents a piece of artwork. If you want to sell or trade that NFT on another blockchain network, you would need to create a new NFT on that network, which can be time-consuming and costly. However, with CrossChain NFTs, you can simply transfer the original NFT to the new blockchain network, enabling you to sell or trade it without having to go through the process of creating a new one.

<img width="461" alt="image" src="https://user-images.githubusercontent.com/124175970/224872315-6b455b3f-e822-400d-ab2d-cb81ad135f5d.png">


## `Understanding Router CrossTalk`

**Overview**

Router's CrossTalk library is a tool that makes it easy for different blockchains to communicate with each other. This library is designed to work with Router's infrastructure, and allows contracts on one blockchain to talk to contracts on another blockchain. You can use this library in your own development projects to make it easier for your contracts to communicate across different blockchains, without disrupting other parts of your project.

**Gateway Contracts**

Gateway contracts are contracts which are pre-deployed (refer appendix) on supported blockchains for cross-chain communication.The source chain's gateway contract communicates with the destination chain's gateway contract, enabling communication between application contracts deployed on different chains

[Gateway Contract Addresses](https://devnet.lcd.routerprotocol.com/router-protocol/router-chain/multichain/chain_config)

**CrossTalk Workflow**

<img width="503" alt="image" src="https://user-images.githubusercontent.com/124175970/224872866-cb82abb4-d072-4c7d-bc46-672a18afbb54.png">

When a user wants to execute a cross-chain request, they call the "requestToDest" function on the Router's Gateway contract. They pass the payload of data to be transferred from the source chain to the destination chain along with thenecessary parameters.The "requestToDest" function sends the data to the destination chain where the user's contract with the "handleRequestFromSource" function is waiting to receive it.Once the data is received, the "handleRequestFromSource" function processes it on thedestination chain.After processing the data, the destination chain sends an acknowledgment back to the source chain where "handleCrossTalkAck" function in the user's contract is used to handle it.

**Understanding CrossTalk Functions**

Router’s Gateway contracts have a function named requestToDest that facilitates the transmission of a cross-chain message. Whenever users want to execute a cross-chain request, they can call this function by passing the payload to be transferred from the source to the destination chain along with the required parameters.

In addition to calling the aforementioned function, CrossTalk users will also have to implement two functions on their contracts:

To handle a cross-chain request on the destination chain, users are required to include a handleRequestFromSource function on their destination chain contracts.
To process the acknowledgment of their requests on the source chain, user will have to implement a handleCrossTalkAck function on their source chain contracts.

**requestToDest parameters**

1) requestArgs is a struct having these parameters :
a) expiryTimestamp: The timestamp by which your 
cross-chain call will expire
b) isAtomicCalls: To make a batch of transactions 
atomic, set it to true else false
c) feePayer: This specifies the address on the 
Router chain from which the cross-chain fee will be 
deducted.
For example:- 
```sh 
Utils.RquestArgs(1000000000000000, 
false, Utils.FeePayer.APP)
```
2) These structs should also be passed as parameters to requestToDest function to set the acknowledgement type , gas limit and gas price for 
acknowledgment
```sh
Utils.AckType(Utils.AckType.NO_ACK),
Utils.AckGasParams (destGasLimit, destGasPrice)
```
3) destinationChainParams: is a struct having 
these parameter:-
a) gasLimit: Required gas limit for executing 
cross-chain requests
b)gasPrice: Gas price in wei to be used on the destination chain.
c)destChainType: Represents the type of chain
d) destChainId: Chain ID of destination chain, in 
string format.
```sh
Utils.DestinationChainParams(destGasLimit,destGasPrice,_dstChainType,
_dstChainId)
```
4) contractCalls: struct , including an array of payloads and contract addresses to be sent to the destination chain. You can send any information you want, and each piece of data will be sent to the respective contract address that you specify in the arrays.
```sh
struct ContractCalls {
 bytes[] payloads;
 bytes[] destContractAddresses;}
 ```
 
**Example Code for Above**

```sh
IGateway(gatewayContract).requestToDest(
Utils.RequestArgs(1000000000000000, false,
Utils.FeePayer.APP),
Utils.AckType(Utils.AckType.NO_ACK),
Utils.AckGasParams(0,0),
Utils.DestinationChainParams(
destGasLimit,
destGasPrice,
_dstChainType,
_dstChainId
),
Utils.ContractCalls(payloads, addresses)
);
```

**handleRequestFromSource

In this function, you will get the address of the contract that initiated this request from the source chain, the payload you created on the source chain, the source chain ID, and the source chain type. After receiving this information, you can process your payload and complete your cross-chain transaction.

**Example Code for above**

```sh
function handleRequestFromSource(
bytes memory srcContractAddress,
bytes memory payload,
string memory srcChainId,
uint64 srcChainType
) external returns (bytes memory) {
require(
keccak256(srcContractAddress) ==
keccak256(ourContractOnChains[srcChainType][srcChainId]),
"Invalid src chain"
);
(uint256 amount, address recipient) = abi.decode(
payload,
(uint256, address)
);
_mint(recipient, amount);
return "";
}
```


![Click here to Open Router CrossTalk Cheatsheet](https://user-images.githubusercontent.com/124175970/224877602-3e7c7bd2-700c-4ac8-96f5-0e391f8859bf.png)

[Click here to download Router CrossTalk Cheatsheet](https://github.com/router-resources/CrossChainNFTAssignment/files/10963540/crosstalk.pdf)

# `Making CrossChain NFT using Router CrossTalk`

![nftRouter](https://user-images.githubusercontent.com/124175970/224004658-177790e4-c7f5-4cb4-9c44-810bd6c780d0.gif)

## `Initiating the Contract`

For initiating the smart contract named "nft", the contract imports four external contracts :-

1. **ICrossTalkApplication.sol**

2. **IGateway.sol**

3. **ERC721.sol**

The "ICrossTalkApplication.sol" and "IGateway.sol" contracts are imported from the "evm-gateway-contract/contracts" and "ERC721.sol" from "openzeppelin/contracts/token".The "nft" contract implements the "ICrossTalkApplication" and "ERC721.sol" contract by inheriting from them. This means that the "nft" contract must have all the functions and variables defined in the "ICrossTalkApplication" contract. By importing and implementing these contracts, the "nft" contract will have access to their functionality and will be compatible with other contracts that follow the same standards.

```sh
//SPDX-License-Identifier: UNLICENSED
pragma solidity >=0.8.0 <0.9.0;

import "evm-gateway-contract/contracts/ICrossTalkApplication.sol";
import "evm-gateway-contract/contracts/IGateway.sol";
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract nft is ERC721, ICrossTalkApplication {
}
```
## `Creating State Variables and the Constructor`

The smart contract has the following state variables:

1. **onwer** - an address variable which stores the address from which the contract has been deployed.

2. **gatewayContract** - an address variable which holds the address of the gateway contract. Gateway contracts are contracts which are pre-deployed on supported blockchains for cross-chain communication.The source chain's gateway contract communicates with the destination chain's gateway contract, enabling communication between application contracts deployed on different chains. Find GatewayContract Addresses [here](https://devnet.lcd.routerprotocol.com/router-protocol/router-chain/multichain/chain_config)

3. **destGasLimit** - a uint64 variable which indicates the amount of gas required to execute the function that will handle cross-chain requests on the destination chain.

4. **ourContractOnChains** - a mapping which maps a chain type and chain ID to the address of nft contract deployed on different chains. This mapping will be used to set the address of the destination contract to the source contract and visa versa

The constructor of the smart contract takes three parameters:

1. **gatewayAddress** - an address variable which holds the address of the gateway contract.

2. **_destGasLimit** - a uint64 variable which indicates the amount of gas required to execute the function that will handle cross-chain requests on the destination chain.

Inside nft contract contructor, pass the name of your token followed by its symbol.

The smart contract extends the ERC721 standard and includes all the required functions and variables such as balanceOf, mint, burn and others.

```sh
    address owner;
    address public gatewayContract;
    uint64 public destGasLimit;
    mapping(uint64 => mapping(string => bytes)) public ourContractOnChains;
constructor( address payable gatewayAddress,
        uint64 _destGasLimit ) ERC721("Token","RTK")
        {
            gatewayContract=gatewayAddress;
            destGasLimit=_destGasLimit;
            owner=msg.sender;
        }
```

## `Setting up the Destination Contract on the Source Contract`

**setContractOnChain**:-

The given code defines a setter function setContractOnChain which allows the owner to set the address of a destination contract on the source chain and visa versa. The function takes three parameters:

chainType - a uint64 variable which represents the type of the chain (e.g. Ethereum, Binance Smart Chain, etc.)
chainId - a string which represents the ID of the chain where the contract is deployed.
contractAddress - an address variable which holds the address of the nft contract deployed on the other chain we want to send the tokens to.
The function first checks whether the caller is the owner by comparing the msg.sender with the admin address variable. If the caller is not the owner, the function will revert with an error message "only owner".

If the caller is the owner, the function will convert the contractAddress to bytes using the toBytes function and store it in the ourContractOnChains mapping using the chainType and chainId as the keys.

```sh
function setContractOnChain(
    uint64 chainType, 
    string memory chainId, 
    address contractAddress
) external {
    require(msg.sender == onwer, "only owner");
    ourContractOnChains[chainType][chainId] = toBytes(contractAddress);
}
```
## `Transferring tokens from a source chain to a destination chain`

**transferCrossChain:-**

This function allows a user to transfer their NFTs from their account on one chain to their account on a destination chain. The function burns the NFTs specified by their id's from the user's account, creates a cross-chain communication request to the destination chain, and passes the transfer parameters as payload in the request.

The function accepts the following parameters:

1. **_dstchainType**: A uint64 representing the type of the destination chain. See the link provided in the description for the list of available chain types.

2. **_dstchainId**: A string representing the ID of the destination chain.

3. **destGasPrice**: A uint64 representing the gas price of the destination chain.

4. **recipient**: Wallet address on the destination chain we want to transfer our NFT to.

5. **id**: A uint256 variable specifying the id of the NFT we want to transfer to the recipient on the destination chain

The function burns the NFT with specified id from the user's account and creates a cross-chain communication request to the destination chain. The payload for the request is generated by ABI encoding "amount" and "recipient".The function uses the ourContractOnChains mapping to retrieve the address of the nft contract on the destination chain.

The function calls the requestToDest function of the Gateway Contract to generate the cross-chain communication request to the destination chain.The requestToDest function in Router's Gateway contracts is used to send a request to the Destination Chain .To execute a cross-chain request, users can call this function and pass the payload and required parameters from the source to the destination chain.

**requestToDest** function takes in these parameters:-

1. **requestArgs** is a struct having these parameters:-
a) expiryTimestamp: The timestamp by which your cross-chain call will expire
b) isAtomicCalls: To make a batch of transactions atomic, set it to true else false
c) feePayer: This specifies the address on the Router chain from which the cross-chain fee will be deducted. For example:- Utils.RequestArgs(1000000000000000, false, Utils.FeePayer.APP)

2. **actType** and **actGasParams** should also be passed as parameters to requestToDest function to set the acknowledgement type , gas limit and gas price for acknowledgment
Utils.AckType(Utils.AckType.NO_ACK),
Utils.AckGasParams (destGasLimit, destGasPrice)

3. **destinationChainParams**: is a struct having these parameter:-
a)gasLimit: Required gas limit for executing cross-chain requests b)gasPrice: Gas price in wei to be used on the destination chain. c)destChainType: Represents the type of chain
d)destChainId: Chain ID of destination chain, in string format.
Utils.DestinationChainParams(destGasLimit,destGasPrice,_dstChainType,
_dstChainId)

4. **contractCalls**: struct , including an array of payloads and contract addresses to be sent to the destination chain. You can send any information you want, and each piece of data will be sent to the respective contract address that you specify in the arrays.
struct ContractCalls {
    bytes[] payloads;
    bytes[] destContractAddresses;}


```sh
 function transferCrossChain(
        uint64 _dstChainType,
        string memory _dstChainId, 
        uint64 destGasPrice,
        address recipient,
        uint256 id
    ) public {
        bytes memory payload = abi.encode(id, recipient);

        
        _burn(id);

      

        bytes[] memory addresses = new bytes[](1);
        addresses[0] = ourContractOnChains[_dstChainType][_dstChainId];
        bytes[] memory payloads = new bytes[](1);
        payloads[0] = payload;

        IGateway(gatewayContract).requestToDest(
            Utils.RequestArgs(1000000000000000, false, Utils.FeePayer.APP),
            Utils.AckType(Utils.AckType.NO_ACK),
            Utils.AckGasParams(destGasLimit, destGasPrice),
            Utils.DestinationChainParams(
                destGasLimit,
                destGasPrice,
                _dstChainType,
                _dstChainId
            ),
            Utils.ContractCalls(payloads, addresses)
        );

       
    }
  ```
 
## `Handling a cross-chain request`

**handleRequestFromSource function:-**

This function is called by the Gateway contract on the destination chain, which is triggered when a cross-chain transfer request is sent by our contract on the source chain. This function receives several parameters, including the source contract address, the payload, the source chain ID, and the source chain type.

1. **srcContractAddress**: A bytes array that represents the address of the contract on the source chain that initiated the cross-chain transfer request.

2. **payload**: A bytes array that containing the payload we sent from the source chain.

3. **srcChainId**: A string that represents the ID of the source chain from which the cross-chain transfer request originated.

4. **srcChainType**: An unsigned 64-bit integer that represents the type of the source chain from which the cross-chain transfer request originated.

he function first checks that the call is made only by the Gateway contract and that the request is received from our contract on the source chain. If the conditions are not met, the function will revert the transaction.

The payload that was sent with the cross-chain transfer request contains recipient's address, the id of NFT to be minted on the destination chain. The function decodes the payload using abi.decode() function.

After decoding the payload, the function uses the _mint function of the ERC-721 contract from the OpenZeppelin library to mint the ERC-721 token to the recipient's address on the destination chain. 

Finally, the function returns an empty string. Note : We have to return atleast an empty string as per the function definition.

```sh
function handleRequestFromSource(
        bytes memory srcContractAddress,
        bytes memory payload,
        string memory srcChainId,
        uint64 srcChainType
    ) external returns (bytes memory) {

        
        require(
            keccak256(srcContractAddress) ==
                keccak256(ourContractOnChains[srcChainType][srcChainId]),
            "Invalid src chain"
        );
        (uint256 amount, address recipient) = abi.decode(
            payload,
            (uint256, address)
        );

        _mint(recipient, amount);

        
        return "";
    }
```
## `Handling the acknowledgement received from destination chain`

**handleCrossTalkAck:-**

The handleCrossTalkAck function is a public function that needs to be implemented in the contract to satisfy the ICrossTalkApplication interface.
The function takes three parameters: **eventIdentifier**, **execFlags**, and **execData** . However, since we are only implementing an empty function, we do not need to use these parameters.

The handleCrossTalkAck function does not perform any operation on the contract or on the blockchain. It is implemented as an empty function and only serves as a placeholder to satisfy the interface requirements.

Therefore, the handleCrossTalkAck function should be implemented with an empty body as shown in the code provided.

```sh
function handleCrossTalkAck(
  uint64, //eventIdentifier,
  bool[] memory, //execFlags,
  bytes[] memory //execData
) external view override {}
```

## `Full Code`

```sh
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;
import "@routerprotocol/evm-gateway-contracts@1.0.5/contracts/IGateway.sol";
import "@routerprotocol/evm-gateway-contracts@1.0.5/contracts/ICrossTalkApplication.sol";
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
contract nft is ERC721, ICrossTalkApplication{
  
    address owner;
    address public gatewayContract;
    uint64 public destGasLimit;
    mapping(uint64 => mapping(string => bytes)) public ourContractOnChains;
constructor( address payable gatewayAddress,
        uint64 _destGasLimit, string memory feePayer) ERC721("Token","RTK")
        {
            gatewayContract=gatewayAddress;
            destGasLimit=_destGasLimit;
            owner=msg.sender;
            IGateway(gatewayAddress).setDappMetadata(feePayer);
        }
    modifier onlyOwner() {
        require(owner == msg.sender, "Caller is not owner");
        _;
    }
        function mint(address to, uint256 id) public onlyOwner {
        _mint(to, id);
    }
        function setContractOnChain(
        uint64 chainType,
        string memory chainId,
        address contractAddress
    ) external onlyOwner {
        ourContractOnChains[chainType][chainId] = toBytes(contractAddress);
    }
        function transferCrossChain(
        uint64 _dstChainType,
        string memory _dstChainId, 
        uint64 destGasPrice,
        address recipient,
        uint256 id
    ) public {
        bytes memory payload = abi.encode(id, recipient);

        
        _burn(id);

      

        bytes[] memory addresses = new bytes[](1);
        addresses[0] = ourContractOnChains[_dstChainType][_dstChainId];
        bytes[] memory payloads = new bytes[](1);
        payloads[0] = payload;

        IGateway(gatewayContract).requestToDest(
            Utils.RequestArgs(1000000000000000, false),
            Utils.AckType(Utils.AckType.NO_ACK),
            Utils.AckGasParams(destGasLimit, destGasPrice),
            Utils.DestinationChainParams(
                destGasLimit,
                destGasPrice,
                _dstChainType,
                _dstChainId,
                "0x"
            ),
            Utils.ContractCalls(payloads, addresses)
        );

       
    }
        function toBytes(address a) public pure returns (bytes memory b) {
        assembly {
            let m := mload(0x40)
            a := and(a, 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF)
            mstore(
                add(m, 20),
                xor(0x140000000000000000000000000000000000000000, a)
            )
            mstore(0x40, add(m, 52))
            b := m
        }
    }
    function setDestinationGasPrice(uint64 _destGasLimit) public{
        destGasLimit=_destGasLimit;
    }
    function handleRequestFromSource(
        bytes memory srcContractAddress,
        bytes memory payload,
        string memory srcChainId,
        uint64 srcChainType
    ) external returns (bytes memory) {

        
        require(
            keccak256(srcContractAddress) ==
                keccak256(ourContractOnChains[srcChainType][srcChainId]),
            "Invalid src chain"
        );
        (uint256 id, address recipient) = abi.decode(
            payload,
            (uint256, address)
        );

        _mint(recipient, id);

        
        return "";
    }

  function handleCrossTalkAck(
        uint64, // eventIdentifier
        bool[] memory, // execFlags
        bytes[] memory // execData
    ) external {}



}
## `Steps`


✍️ **Setting up your editor:**

Log in to your preferred Solidity development platform, such as Remix or Truffle, etc. For this tutorial, we will be using Remix IDE.

Create a new workspace by selecting the "New Workspace" option. You may need to specify a name for the workspace and choose a template to use. For example, you could select the "Solidity" template or let it be "Default" template ,etc 

![image](https://user-images.githubusercontent.com/124175970/228418777-5ecf5f9e-f3ff-4ae5-ad61-742b9aff3b12.png)


Create a new file in the workspace by selecting the "New File" option. Give the file a name and save it with the ".sol" extension. For example, you could name the file "CrossChainNFT" and save it as "CrossChainNFT.sol".

![image](https://user-images.githubusercontent.com/124175970/228418913-0f25cba3-07c4-442a-8bcb-f52f77d53f3d.png)


Open the "NFT.sol" file, which contains the code you want to use for your new file. Copy the entire code from the "NFT.sol" file.

Go back to the editing area for your new file in the workspace. Paste the code you copied from "NFT.sol" into this new file.

![image](https://user-images.githubusercontent.com/124175970/228419075-2b9e2ba0-79e2-46c0-9c56-354ab398292c.png)


✍️ **Setting up your wallet:**

Open your preferred web browser.

Go to https://metamask.io/download/ and install the Metamask extension for your browser.

![image](https://user-images.githubusercontent.com/124175970/228419311-d9252876-a4cc-4743-aa00-fa95c0376805.png)


Open the Metamask extension by clicking on its icon in your browser toolbar.

Click on the "Create Wallet" button to create a new wallet.

![image](https://user-images.githubusercontent.com/124175970/228419380-2be9642a-1e97-437d-80e0-76093bb1c989.png)


Set a password for your wallet in the provided field. Make sure to remember this password, as it will be needed to access your wallet in the future.

![image](https://user-images.githubusercontent.com/124175970/228419481-6c2091cd-93a7-4258-a920-10d12e555801.png)


Choose either the "Secure my wallet with a seed phrase" or "No thanks, maybe later" option. We recommend choosing the first option to secure your wallet with a backup seed phrase.

![image](https://user-images.githubusercontent.com/124175970/228419558-142fb21e-9e3b-4fc3-a12a-aaae5376a6c2.png)

[Note: A seed phrase, also known as a recovery phrase or mnemonic phrase, is a set of words that serves as a backup to your cryptocurrency wallet. It is usually a sequence of 12, 18, or 24 words that are randomly generated by your wallet when you create it.

The seed phrase is used to recover your wallet in case your device is lost, stolen, or damaged. By entering the seed phrase into a compatible wallet, you can restore access to your funds and private keys.

It's important to keep your seed phrase safe and private, as anyone who has access to it can also access your wallet and funds. You should never share your seed phrase with anyone or store it in an unsecured location such as an email or a cloud storage service. Instead, it's recommended to write it down on a piece of paper and store it in a safe and secure location.

]

Connect to the Mumbai network:

Go to https://mumbai.polygonscan.com/ Scroll down to the bottom of the page and click on the "Add Mumbai Network" button to add Mumbai Network to Metamask Wallet

![image](https://user-images.githubusercontent.com/124175970/228419917-07c5f0f9-9e98-4cc4-9e34-dc86635b83fb.png)


Connect to the Fuji network:

Go to https://testnet.snowtrace.io/ Scroll down to the bottom of the page and click on the "Add C-Chain ( Fuji ) Network" button to add Fuji Network to Metamask Wallet

![image](https://user-images.githubusercontent.com/124175970/228420007-a0f475e9-e9e1-4d26-a2c7-2c51aef96552.png)


💵 **Adding faucets to your account on Fuji and Polygon**

A faucet is a service that allows you to receive free cryptocurrency to use for testing purposes.

To add faucet to your Fuji account, visit https://faucet.avax.network/ and follow these steps:

Paste your wallet address in the provided field. Click on the "REQUEST 2 AVAX" button to receive free AVAX tokens to your wallet address.

![image](https://user-images.githubusercontent.com/124175970/228420155-460900f5-2bda-4bff-8f0c-15dddcd56622.png)


To add faucet to your account on the Mumbai network, visit https://faucet.polygon.technology/ and follow these steps:

Paste your wallet address in the provided field. Click on the "Submit" button to receive free MATIC tokens to your wallet address.

![image](https://user-images.githubusercontent.com/124175970/228420223-74e2325e-ad7c-488d-85c8-96669a6bf55a.png)


💿 **Install all dependencies:**

You don't need to install any dependencies. Remix automatically downloads all the dependencies for you during the time of compile.

🧑‍💻 **Compiling your CrossChain ERC-721 Contract:**

Go back to your Remix IDE.

In the left-hand sidebar, click on the "Solidity Compiler" option.

Click on the "Compile NFT.sol" button to compile the code for your contract.

![image](https://user-images.githubusercontent.com/124175970/228420731-a9399579-0489-4646-b7bf-c60b5fb9c653.png)


If the compilation is successful, you should see a green checkmark next to the "NFT.sol" file in the left-hand sidebar.

If there are any errors in your code, you will see them listed in the right-hand panel under the "Errors" tab. Click on each error to see a more detailed description of the problem and how to fix it.

Alternatively, you can use the shortcut command, "Ctrl + S" on your keyboard to compile the code

🚀 **Deploying the Contract:**

Switch to the Fuji/Binance Network from your Metamask extension by clicking on the Metamask icon in your browser toolbar, and selecting "Fuji/Binance" from the network dropdown menu.

![image](https://user-images.githubusercontent.com/124175970/228421076-276b38c8-ccf1-407e-bc5f-2fd44be7f070.png)


To deploy the contract, go back to Remix and click on the "Deploy & Run Transactions" button and select the correct contract from the dropdown menu.

![image](https://user-images.githubusercontent.com/124175970/228421539-935899e3-075f-47c1-aada-44f5b8e18738.png)


Next, click on the "Environment" dropdown menu and select "Injected Web3" to ensure Remix can connect to your Metamask wallet 

![image](https://user-images.githubusercontent.com/124175970/228420931-d83b5a02-a875-4f35-98ea-203ad96ae979.png)


Enter the "Gateway address" for Fuji/Binance (which can be found at https://devnet.lcd.routerprotocol.com/router-protocol/router-chain/multichain/chain_config), and set the "DestGasLimit" to 500000.

![image](https://user-images.githubusercontent.com/124175970/228421715-d54f5ff0-5ccf-4bcf-a6cd-19d1f456f0e9.png)


To deploy the contract on the Mumbai Network, switch back to the Metamask extension and select "Mumbai" from the network dropdown menu. Then, return to Remix and repeat the previous steps, but this time, select enter the corresponding "Gateway address" for Mumbai from the same website (https://devnet.lcd.routerprotocol.com/router-protocol/router-chain/multichain/chain_config). Set the "DestGasLimit" to 500000.

🔨 **Mint created ERC-721 token on Source Chain:**

In order to mint the created ERC-721 token on the source , mint function defined in openzeppelin can be used.

🤝 **Set destination contract to source contract and source contract to destination contract:**

Switch to the Fuji/Binance Network by clicking on the Metamask extension in your browser and selecting "Fuji/Binance" from the dropdown menu. Once you are on the correct network, select the contract you deployed on Fuji from the "Contract" section of Remix.

Then, click on the "setContractOnChain" function in the "Contract" section and pass in the following parameters:

_chainId: 0 _destChainId: 80001 _contract: The address of the Mumbai contract that you just deployed Click on the "transact" button to execute the function.

Switch to the Mumbai Network by clicking on the Metamask extension in your browser and selecting "Mumbai" from the dropdown menu. Once you are on the correct network, select the contract you deployed on Mumbai from the "Contract" section of Remix.

Then, click on the "setContractOnChain" function in the "Contract" section and pass in the following parameters:

_chainId: 0 _destChainId: 43113 _contract: The address of the Fuji/Binance contract that you just deployed Click on the "transact" button to execute the function.

💵 **Send Route tokens to the source contract:**

Copy the Fuji contract address that you just deployed in the previous steps, then visit https://devnet-faucet.routerprotocol.com/ in your web browser. Paste the Fuji contract address into the provided field and click on the "Get Route" button to receive some Route tokens in the Fuji contract.CrossTalk works on a prepaid fee model. Upon receiving the CrossTalk Request, the Router chain will calculate the estimated fee for executing the transaction on the destination chain in terms of ROUTE tokens and deduct the fee plus incentive from the feePayer address upfront.Fee and relayer incentive for any cross-chain request on Router have to be paid in ROUTE tokens only

![image](https://user-images.githubusercontent.com/124175970/228421799-e89e1a5e-471a-4629-8707-693e2a1520a9.png)


🚂 **Transfer minted ERC-721 tokens from source chain to destination chain:**

To transfer minted ERC-721 tokens from source chain to destination chain, we make use of transferCrosschain function, which burns token with given id on source chain and mint the same token having same id on the destination chain. For more info, go to [`Transferring tokens from a source chain to a destination chain`](#Transferring-tokens-from-a-source-chain-to-a-destination-chain)

🔍 **Browse to [Router Devnet Explorer](https://devnet-explorer.routerprotocol.com/crosstalks)** to see the transactions made. Wait for sometime till you see 4 green checks in your transaction column.This indicates, the tokens have been successfully transferred to the destination chain

[Router Devnet Docs](http://devnet-docs.routerprotocol.com/crosstalk/understanding-crosstalk)**



# `Assignment description`

**To build a CrossChain NFT using Router CrossTalk with the following instructions:-**

1. Give the NFT a name - "Your name" and symbol - "Your Name's first and 2nd name first letter used as abbreviation".

2. Use Mumbai Testnet as the source chain and Fuji Testnet as the destination chain.

3. Mint the NFT with id = 450 on the source chain.

4. Transfer the NFT from the source chain to the destination chain.

5. Commit your solidity file to the repository.

6. Copy the transaction hash from the Router Explorer and submit in this [form](https://docs.google.com/forms/d/e/1FAIpQLSd8Xuiuw32kOqGsWmT5s7GLjLVZ_rHXw9bAJbdbr0XzrVG6RA/viewform?embedded=true) 

**Number of Points:**

You will earn 100 points after you have been evaluated based on the assignmnet.

# `Evaluation Process:`

We'll evaluate you on the basis of the following :

1. Whether you made use of the CrossTalk Library to build the CrossChain NFT.

2. Whether you followed all the instructions given in **Assignment description** or not

3. Whether you transferred the NFT from the source chain (Mumbai Testnet) to the destination chain (Fuji Testnet) using Router CrossTalk. We check this by the transaction hash that you provide in the form]

# `Recommended qualifications`

**Desired Skills:**

- Familiarity with the Git and GitHub
- Familiarity with Basics of Blockchain.
- Familiarity with Basics of Solidity Language.
- Understands the need of going Cross-Chain.


### Eligibility

To participate, you must be:

* 16 years or older

* Passionate about Web3 









