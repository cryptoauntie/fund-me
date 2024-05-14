# Fund Me

Fund Me a decentralized crowd sourcing application. It allows the owner to recieve and withdraw funds sent from others. Built on Ethereum blockchain technology, it ensures transparency and reliability in fundraising activities.


- [Fund Me](#fund-me)
  - [Built With](#built-with)
- [Getting Started](#getting-started)
  - [Requirements](#requirements)
  - [Quickstart](#quickstart)
- [Usage](#usage)
  - [Deploy](#deploy)
  - [Testing](#testing)
    - [Test Coverage](#test-coverage)
- [Deployment to a testnet or mainnet](#deployment-to-a-testnet-or-mainnet)
  - [Scripts](#scripts)
    - [Fund the contract](#fund-the-contract)
    - [Withdraw funds](#withdraw-funds)
  - [Estimate gas cost](#estimate-gas-cost)
- [Formatting](#formatting)
- [Disclaimer](#disclaimer)
- [Acknowledgements](#acknowledgements)
- [Thank you!](#thank-you)


## Built With

- Foundry - The Ethereum smart contract framework used.
- Git: Version control system.
- Chainlink - Decentralized oracle network for secure and reliable data feeds.
    

# Getting Started

## Requirements

Ensure you have the following prerequisites installed on your system:

- [git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
  - You'll know you did it right if you can run `git --version` and you see a response like `git version x.x.x`
- [foundry](https://getfoundry.sh/)
  - You'll know you did it right if you can run `forge --version` and you see a response like `forge 0.2.0 (2e3c197 2024-05-06T15:58:31.193893000Z)`


## Quickstart

Clone this repository and build the project locally:

```
git clone https://github.com/dmariet/fund-me
cd foundry-fund-me-f23
forge build
```


# Usage

## Deploy

Deploy the Fund Me contract to your desired network:

```
forge script script/DeployFundMe.s.sol
```

## Testing

Ensure proper functioning by testing the project functions:


```
forge test
```

or 

For more advanced testing or to test a single function, use the following commands:

```
// Only run test functions matching the specified regex pattern.

forge test --match-test testFunctionName
```

or

```
forge test --fork-url $SEPOLIA_RPC_URL
```

### Test Coverage

Generate test coverage reports:
```
forge coverage
```


# Deployment to a testnet or mainnet

1. Setup environment variables in a `.env` file:

You'll want to set your `SEPOLIA_RPC_URL` and `PRIVATE_KEY` as environment variables. You can add them to a `.env` file, similar to what you see in `.env.example`.

- `PRIVATE_KEY`: The private key of your account (like from [metamask](https://metamask.io/)). **NOTE:** FOR DEVELOPMENT, PLEASE USE A KEY THAT DOESN'T HAVE ANY REAL FUNDS ASSOCIATED WITH IT. IT IS BEST TO ENCRYPT IT INSTEAD OF STORING IN `.env` (keep reading).
  - You can [learn how to export it here](https://metamask.zendesk.com/hc/en-us/articles/360015289632-How-to-Export-an-Account-Private-Key).
- `SEPOLIA_RPC_URL`: This is url of the sepolia testnet node you're working with. You can get setup with one for free from [Alchemy](https://alchemy.com/?r=890d65401067a3ce)

Optionally, add your `ETHERSCAN_API_KEY` if you want to verify your contract on [Etherscan](https://etherscan.io/).

```
PRIVATE_KEY=your_private_key
SEPOLIA_RPC_URL=your_sepolia_rpc_url
ETHERSCAN_API_KEY=your_etherscan_api_key (optional)
```


FOR DEVELOPMENT, you'll want to encrypt your `PRIVATE_KEY` instead of storing it in plain text in the `.env` file -> a keystore in Foundry.

- You will create an `ACCOUNT_NAME` and a password for your encrypted `PRIVATE_KEY`.

```
cast wallet import your-account-name --interactive
Enter private key:
Enter password:
`your-account-name` keystore was saved successfully. Address: address-corresponding-to-private-key
```

```
forge script <script> --rpc-url <rpc_url> --account <account_name> --sender <address> --broadcast
```

- Add your `ACCOUNT_NAME` and `ADDRESS` to your `.env` file.
```
ACCOUNT_NAME=xxxxyour-account-name
ADDRESS=0x000your-address
SEPOLIA_RPC_URL=http://0.0.5555
ETHERSCAN_API_KEY=your_etherscan_api_key (optional)
```

1. Get testnet ETH from Chainlink Faucet:

Head over to [faucets.chain.link](https://faucets.chain.link/) and get some testnet ETH. You should see the testnet ETH show up in your metamask. If not, make sure you have the testnet ETH added

3. Deploy the contract:

```
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY
```

or if the `PRIVATE_KEY` is encrypted

```
forge script script/DeployFundMe.s.sol --rpc-url $SEPOLIA_RPC_URL --account $ACCOUNT_NAME --sender $ADDRESS --broadcast --verify --etherscan-api-key $ETHERSCAN_API_KEY -vvvv
```

## Scripts

After deploying to a testnet or local net, you can execute the various contract scripts: 

### Fund the contract

Using cast deployed locally example: 

```
cast send <FUNDME_CONTRACT_ADDRESS> "fund()" --value 0.1ether --private-key <PRIVATE_KEY>
```

or
```
forge script script/Interactions.s.sol --rpc-url sepolia  --private-key $PRIVATE_KEY  --broadcast
```

or if the `PRIVATE_KEY` is encrypted

```
cast send <FUNDME_CONTRACT_ADDRESS> "fund()" --value 0.1ether --account ACCOUNT_NAME --sender ADDRESS
```

or
```
forge script script/Interactions.s.sol --rpc-url sepolia --account $ACCOUNT_NAME --sender $ADDRESS --broadcast
```

### Withdraw funds

```
cast send <FUNDME_CONTRACT_ADDRESS> "withdraw()"  --private-key <PRIVATE_KEY>
```

or if the `PRIVATE_KEY` is encrypted
```
cast send <FUNDME_CONTRACT_ADDRESS> "withdraw()"  --account ACCOUNT_NAME --sender ADDRESS
```

## Estimate gas cost

You can estimate how much gas things cost by running:

```
forge snapshot
```

And you'll see an output file called `.gas-snapshot`


# Formatting


To ensure formatting consistency:
```
forge fmt
```

# Disclaimer 

None of the code has been audited or undergone a security review, use at your own risk.

# Acknowledgements

Special thanks to Patrick Collins for his invaluable teaching and guidance!


# Thank you!

If you find this helpful, consider following or supporting me!

[![Crypto Auntie Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/CryptoAuntieD)
[![Crypto Auntie YouTube](https://img.shields.io/badge/YouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.youtube.com/channel/UCDVVmzwg-0g5XluEzqrtHnA)