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

# Contact
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

// BUY protection
MINIMUM_LIQUIDITY_IN_DOLLARS : 0,  // minimum value of liquidity added to make the bot buy. Team recommend to put 1000 minimum
HONEYPOT_CHECK : false, 
STOP_IF_BALANCE_IS_LOWER_THAN : 0.2, // bot will stop automatically if balance goes under this amount (to avoid being scammed by honeypot)

```

#### COUNTER ANTI BOT PARAMETERS
```yaml
AMOUNT_OF_BUYS: 2, // increment number if you want the bot to make multiple buys in the same Tx. Only compatible with USE_CUSTOM_CONTRACT = true
TOKENS_DESTINATION: "main_wallet", 
// available values : 
    - main_wallet --> all the tokens of your multiplebuy will be sent to your main trading wallet
    - multiple_wallets --> the tokens of your multiplebuy will be sent to wallets defined in WALLETS_RECIPIENT

WALLETS_RECIPIENTS: ["0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig", "0xtsarbuigtsarbuigtsarbuigtsarbuigtsarbuig"], // List of wallets where tokens will be transferred if TOKENS_DESTINATION = 'multiple_wallets'
BUYAFTER_XXX_SECONDS : 0,  // if you want the bot to wait XXX seconds before buying
```

#### GAS PARAMETERS
```yaml
GAS_FOR_LIQUIDITY_SNIPE: "100%", // use percentage here. Example : with '120%', if tracked wallet uses GAS = 10, you will use GAS = 12. With '100%' it's same as sniped Tx
GAS_BOOST: 40, // only if you use txGas = BOOST
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

# Dedicated modes

#### FORCESELL mode
```yaml
./SniperJs --forcesell  : use this mode if you want to sell all your tokens in 1 click
```

#### AUTOSELL mode
```yaml
./SniperJs --autosell  : use this mode if you want he bot to sell all your tokens after a xx% profit 
```

#### ANTIRUG mode
```yaml
./SniperJs --antirug  : use this mode if you want to start antirug mode on a token you already hold
```
