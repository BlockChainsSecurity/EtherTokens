### ETHEREUMBLACK

https://etherscan.io/address/0xE2fA3d7B292c216390AbAd4c625d5f2524B85A1f#code

```javascript
function sell(uint256 amount) {
	if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
    	balanceOf[this] += amount;                         // adds the amount to owners balance
    	balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
	if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
    	throw;                                         // to do this last to avoid recursion attacks
	} else {
    	Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
	}
}
```

This contract could be used  to trade ETHEREUMBLACK (ETCBK) tokens using ETHs. However there exists a integer overflow in function `sell()`. 

The owner of the contract could set `sellPrice` and `buyPrice` using `setPrices()` function. For example,  after some transactions, the owner could set sellPrice to 0x8000000000000000000000000000000000000000000000000000000000000000. When some user wanted to sell 2 ETCBKs for ETHs back，`amount * sellPrice` equals 0. Thus the seller gave out 2 ETCBKs but none ETHs was retrieved. The contract still kept it, which makes this token unsafe.



### Similar Vulnerabilies

Other tokens found vulnerable by us are listed below. These ones have similar code pattern.

##### CCindexToken
https://etherscan.io/address/0xab3a93b317def7426c8345538690036cb92a11e6#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### MyAdvancedToken
https://etherscan.io/address/0x223499d60fE7E3Dc5339e8219e708D18bfc2E6Fe#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### MyBoToken
https://etherscan.io/address/0x3ac96bbe8b60d715fd818b3fe242edf9def20571#code
```javascript
function sell(uint256 amount) {
    if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
    balanceOf[this] += amount;                         // adds the amount to owners balance
    balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
    if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
      throw;                                         // to do this last to avoid recursion attacks
    } else {
      Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
    }
  }
```

##### SwapToken
https://etherscan.io/address/0x27054b13b1b798b345b591a4d22e6562d47ea75a#code
```javascript
function sellBuyerTokens(uint amount) returns (uint revenue){
        if (creditStatus == false) throw;                       // checks if buyer is eligible for a claim
        if (balanceOfBuyer[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOfBuyer[this] += amount;                         // adds the amount to owners balance
        balanceOfBuyer[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        revenue = amount * cPT;
        if (!msg.sender.send(revenue)) {                   // sends ether to the seller: its important
            throw;                                         // to do this last to prevent recursion attacks
        } else {
            Transfer(msg.sender, this, amount);             // executes an event reflecting on the change
            return revenue;                                 // ends function and returns
        }
    }
```

##### TSwap
https://etherscan.io/address/0x125c0260feec92471d1a144f3cdce185a565f374#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### STE
https://etherscan.io/address/0xeba49ddea9f59f0a80ecbb1fb7a585ce0bfe5a5e#code
```javascript
function sell(uint256 amount) public {
        if (sellPrice == 0) revert();
        if (balanceOf[msg.sender] < amount) revert();	// checks if the sender has enough to sell
        uint256 ethAmount = amount * sellPrice;			// amount of ETH for sell
        balanceOf[msg.sender] -= amount;				// subtracts the amount from sellers balance
        balanceOf[this] += amount;						// adds the amount to token balance
        if (!msg.sender.send(ethAmount)) revert();		// sends ether to the seller.
        Transfer(msg.sender, this, amount);
    }
```

##### ETHERCASH
https://etherscan.io/address/0xd7cf04472739aaa2565af739e2e1d08f99ec8981#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### WelfareTokenFund
https://etherscan.io/address/0x83b6ad8e37ab7a4f71da533a35271484270ec6c2#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### ProgressiveToken
https://etherscan.io/address/0xa4f061ad427d0dcd51f511e639bab0a3497e428d#code
```javascript
function sell(uint amount) returns (uint revenue){
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        reward=getReward(now);                             //calculating current reward.
        if(currentSupply + reward > totalSupply ) throw;   // check for totalSupply.
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        balanceOf[block.coinbase]+=reward;                 // rewarding the miner.
        updateCurrentSupply();                             //updating currentSupply.
        revenue = amount * sellPrice;                      // amount (in wei) corresponsing to no of coins.
        if (!msg.sender.send(revenue)) {                   // sends ether to the seller: its important
            throw;                                         // to do this last to prevent recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
            return revenue;                                // ends function and returns
        }
    }
```

