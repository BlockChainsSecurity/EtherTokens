### GEMCHAIN(GEM)



https://etherscan.io/address/0xfb340423dfac531b801d7586c98fe31e12a32f31#code



```javascript
function mintToken(address target, uint256 mintedAmount) public onlyOwner {
    balanceOf[target] += mintedAmount;
    totalSupply += mintedAmount;
    Transfer(0, owner, mintedAmount);
	Transfer(owner, target, mintedAmount);
}
```



The GEM token could be arbitrary minted by its creator in function mintToken(). The balances[target] and ) mintedAmount are a defined as uint, so oprator '+' would definitely result in an integer overflow.



Simulated on Remix:

![](./1.png)

The owner of the contract could mint arbitary amout of (for example 0x8000000000000000000000000000000000000000000000000000000000000000 Wei) subconcurrency GEM to an arbitary user.



![](./2.png)



If the owner of the contract mint another 0x8000000000000000000000000000000000000000000000000000000000000000 GEM to the user again,  integer overflow happened which make balanceOf this user to be 0.

And actually the owner of the contract could control the balance of an arbitary user to be an aribitary value. 



This is a serious problem for digital assets.



### Similar Vulnerabilities

Other tokens found vulnerable by us are listed below. These ones have a similar code pattern.

##### ...