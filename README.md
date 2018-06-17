# 0xLTC

 
 ## 0xLiteCoin 
 [Deployed on Ethereum](https://etherscan.io/address/0x012fd5049a203df08c02fb2e0ed15ceed10d9ed4
)
 
![0xLitecoin_small](https://raw.githubusercontent.com/0xLiteCoinToken/0xLTC/master/logo.png)

 
 #### An ERC20 token that is mined using PoW through a SmartContract 
  
  * Before the BTC Talk [ANN] ~ 0.0357143% of supply was mined publicly over the period of just under about 1 day.
  * No ICO
  * 84,000,000 tokens total
  * Difficulty target auto-adjusts with PoW hashrate
  * Rewards decrease as more tokens are minted 
  * Compatible with all services that support ERC20 tokens
  
  
   
 #### How does it work?
 
Typically, ERC20 tokens will grant all tokens to the owner or will have an ICO and demand that large amounts of Ether be sent to the owner.   Instead of granting tokens to the 'contract owner', all 0xLitecoin tokens are locked within the smart contract initially.  These tokens are dispensed, 50 at a time, by calling the function 'mint' and using Proof of Work, just like mining Litecoin or Bitcoin.  Here is what that looks like: 


     function mint(uint256 nonce, bytes32 challenge_digest) public returns (bool success) {

       
        uint reward_amount = getMiningReward();

        
        bytes32 digest =  keccak256(challengeNumber, msg.sender, nonce );

         
        if (digest != challenge_digest) revert();

        //the digest must be smaller than the target
        if(uint256(digest) > miningTarget) revert();
     

         uint hashFound = rewardHashesFound[digest];
         rewardHashesFound[digest] = epochCount;
         if(hashFound != 0) revert();  //prevent the same answer from awarding twice

        balances[msg.sender] = balances[msg.sender].add(reward_amount);

        tokensMinted = tokensMinted.add(reward_amount);

        //set readonly diagnostics data
        lastRewardTo = msg.sender;
        lastRewardAmount = reward_amount;
        lastRewardEthBlockNumber = block.number;
        
        //start a new round of mining with a new 'challengeNumber'
         _startNewMiningEpoch();

          Mint(msg.sender, reward_amount, epochCount, challengeNumber );

       return true;

    }
 
 
As you can see, a special number called a 'nonce' has to be passed into this function in order for tokens to be dispensed.  This number has to fit a special 'puzzle' similar to a sudoku puzzle, and this is called Proof of Work.   To find this special number, it is necessary to run a mining program.  



A cpu miner exists for mining 0x tokens and it can be downloaded here: 

https://github.com/0xbitcoin/0xbitcoin-miner


 

 
 
 
 
 ----------
 

  

 
 
