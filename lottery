//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Lottery  {
    address public manager;
    address payable[] public players;

    constructor() {
        manager = msg.sender;
    }

    function enter() public payable {
        require(msg.value == 0.01 ether, "You need send 0.01 ether to enter the lottery");
        players.push(payable(msg.sender));
    }

    modifier restricted() {
        require(msg.sender == manager,"Only manager can call this function");
        _;
    }

    function pickWinner() public restricted {
        require(players.length > 0, "There is no players in the lottery");

        uint index = random() % players.length;
        players[index].transfer(address(this).balance);

        players = new address payable[](0);        
    }

    function getPlayers() public view returns (address payable[] memory) {
        return players;
    }

    function random() private view returns (uint) {
        return uint(keccak256(abi.encodePacked(block.difficulty, block.timestamp, players.length)));
    }
}

