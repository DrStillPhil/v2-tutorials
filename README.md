# V2 Tutorials

## Tutorial 1: Basic Multiposition Management

In this tutorial we walk through using ArrakisV2 as a solo LP managing their personal Uniswap V3 liquidity positions on the DAI/WETH token pair.

Follow the tutorial step-by-step with detailed explanations [here](https://google.com) T.B.D

### Step 1: Setup Environment

1. clone repository: `$ git clone https://github.com/ArrakisFinance/v2-tutorials.git`
2. enter repository: `$ cd ~/<whatever directory you are in>/v2-tutorials`
3. download dependencies: `$ yarn` (don't have yarn? see [here](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable))
4. compile contracts: `$ yarn compile`
5. create `.env` file: `$ touch .env`
6. fill in `ALCHEMY_ID` variable in the `.env` file (don't have an alchemy api key? see [here](https://www.alchemy.com/))
7. choose the polygon address you want to use for this tutorial (need a wallet? get metamask [here](https://metamask.io/)).
8. fill in `PK` variable in the `.env` file with hexadecimal private key for your address, `0x` prefixed (how to export metamask private key? see [here](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-export-an-account-s-private-key#:~:text=On%20the%20account%20page%2C%20click,click%20%E2%80%9CConfirm%E2%80%9D%20to%20proceed.))

Your `.env` file should now look something like this:

```
ALCHEMY_ID=aaaaaaaaaaaaaaaaaaaaaaaaaaaa
PK=0xffffffffffffffffffffffffffffffffffffffffffffffffffffffff
```

### Step 2: Create ArrakisV2 Vault Instance

First, fund your address with some MATIC (for gas costs) and at least 1 DAI, on polygon (matic) mainnet. (Acquiring or bridging tokens to matic mainnet is outside the scope of this tutorial)

Now we will run a script to initialize a private ArrakisV2 Vault on the DAI/WETH token pair:

```
$ yarn tutorial1-init --network polygon
```

(issues with gas pricing? you can manually override gas pricing with `MAX_FEE` and `MAX_PRIORITY_FEE` variables in the `.env` file.)

Congrats! You instantiated a private ArrakisV2 vault on matic mainnet.

Here's what got accomplished:

1. Create DAI/WETH ArrakisV2 vault and whitelist a few uniswap V3 fee tiers for use.
2. Set your address as the owner and manager of the vault as well as the `restrictedMint` so only your address may mint more LP shares.
3. Mint 1 LP share by depositing 1 DAI to finish initializing the private vault.

### Step 3: Fund vault

With the completion of Step 2 you control an ArrakisV2 vault that essentially works like your personal proxy wallet for holding DAI and WETH and deployoing the DAI/WETH holdings in and out of Uniswap V3. To fund the vault, you can simply transfer DAI and WETH to your ArrakisV2 token contract.

NOTE: (Your wallet may throw a warning here, which makes sense since **you should never send tokens directly to an ERC20 token contract unless you know exactly what and why you are doing this** but in this particular case it's entirely safe. You'll be able to retreive all tokens back from the vault by calling `burn()` and burning the Arrakis LP token you hold in your wallet).

So, copy the vault address output in Step 2 and on matic mainnet transfer WETH and DAI from any wallet to the vault address. Try to make it as close to 50/50 in dollar value if you can! (e.g. put in 5 DAI and $5 worth of WETH)

### Step 4: Deposit liquidity

To finally deposit your liquidity into Uniswap V3 LP positions run this command:

```
$ yarn tutorial1-setPosition --network polygon
```

Congrats! You just placed two LP positions on two different fee tiers with your ArrakisV2 vault. You can easily rebalance these into new configurations of Uniswap V3 LP at any time you like!
