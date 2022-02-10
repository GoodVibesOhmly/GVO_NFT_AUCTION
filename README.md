# Smart Batched Auctions 

Using this method, users submit bids to a smart contract specifying the number of tokens they want and the price they wish to purchase them for. Once the bidding period ended, a clearing price is calculated to match demand and supply. Users who bid above that price claim the NFTs, plus the ETH difference between the bid and the clearing price, whenever they want. Users who bid below get their ETH refunded by the contract. 

## Introduction

An implementation of Smart Batch Auctions for ERC721, based off Paradigm's [A Guide to Designing Effective NFT Launches](https://www.paradigm.xyz/2021/10/a-guide-to-designing-effective-nft-launches/), by [@hasufl](https://twitter.com/hasufl) and [@_anishagnihotri](https://twitter.com/_anishagnihotri). Smart batch auctions follow the spankchain ICO model: during a bidding period, users are able to submit bids for a specificied quantity of tokens and price. After the bidding period is over, a clearing price is set to match demand and supply.
 

## Implementation Notes

A few notes on the current implementation:

### The benefits of fixed supply

The main reason for this is that the NFT supply curve is constant: it’s just equal to some fixed supply n. Hence, we know exactly where it will intersect the demand curve: at the price of the nth highest bid. If we keep the top n bids in a binary heap, we can insert new bids in O(logn), and find a clearing price in O(1). Assuming a fixed supply of 10000 tokens, and multiple bids per user, bidding is only around ~2x more expensive in the auction model than in the raffle. Additionally, finding the clearing price requires minimal gas (we just need to look at the heap), while clearing the lottery raffle is an O(n) operation (knuth shuffle). 


## How to run 

```bash
# Install dependencies
npm install

# test contracts with hardhat
npx hardhat test
```
