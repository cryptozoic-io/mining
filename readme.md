# Cryptozoic mining

Cryptozoic main net is working normally , any miners can join and mine.

## 1.Miners

There are two kinds of miners in cryptozoic , one is Lite miner and another one is Super miner. The descriptions of miners are following:

### 1.1 Lite Miner

Lite miner can mine normally and get the 10% of the rewards. There is only one requirement

* **1.Prepare one or more mining machines built-in the mining software.**

#### R**eward of lite miner **

| beginning block number | ending block number | reward of block | reward of lite miner |
| :--- | :--- | :--- | :--- |
| 1 | 1,280,000 | 64 VCC | 6.4 VCC |
| 1,280,001 | 3,840,000 | 32 VCC | 3.2 VCC |
| 3,840,001 | 7,680,000 | 16 VCC | 1.6 VCC |
| 7,680,001 | 12,800,000 | 8 VCC | 0.8 VCC |
| 12,800,001 | 19,200,000 | 4 VCC | 0.4 VCC |
| 19,200,001 | endless | 2 VCC | 0.2 VCC |

### 1.2 Super Miner

Super miner can mine convictively and get the between 20% - 65% of the rewards. There are two requirements if you wanna be a super miner

* **1.Prepare one or more mining machines built-in the mining software.**
* **2.The coinbase of miner must hold the specified amount of VCC**

#### Types

There are five levels in super miners. Level depends on  the amount of VCC which is held by the coinbase of miner.Super miner at different level gets different reward when getting mined.

The details are following:

| Level of Super Miner | Amount of VCC to be held | Reward Percent of Total Rewards |
| :--- | :--- | :--- |
| SuperMiner Lv. 1 | 2,000,000 VCC | 20% |
| SuperMiner Lv. 2 | 4,000,000 VCC | 30% |
| SuperMiner Lv. 3 | 8,000,000 VCC | 40% |
| SuperMiner Lv. 4 | 12,000,000 VCC | 50% |
| SuperMiner Lv .5 | 16,000,000 VCC | 65% |

#### **Reward of super miner.**

| beginning block number | ending block number | reward of block | reward of Lv.1 | reward of Lv.2 | reward of Lv.3 | reward of Lv.4 | reward of Lv.5 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1,280,000 | 64 VCC | 12.80  VCC | 19.20 VCC | 25.60 VCC | 32.00 VCC | 41.60 VCC |
| 1,280,001 | 3,840,000 | 32 VCC | 6.40  VCC | 9.60 VCC | 12.80 VCC | 16.00 VCC | 20.80 VCC |
| 3,840,001 | 7,680,000 | 16 VCC | 3.20  VCC | 4.80 VCC | 6.40 VCC | 8.00 VCC | 10.40 VCC |
| 7,680,001 | 12,800,000 | 8 VCC | 1.60    VCC | 2.40 VCC | 3.20 VCC | 4.00 VCC | 5.20 VCC |
| 12,800,001 | 19,200,000 | 4 VCC | 0.80    VCC | 1.20 VCC | 1.60 VCC | 2.00 VCC | 2.60 VCC |
| 19,200,001 | endless | 2 VCC | 0.40    VCC | 0.60 VCC | 0.80 VCC | 1.00 VCC | 1.30 VCC |

## 2. Reward of new block

The reward of new block divides into 4 parts

* Making-A-Wish program
* Super nodes
* Miners
* Destroy

The details are as following.

