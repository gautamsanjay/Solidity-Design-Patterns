# Self Destruct Pattern

What to do when you are dealing with timed contract e.g. loan contract after bein paid off or a bidding contract which is time based. In both cases contract must be terminated once a milestone has been reached. In such cases "Self Destruct" pattern comes handy. It is used to terminate a contract which means it won't be possible to invoke a function of the smart contract and no transactions will be loggged in the ledger. It doesn't mean that any existing data will be deleted from the blockchain becasue it can't be. 

// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.7.0 <0.9.0;
contract TestSelfDestructPattern {
      
    bool public contractEnded;
    address payable public contractCreator;

    modifier isNotFinished(){
        require(contractEnded == false,"Contract is no longer valid");
        _;
    }

    constructor(){
        contractCreator = payable(msg.sender);
    }

    function sendMoneyToContract() public payable isNotFinished() {

    }

    receive() external payable isNotFinished() {

    }

    /**
    Only contract creator can end the contract.
    */
    function  endTheContract() public {
        require(msg.sender == contractCreator,"You are not the creator, can't end the contract");
        contractEnded = true;
        contractCreator.transfer(address(this).balance);

    }

}


# Factory Pattern

# Mapping Iterator

# Withdrawal Pattern

# Name Registry


