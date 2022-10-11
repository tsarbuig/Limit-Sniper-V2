# Limit-Sniper-V2

Read our intro: https://medium.com/@tsarbuig/a-fresh-new-start-for-limitswap-sniper-bd6efaaf40c

&nbsp;

![image](https://user-images.githubusercontent.com/70858574/194782261-ff9876d5-9bfe-4db5-bb56-866049b1b3a5.png)

&nbsp;

LimitSwap team has worked hard to deliver you a brand new Sniper bot, designed to be the best-in-class in the Market

Our new bot will provide you all the tools you need to become a successful sniper :

- **1000x faster** than Sniper V1 thanks to JavaScript
- **Custom contract** sniping
- **Pinksale** sniping
- **Automatic anti-rug** tool (frontrun rugs when liquidity is removed / you get blacklisted / etc.)
- **Automatic selling** after xx% profits
- **Profits calculator**
- Automatic **MaxTxAmount detection**
- **Multiple buys** with several wallets in same Tx (example : buy 1000 tokens with 5 different wallets → click here for Tx )

&nbsp;

# Things you need to know
1/ You need a private or semi private node to make it work (because it scans mempool) --> if you don't have one already, please contact our official node provider, @zdarfa on Telegram (https://moppynodes.com/)

2/ Sniper currently works on ETH and BSC, but ask me if you want me to add more chain (MATIC / FTM / etc.)
&nbsp;




&nbsp;

# How can I buy it?
Join our Telegram channel for more infos:  https://t.me/LimitSwap 

&nbsp;

# Bot configuration

#### BUY / SELL  PARAMETERS
```yaml
KIND_OF_SWAP: "base", 
    // Available values : 
    - base --> buy a fixed amount of ETH/BNB
    - tokens --> buy a fixed amount of tokens

BUY_AMOUNT_IN_BASE: "0.1", // used if KIND_OF_SWAP = base --> enter the ETH/BNB buy amount you want to use
BUY_AMOUNT_IN_TOKENS: "1000", // used if KIND_OF_SWAP = tokens --> enter the amount of tokens you want to buy
SLIPPAGE: "40%", // put only integer numbers here (no decimals)

SELL_MODE: "autosell", 
    // available values : 
    - autosell --> will copy buy Tx but will sell automatically after xx% of profit. Target is defined by AUTOSELL_PROFIT parameter
    - donotsell --> will not try to sell

SELL_AMOUNT: "100%", // it will sell  xx%  of the amount of those tokens that you hold in your wallet
AUTOSELL_PROFIT: "200%", // if you use 'autosell' mode, bot will automatically sell token when price has reached buyprice * AUTOSELL_PROFIT

BUYAFTER_XXX_SECONDS : 0,  // if you want the bot to wait XXX seconds before buying
```

#### COUNTER ANTI BOT PARAMETERS
```yaml
SUPER_FAST_SNIPE_WITHOUT_PRECHECKS : false, // if true, all controls below will be disabled
MINIMUM_LIQUIDITY_IN_DOLLARS : 1000,  // minimum value of liquidity added to make the bot buy. Team recommend to put 1000 minimum
HONEYPOT_AND_TAX_CHECK : false, // check if token is a honeypot before buying --> this control will take from 0.02s to 0.008s depending on your node
MAX_BUY_TAX : "40%", // used if HONEYPOT_AND_TAX_CHECK = true --> bot won't buy if buy tax > MAX_BUY_TAX
MAX_SELL_TAX : "40%", // used if HONEYPOT_AND_TAX_CHECK = true --> bot won't buy if sell tax > MAX_SELL_TAX
```

#### COUNTER ANTI BOT PARAMETERS
```yaml
AMOUNT_OF_BUYS: 2, // increment number if you want the bot to make multiple buys in the same Tx. Only compatible with USE_CUSTOM_CONTRACT = true
TOKENS_DESTINATION: "main_wallet", 
    // available values : 
    - main_wallet --> all the tokens of your multiplebuy will be sent to your main trading wallet
    - multiple_wallets --> the tokens of your multiplebuy will be sent to wallets defined in WALLETS_RECIPIENT

WALLETS_RECIPIENTS: ["0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig", "0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig"], // list of wallets where tokens will be transferred if TOKENS_DESTINATION = 'multiple_wallets'
```

#### GAS PARAMETERS
```yaml
// GAS will be calculated automatically, it needs to be same as addliquidity / opentrading Tx
```

#### ANTIRUG PARAMETERS  
```yaml
ACTIVATE_ANTIRUG : true, // use it if the wallet you track does not have its own antirug protection
LIQUIDITY_REMOVAL_PERCENTAGE : 30, // Force sell all your tokens is liquidity removal > LIQUIDITY_REMOVAL_PERCENTAGE
GAS_MULTIPLIER : 2.0, // in case of force sell after detecting a rug
```

#### PINKSALE
```yaml
PINKSALE_PRESALE_ADDRESS : "0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig", // for BUY_MODE = pinksale
```

#### CONTRACT BOT
```yaml
USE_CUSTOM_CONTRACT : true,
CONTRACT_BOT : "0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig", // Enter here the contract address that you got after deploying contract
```
&nbsp;

# Dedicated modes

#### FORCESELL mode
```yaml
./SniperV2 --forcesell  : use this mode if you want to sell all your tokens in 1 click
```

#### AUTOSELL mode
```yaml
./SniperV2 --autosell  : use this mode if you want he bot to sell all your tokens after a xx% profit 
```

#### ANTIRUG mode
```yaml
./SniperV2 --antirug  : use this mode if you want to start antirug mode on a token you already hold
```
&nbsp;

# Examples of Tx with MULTIBUY modes (with custom contract only)

```yaml
// Send 5 buys made in tokens to your trading wallet
KIND_OF_SWAP: "base",
BUY_AMOUNT_IN_BASE: "0.0001",
AMOUNT_OF_BUYS: 5,
TOKENS_DESTINATION: "main_wallet", 
```
<img width="734" alt="image" src="https://user-images.githubusercontent.com/70858574/195204453-e45f313f-29ad-461b-a0fb-13c661367f5a.png">


```yaml
// Send 5 buys made in WBNB to your trading wallet
KIND_OF_SWAP: "tokens",
BUY_AMOUNT_IN_TOKENS: "1000",
AMOUNT_OF_BUYS: 5,
TOKENS_DESTINATION: "main_wallet", 
```
<img width="723" alt="image" src="https://user-images.githubusercontent.com/70858574/195205348-eae4e2ce-1d9e-4722-a12d-acb05cde5ad4.png">


```yaml
// Send 3 buys made in WBNB to 3 different wallets
KIND_OF_SWAP: "base",
BUY_AMOUNT_IN_BASE: "0.0001",
AMOUNT_OF_BUYS: 3,
TOKENS_DESTINATION: "multiple_wallets", 
WALLETS_RECIPIENTS: ["0x200E4Fe41faF92C96bd74c711738Ad550175A779", "0x5aa376af6a5d99d051c3f994de26bb5ae234da26", "0xf62803b9f8a146d07b993ad08bda8de91dde8690"],
```
![image](https://user-images.githubusercontent.com/70858574/195206368-a3049377-354f-40f4-b667-40732514f89e.png)


```yaml
// Sent 3 buys made in tokens to 3 different wallets
KIND_OF_SWAP: "tokens",
BUY_AMOUNT_IN_TOKENS: "1000",
AMOUNT_OF_BUYS: 3,
TOKENS_DESTINATION: "multiple_wallets", 
WALLETS_RECIPIENTS: ["0x200E4Fe41faF92C96bd74c711738Ad550175A779", "0x5aa376af6a5d99d051c3f994de26bb5ae234da26", "0xf62803b9f8a146d07b993ad08bda8de91dde8690"],
```
![image](https://user-images.githubusercontent.com/70858574/195205954-a0c44fd1-2717-49a4-b590-a5135622b424.png)