| Making-A-Wish Program | Super Nodes | Miners | Destory |
| :--- | :--- | :--- | :--- |
| 5% | 30% | 10-65% | 0-55%\(Depends on the miners' reward amount\) |

Note that miners' reward is dynamic base on the Cryptozoic-POS.The left is sent to destroyed.

For Example.

**Case 1. Lite miner get mined**

If a lite miner get mined at block 183000 when the total reward is 64VCC. the reward's detail is like this:

| Total Reward | Making-A-Wish Program\(5%\) | Super Nodes\(30%\) | LiteMiner\(10%\) | Destory\(Remain:1-5%-30%-10% = 55%\) |
| :--- | :--- | :--- | :--- | :--- |
| 64 | 64\*5% = 3.2 | 64\*30% = 19.2 VCC | 64\*10% = 6.4 VCC | 64 \* 55% = 35.2 VCC |

**Case 2. Super miner get mined**

If a Super miner Lv.5 get mined at block 183000 when the total reward is 64VCC.the reward's detail is like this:

| Total Reward | Making-A-Wish Program\(5%\) | Super Nodes\(30%\) | Super Miner Lv.5\( 65% \) | Destory\(Remain:1-5%-30%-65% = 0%\) |
| :--- | :--- | :--- | :--- | :--- |
| 64 | 64\*5% = 3.2 | 64\*30% = 19.2 VCC | 64\*10% = 41.6 VCC | 64 \* 0% = 0 VCC |

## 3. Principle of Mining

### 3.1 How to judge the miner type?

As shown above in 1.2 Super Miner, the difference of Lite miner and Super miner is whether if miners holds the specified amount of VCC.

### 3.2 How to reward differently when mining?

the reward will be calculated when a block is generated.So the processing of reward are:

* step 1. get the VCC amount of the current miner's coinbase.
* step 2. determine the level of the miner
* step 3. calculate the reward
* step 4. add reward to the coinbase
* step 5. destroy the left part.

the pseudo code is like this:

```js
//firstly. get the VCC amount of the current miner's coinbase.
var coinbaseVCCAmont = miner.header.getBalance();

//secondly. calculate the total reward of new block
var totalReward = ...;    //
var blockHeight = block.header.getBlockHeight();
if(blockHeight<=1280000){
    totalReward = 64.00 ;
}else if(blockHeight<=3840000){
    totalReward = 32.00 ;
}else if(blockHeight<=7680000){
    totalReward = 16.00 ;
}else if(blockHeight<=12800000){
    totalReward = 8.00 ;
}else if(blockHeight<=19200000){
    totalReward = 4.00 ;
}else {
    totalReward = 2.00 ;
}

//thirdly. determine the level of current miner and calculate the reward 
var minerReward;
if(coinbaseVCCAmont>=160000000 ){
    //super miner Lv.5 gets the 65%
    minerReward = totalReward * 0.65;
}else if(coinbaseVCCAmont>=12000000 ){
    //super miner Lv.4 gets the 50%
    minerReward = totalReward * 0.50;
}else if(coinbaseVCCAmont>=8000000 ){
    //super miner Lv.3 gets the 40%
    minerReward = totalReward * 0.40;
}else if(coinbaseVCCAmont>=4000000 ){
    //super miner Lv.2 gets the 30%
    minerReward = totalReward * 0.30;
}else if(coinbaseVCCAmont>=2000000 ){
    //super miner Lv.1 gets the 20%
    minerReward = totalReward * 0.20;
}else{
    //lite miner gets the 10%
    minerReward = totalReward * 0.10;
}

//forth. add the reward to the coinbase
...
addBalance(miner.header.getCoinBase,minerReward);

//last. destroy the left
...
var rewardToDestroy = totalReward - 0.35*totalReward - minerReward;
var destroyAddress = "0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFD"
addBalance(destroyAddress,rewardToDestroy);
```

### 3.3 updating time

This mining principle is going to effect at the block 183000.the earth time is about at Jul 26 2019.

## 4. Locale Mining

All miners can mine locally by using the gvc client which supplies the mining interface.Only machines built-in CPU can mine locally.

get the gvc client from github:

> [https://github.com/cryptozoic-io/support/tree/master/downloads](https://github.com/cryptozoic-io/support/tree/master/downloads)

## 5. Mining Pool

Everyone can build up a mining pool and get the rewards of mining.

every Ethereum mining pool and Ethereum mining machine can mine Cryptozoic.

pool likes:

OpenEtherumPool:[https://github.com/sammy007/open-ethereum-pool](https://github.com/sammy007/open-ethereum-pool)

software likes:

ETHMiner:[https://github.com/ethereum-mining/ethminer](https://github.com/ethereum-mining/ethminer)

