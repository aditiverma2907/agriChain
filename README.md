# AgriChain Smart Contracts

## Overview
This folder contains Solidity smart contracts for the AgriChain supply chain management system.

## Deployment Instructions

### Option 1: Using Remix IDE (Recommended for Beginners)
1. Go to [Remix IDE](https://remix.ethereum.org/)
2. Create a new file and copy `AgriChainSupplyChain.sol` content
3. Compile the contract (Solidity version 0.8.x)
4. Deploy to a testnet:
   - Connect MetaMask to Sepolia testnet
   - Get test ETH from [Sepolia faucet](https://sepoliafaucet.com/)
   - Deploy the contract
   - Copy the deployed contract address

### Option 2: Using Hardhat
```bash
npm install --save-dev hardhat @nomicfoundation/hardhat-toolbox
npx hardhat init
# Copy contract to contracts folder
npx hardhat compile
npx hardhat run scripts/deploy.js --network sepolia
```

### Option 3: Using Foundry
```bash
forge init
# Copy contract to src folder
forge build
forge create --rpc-url $SEPOLIA_RPC_URL --private-key $PRIVATE_KEY src/AgriChainSupplyChain.sol:AgriChainSupplyChain
```

## After Deployment
1. Copy the deployed contract address
2. Update `AGRICHAIN_CONTRACT_ADDRESS` in `src/lib/blockchain.ts`
3. Update `BLOCKCHAIN_NETWORK` if not using Sepolia

## Contract Features

### registerProduct
Registers a new product on the blockchain with initial farmer details.

**Parameters:**
- `productId`: Unique product identifier
- `name`: Product name
- `category`: Product category
- `origin`: Origin location
- `farmerName`: Name of the farmer
- `initialPrice`: Initial price in wei (1 ETH = 10^18 wei)

### updateSupplyChain
Updates the supply chain when product moves to a new stage.

**Parameters:**
- `productId`: Product identifier
- `stage`: Stage (1=Wholesaler, 2=Retailer, 3=Consumer)
- `price`: Updated price in wei
- `location`: Current location

### getProduct
Retrieves product details from the blockchain.

### getSupplyChainEntry
Gets a specific supply chain entry by index.

## Testing Networks

### Sepolia Testnet
- Network Name: Sepolia
- RPC URL: https://sepolia.infura.io/v3/YOUR-PROJECT-ID
- Chain ID: 11155111
- Currency Symbol: ETH
- Block Explorer: https://sepolia.etherscan.io

### Mumbai Testnet (Polygon)
- Network Name: Mumbai
- RPC URL: https://rpc-mumbai.maticvigil.com
- Chain ID: 80001
- Currency Symbol: MATIC
- Block Explorer: https://mumbai.polygonscan.com

## Getting Test Tokens
- Sepolia ETH: https://sepoliafaucet.com/
- Mumbai MATIC: https://faucet.polygon.technology/

## Contract Verification
After deployment, verify your contract on Etherscan:
```bash
npx hardhat verify --network sepolia DEPLOYED_CONTRACT_ADDRESS
```

## Security Notes
- Never commit private keys to version control
- Use environment variables for sensitive data
- Test thoroughly on testnet before mainnet deployment
- Consider adding access control (e.g., OpenZeppelin's Ownable)
