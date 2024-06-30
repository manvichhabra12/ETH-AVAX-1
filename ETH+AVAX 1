// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

contract UniquePaymentManager {
    address private  owner;
    uint256 private  totalPayments;
    mapping(address => uint256) private  payments;

    constructor() {
         owner = msg.sender;
    }

    // Function to make a payment
    function makePayment() external payable {
        require(msg.value > 0, "Payment amount must be greater than 0.");

        uint256 paymentAmount = msg.value;
         payments[msg.sender] += paymentAmount;
         totalPayments += paymentAmount;

        assert( totalPayments >= paymentAmount);

        if (paymentAmount > 10 ether) {
            revert("Payment amount exceeds the limit.");
        }
    }

    // Function to withdraw the accumulated payments (only callable by the contract owner)
    function withdrawPayments() external {
        require(msg.sender ==  owner, "Only the contract owner can withdraw payments.");

        uint256 paymentAmount =  payments[msg.sender];
        require(paymentAmount > 0, "No payments available for withdrawal.");

         payments[msg.sender] = 0;
         totalPayments -= paymentAmount;

        payable(msg.sender).transfer(paymentAmount);
    }

    // Function to update the donation limit (only callable by the contract owner)
    function updateDonationLimit(uint256 newLimit) external {
        require(msg.sender ==  owner, "Only the contract owner can update the limit.");
        require(newLimit > 0, "New limit must be greater than 0.");

         donationLimit = newLimit;
    }

    // Function to get the current donation limit
    function getDonationLimit() external view returns (uint256) {
        return  donationLimit;
    }

    uint256 private  donationLimit = 10 ether;
}