##### MyToken
https://etherscan.io/address/0xaae6b19867d40aa105c7256b44010d79dbdaa031#code
```javascript
function sell(uint amount) returns (uint revenue){
            if (balanceOf[msg.sender] < amount ) throw;       
            balanceOf[this] += amount;                        
            balanceOf[msg.sender] -= amount;                  
            revenue = amount * sellPrice;                     
            msg.sender.send(revenue);                         
            Transfer(msg.sender, this, amount);                
            return revenue;                                    
        }
```

##### PornCoin
https://etherscan.io/address/0xc310755f88145cabcaa06c714cd668b5465dceaa#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### Ohni
https://etherscan.io/address/0x6f539a9456a5bcb6334a1a41207c3788f5825207#code
```javascript
function sell(uint256 amount) {
		checkForUpdates();
		if (sellPrice == 0) throw;
		if (balanceOf[msg.sender] < amount) throw; // checks if the sender has enough to sell
		balanceOf[this] += amount; // adds the amount to owners balance
		balanceOf[msg.sender] -= amount; // subtracts the amount from sellers balance
		if (!msg.sender.send(amount * sellPrice)) { // sends ether to the seller. Its important
			throw; // to do this last to avoid recursion attacks
		} else {
			Transfer(msg.sender, this, amount); // executes an event reflecting on the change
		}
	}
```

##### MyAdvancedToken7
https://etherscan.io/address/0x223499d60fE7E3Dc5339e8219e708D18bfc2E6Fe#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) revert();        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        
        
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            revert();                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### EthereumLegit
https://etherscan.io/address/0xbaf9d121d6447b19e95f48fad834a0dff1a92691#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### ProvidenceCasinoToken
https://etherscan.io/address/0x50584a9bdfab54b82e620b8a14cc082b07886841#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### MoneyTreeToken
https://etherscan.io/address/0x070c9244a54353a0f9c43670b21856df2cc4e439#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### PVE
https://etherscan.io/address/0x1FF56987B459d1Bc67A89879d00448F3de46e12D#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### TravelCoinToken
https://etherscan.io/address/0x23cb17d7d079518dbff4febb6efcc0de58d8c984#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### NectarCoin
https://etherscan.io/address/0x5e0D4C7713914d17989Ff5Bcdfa5583dD714e65F#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### ETH033
https://etherscan.io/address/0xa47178da1119218bc2a8dd9e3251ee89b7c7e7f0#code
```javascript
function sell(uint amount) returns (uint revenue){
    if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
    balanceOf[this] += amount;                         // adds the amount to owners balance
    balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
    revenue = amount * sellPrice;
    if (!msg.sender.send(revenue)) {                   // sends ether to the seller: its important
        throw;                                         // to do this last to prevent recursion attacks
    } else {
        Transfer(msg.sender, this, amount);             // executes an event reflecting on the change
        return revenue;                                 // ends function and returns
    }
}
```

##### ExtremeToken
https://etherscan.io/address/0xff1560afef58be59b11c72734ad1d89db63e4e71#code
```javascript
function sell(uint256 amount) {
        if (balances[msg.sender] < amount ) throw;
        balances[this] += amount;
        balances[msg.sender] -= amount;
        if (!msg.sender.send(amount * sellPrice)) {
            throw;
        } else {
            Transfer(msg.sender, this, amount);
        }               
    }
```

##### ObjectToken
https://etherscan.io/address/0x868326eFCA6e89F75a76D141167759f1AD10854C#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### MAVCash
https://etherscan.io/address/0x61dc161B06088b9cbaaD53391134929A83D1EB7A#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### cashBackMintable
https://etherscan.io/address/0xb5bfe2803e37525ac9f16a60f208b1c33c878347#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### CoinToken
https://etherscan.io/address/0x2cbd64273066bc181c792eaacdc8e5e522ef94d7#code
```javascript
function sell(uint256 amount) {
    if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
    balanceOf[this] += amount;                         // adds the amount to owners balance
    balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
    if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
      throw;                                         // to do this last to avoid recursion attacks
    } else {
      Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
    }
  }
```

