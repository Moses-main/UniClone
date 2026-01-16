# Decentralized Exchange (DEX) on Ethereum

A simple yet powerful decentralized exchange (DEX) built on Ethereum using Solidity and Foundry. This DEX allows users to swap between ETH and a custom ERC-20 token, provide liquidity, and earn trading fees.

## Features

- **Automated Market Maker (AMM)** - Uses a constant product formula (x * y = k) for price determination
- **Liquidity Pools** - Users can provide liquidity and earn trading fees
- **LP Tokens** - ERC-20 tokens representing liquidity provider shares
- **Token Swaps** - Seamless swapping between ETH and the native token
- **No Price Oracle** - Purely market-driven pricing based on pool reserves

## Smart Contracts

### 1. Token.sol
An ERC-20 token contract with a fixed supply of 1,000,000 tokens minted to the deployer.

### 2. Exchange.sol
The core DEX contract that handles:
- Adding/removing liquidity
- Swapping between ETH and tokens
- LP token minting/burning
- Price calculations

## Development

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation)
- [Node.js](https://nodejs.org/) (for development tooling)
- [Git](https://git-scm.com/)

### Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/dex-app.git
   cd dex-app
   ```

2. Install dependencies:
   ```bash
   forge install
   ```

3. Compile contracts:
   ```bash
   forge build
   ```

### Testing

Run the test suite:
```bash
forge test -vvv
```

### Deployment

1. Set up your environment variables in `.env`:
   ```
   PRIVATE_KEY=your_private_key
   RPC_URL=your_ethereum_node_url
   ETHERSCAN_API_KEY=your_etherscan_api_key
   ```

2. Deploy the Token contract:
   ```bash
   forge create --rpc-url $RPC_URL --private-key $PRIVATE_KEY src/Token.sol:Token
   ```

3. Deploy the Exchange contract (replace `TOKEN_ADDRESS` with the deployed Token address):
   ```bash
   forge create --rpc-url $RPC_URL --private-key $PRIVATE_KEY src/Exchange.sol:Exchange --constructor-args TOKEN_ADDRESS
   ```

## Usage

### Adding Liquidity
1. Approve the Exchange to spend your tokens:
   ```javascript
   await token.approve(exchange.address, amount);
   ```
2. Call `addLiquidity` with the token amount (ETH is sent as value):
   ```javascript
   await exchange.addLiquidity(tokenAmount, { value: ethAmount });
   ```

### Swapping Tokens
- **ETH to Token**: Send ETH to `ethToTokenSwap`
- **Token to ETH**: Call `tokenToEthSwap` with token amount

### Removing Liquidity
Call `removeLiquidity` with the amount of LP tokens to burn.

## Security

- Uses OpenZeppelin's battle-tested contracts
- Implements reentrancy guards
- Includes input validation and require statements
- Uses SafeMath for arithmetic operations

## License

MIT

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## Acknowledgements

- [OpenZeppelin](https://openzeppelin.com/)
- [Foundry](https://book.getfoundry.sh/)
- [Uniswap V1](https://github.com/Uniswap/v1-contracts) for inspiration

- **Forge**: Ethereum testing framework (like Truffle, Hardhat and DappTools).
- **Cast**: Swiss army knife for interacting with EVM smart contracts, sending transactions and getting chain data.
- **Anvil**: Local Ethereum node, akin to Ganache, Hardhat Network.
- **Chisel**: Fast, utilitarian, and verbose solidity REPL.

## Documentation

https://book.getfoundry.sh/

## Usage

### Build

```shell
$ forge build
```

### Test

```shell
$ forge test
```

### Format

```shell
$ forge fmt
```

### Gas Snapshots

```shell
$ forge snapshot
```

### Anvil

```shell
$ anvil
```

### Deploy

```shell
$ forge script script/Counter.s.sol:CounterScript --rpc-url <your_rpc_url> --private-key <your_private_key>
```

### Cast

```shell
$ cast <subcommand>
```

### Help

```shell
$ forge --help
$ anvil --help
$ cast --help
```
