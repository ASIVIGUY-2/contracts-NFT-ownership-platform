// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @title FractionalizedNFT
 * @dev Allows fractional ownership of a single NFT by dividing it into shares.
 */
contract FractionalizedNFT {
    address public owner;
    uint256 public nftId;
    uint256 public totalShares;
    uint256 public pricePerShare;
    bool public initialized;

    mapping(address => uint256) public shares;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    /**
     * @dev Initializes the fractional NFT with NFT ID, total shares, and price per share.
     */
    function initializeFractionalNFT(
        uint256 _nftId,
        uint256 _totalShares,
        uint256 _pricePerShare
    ) external onlyOwner {
        require(!initialized, "Already initialized");
        require(_totalShares > 0 && _pricePerShare > 0, "Invalid inputs");

        nftId = _nftId;
        totalShares = _totalShares;
        pricePerShare = _pricePerShare;
        initialized = true;
    }

    /**
     * @dev Allows users to buy a specific number of shares.
     */
    function buyShares(uint256 numberOfShares) external payable {
        require(initialized, "Not initialized");
        require(numberOfShares > 0, "Invalid share amount");
        require(msg.value == numberOfShares * pricePerShare, "Incorrect payment");
        require(totalShares >= numberOfShares, "Not enough shares left");

        shares[msg.sender] += numberOfShares;
        totalShares -= numberOfShares;
    }

    /**
     * @dev Returns the number of shares owned by the sender.
     */
    function getMyShares() external view returns (uint256) {
        return shares[msg.sender];
    }
}
