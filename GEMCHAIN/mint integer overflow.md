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





### bonusToken

https://etherscan.io/address/0x362dcc7187cf0c47be45695549c6b4fb96c08875#code


```
    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }
```



### CryptonitexCoin

https://etherscan.io/address/0x2c0c06dae6bc7d7d7d8b0d67a1f1a47d6165e373#code

```
    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }
```
 
 

### AssetToken

https://etherscan.io/address/0x0bdbc0748ba09fbe9e9ed5938532e41446c2f033#code

```
	function mintToken(address target, uint256 mintedAmount) onlyAdmin{
		balanceOf[target] += mintedAmount;
		totalSupply += mintedAmount;
		Transfer(0, this, mintedAmount);
		Transfer(this, target, mintedAmount);
	}
```

### bankcoin

https://etherscan.io/address/0xf3836bc7415dfb67b4bf8427e37705b1a81e1173#code


```
	function mintToken(address target, uint256 mintedAmount) onlyOwner {
		balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, owner, mintedAmount);
        Transfer(owner, target, mintedAmount);
    }

  ```
### AssetToken

https://etherscan.io/address/0x6248211b830ce0191c7643b19f5ddb059e018672#code


```
	function mintToken(address target, uint256 mintedAmount) onlyAdmin{
		balanceOf[target] += mintedAmount;
		totalSupply += mintedAmount;
		Transfer(0, this, mintedAmount);
		Transfer(this, target, mintedAmount);
	}

```
### etktokens

https://etherscan.io/address/0xce58d27fd266e63c4055ce1b77c6fd6e0a74190b#code


```
	function mintToken(address target, uint256 mintedAmount) onlyOwner {
		balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, owner, mintedAmount);
        Transfer(owner, target, mintedAmount);
    }
```


### MultiGamesToken

https://etherscan.io/address/0x52a5e1a56a124dce84e548ff96122246e46d599f#code

```
    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }

```

### ALEX (ALEX)


https://etherscan.io/address/0x04ed15fa8c47778589c1bf3451e0de25c1eed3ae#code
```
    function mintToken(address target, uint256 mintedAmount) onlyOwner {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, owner, mintedAmount);
        Transfer(owner, target, mintedAmount);
    }
```




### Ethernet Cash (ENC)

https://etherscan.io/address/0x039f5050de4908f9b5ddf40a4f3aa3f329086387#code

```
    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }
```


### EPPCOIN (EPP)

https://etherscan.io/address/0x759981e5af7661836d305f71779690808c1de51f#code

```
    /// @notice Create `mintedAmount` tokens and send it to `target`
    /// @param target Address to receive the tokens
    /// @param mintedAmount the amount of tokens it will receive
    function mintToken(address target, uint256 mintedAmount) onlyOwner public {
        balanceOf[target] += mintedAmount;
        totalSupply += mintedAmount;
        Transfer(0, this, mintedAmount);
        Transfer(this, target, mintedAmount);
    }
```



##### ...