##### ICODollar
https://etherscan.io/address/0x7dfc425c0425d69ca577d76c6d53a26a6c2cc0ac#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### GreenMed
https://etherscan.io/address/0xb444208cB0516C150178fCf9a52604BC04A1aCEa#code
```javascript
function sell(uint256 amount) {
        if (balances[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balances[this] += amount;                         // adds the amount to owners balance
        balances[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### GMile
https://etherscan.io/address/0x8ba49452e12449240425de9895b1aa51f5f3b90d#code
```javascript
function sell(uint256 amount) {if (balanceOf[msg.sender] < amount ) throw;balanceOf[this] += amount;balanceOf[msg.sender] -= amount;if (!msg.sender.send(amount * sellPrice)) {throw;} else {Transfer(msg.sender, this, amount);}}
```

##### RTokenMain
https://etherscan.io/address/0x79ba6302bdb1c601a54b656e23a5bc3a2d5914b3#code
```javascript
function sell(uint256 amount) {
    if(balanceMap[msg.sender] < amount)
      throw;
    balanceMap[msg.sender] -= amount;
    balanceMap[this] += amount;
    if(!msg.sender.send(amount*sellPrice))
      throw;
    else
      Transfer(msg.sender, this, amount);
  }
```

##### DestiNeedToken
https://etherscan.io/address/0xdff8e7f5496d1e1a4af3497cb4712017a9c65442#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### GSI
https://etherscan.io/address/0xCE3b5fFca16ffF926c890f0885A3e90cEb89db0A#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }               
    }
```

##### EnterToken
https://etherscan.io/address/0xb1bd9e21ccbec1102e61e6613bdd018eaa24c77b#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### RiptideCoin
https://etherscan.io/address/0xdd007278b667f6bef52fd0a4c23604aa1f96039a#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### Crowdnext
https://etherscan.io/address/0xc52694e7832594f2aaf2536c777024fb5c1ae9da#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### TokenERC20
https://etherscan.io/address/0x70807fa9343ee3d7d6e9d8602bf3ca867cc86479#code
```javascript
function sell(uint amount) returns (uint revenue){
            if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
            balanceOf[this] += amount;                         // adds the amount to owners balance
            balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
            revenue = amount * sellPrice;                      // calculate the revenue
            msg.sender.send(revenue);                          // sends ether to the seller
            Transfer(msg.sender, this, amount);                // executes an event reflecting on the change
            return revenue;                                    // ends function and returns
        }
```

##### MoneyChainNetToken
https://etherscan.io/address/0x77727ef417696f95a10652cf2d02d6421dda5048#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

##### YLCToken
https://etherscan.io/address/0x9f03d94bf3545153cb28014bc7d1e7177ca99034#code
```javascript
function sell(uint256 amount) {
    assert (balanceOf[msg.sender] >= amount );         // checks if the sender has enough to sell
    balanceOf[this] += amount;                         // adds the amount to owners balance
    balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
    assert (msg.sender.send(amount * sellPrice));      // sends ether to the seller. Its important
                                                       // to do this last to avoid recursion attacks
    Transfer(msg.sender, this, amount);                // executes an event reflecting on the change
  }
```

##### MyYLCToken
https://etherscan.io/address/0x9f03d94bf3545153cb28014bc7d1e7177ca99034#code
```javascript
function sell(uint256 amount) {
    assert (balanceOf[msg.sender] >= amount );         // checks if the sender has enough to sell
    balanceOf[this] += amount;                         // adds the amount to owners balance
    balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
    assert (msg.sender.send(amount * sellPrice));      // sends ether to the seller. Its important
                                                       // to do this last to avoid recursion attacks
    Transfer(msg.sender, this, amount);                // executes an event reflecting on the change
  }
```

##### EnterCoin
https://etherscan.io/address/0x08e836f7d4804d39e798b6459fa54543f260d4c0#code
```javascript
function sell(uint256 amount) {
        if (balanceOf[msg.sender] < amount ) throw;        // checks if the sender has enough to sell
        balanceOf[this] += amount;                         // adds the amount to owners balance
        balanceOf[msg.sender] -= amount;                   // subtracts the amount from sellers balance
        if (!msg.sender.send(amount * sellPrice)) {        // sends ether to the seller. Its important
            throw;                                         // to do this last to avoid recursion attacks
        } else {
            Transfer(msg.sender, this, amount);            // executes an event reflecting on the change
        }
    }
```

