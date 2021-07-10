# ERC721-Base-Code
A simplification of the ERC721 standard for NFT smart contract development on Ethereum blockchain

I built this codebase while learning Solidity and it cemented everything that I've accumulated.
I don't want other people to struggle, or at the very least would like to reduce the burden. Digging
through the OpenZeppelin libraries was a pain, finding detailed information about specific portions
of the code was a pain, and the standard itself is murky in some places, so I wanted to make things
better.

Thus, this code base.
This fulfills all of the requirements of the ERC721 standard and most of the options, but it is
missing some things that the programmer will need to change from any blank document anyway. This
README will fill you in on the missing details, the rest is free to study.

First, the existing code. The whole standard has been reduced to two files. One contains all of the 
interfaces needed to make a basic NFT. The other is the solidity code base. A copy of this should
be in every Solidity programmer's library, as having everything in one place makes it easier to 
see what different parts of the code are doing without digging through dozens of library files and
online blogs. You get to see it in action.

Things to do.
The first line is a comment that documents the license for this file: MIT.
The solidity version statement is next, and this code was written to comply with the most up to date
version available on Remix, 0.8.6. If you are using a 0.7 version or earlier, then you may need to
make some changes to the way functions are defined.

Following is the import block, which loads the interfaces into the code. These are important if you
wish to interact with other contracts, and ERC165 is a necessary requirement for this code block. It 
will throw an error if ERC165 isn't present, so it is included in interfaces.sol with the rest of the
standard interfaces.

Pro Tip: You don't need to have your interfaces in separate files, Remix will let you batch them.

The name of the contract can and should be changed, obviously, but you will need to also change it in
the constructor. We'll come to that in a moment.

The events list is the minimum required by the standard. Feel free to add more as needed.

State variables and mappings are declared next. If you feel like changing these names to something better
suited, feel free to do a replace-all. You might notice that there are a couple things missing here as 
well that aren't required, but easier to add them as you need them.

Constructor:
totalSupply is defaulted to 0, and msg.sender is defined as the owner of the contract. Then the fun starts.
The declaration of contractname is the other place where you will need to change the name of the contract.
If you are new, the placement may seem odd here. You are basically creating a pointer from the contract
back to itself to limit the use of "this." Security issues come up occasionally by using "this" as the
pointer, so contractname was created, and is being used here to deliver all of the necessary bytes4 hashes
that allow other contracts to determine what you have implemented.

If you don't wish your final contract to receive other NFTs, you may want to comment out the TokenReceiver
and ERC165, but it is urged that you set up some way to handle a delivered NFT and leave them in to 
conform to the standard. How you handle them is up to you, and there is no implementation in the code
to impliment wallet functionality of any kind.

Likewise, you may want to add an ERC20 protocol here if you will be handling fungible tokens in your code.
Just follow the pattern you see.

The first block of functions after constructor are the typical metadata functions so that the rest of the
blockchain can see into your code and respond accordingly. These were placed as text strings to simplify
the codebase as much as possible. You may wish to add state variables and replace the string data with
those variables, which is easy to do. It was left in this format to save gas and still provide the 
functionality necessary for minting unique tokens.

There is also no call to mint tokens, handle ERC20 coins, or handle any kind of user indexing for their
NFTs. If you will be minting coins with this code, you are free to create and implement these functions
however you like, as that handling doesn't follow any special naming protocols in the ERC721 standard.

Hopefully, you can see the beauty of having all the necessities in one block of code. There are several
options for using this directly, as follows.

1. add code as needed to complete your NFT project
2. Move the constructor to a separat contract and import this standard to that contract, as:
     contract myContract is ERC721 {
   If you do this, you will also want to change some of the private definitions to internal so they
   can be accessed by your new .sol file.
3. Alternately, you can write your code updates as a separate file and import that into this standard.

Usage:
Upload the two files into the same folder on Remix, and hit compile.
Then code away. Remember to stop and eat at some point, and try not to stay up too late.
