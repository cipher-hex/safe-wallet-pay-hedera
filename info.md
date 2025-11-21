# SafeWallet Pay - Project Information

## Short Description

SafeWallet Pay: Secure multi-chain P2P payments + zero-loss lottery. PYUSD, ENS, Web3Auth powered. 🚀

## Description

SafeWallet Pay is a comprehensive decentralized financial platform that revolutionizes how users interact with cryptocurrency payments and decentralized finance. Built with security, accessibility, and innovation at its core, the platform offers two main services that work seamlessly together.

### Core Services:

**1. Safe P2P Payments**
SafeWallet Pay provides a secure escrow-based payment system that eliminates the risks associated with traditional cryptocurrency transfers. When a user sends funds, they are held in a smart contract until the recipient actively claims them. This prevents accidental loss of funds due to incorrect addresses and provides dispute resolution capabilities. The system supports both wallet addresses and human-readable user IDs, making it accessible to both crypto-native users and newcomers.

**2. Zero-Loss Lottery**
Our innovative lottery system ensures participants never lose their principal investment. When users buy lottery tickets, their funds are pooled and used to generate interest through DeFi protocols. The interest earned becomes the prize pool, while all participants are guaranteed to get their original investment back regardless of whether they win. This creates a risk-free gambling experience that's both entertaining and educational for DeFi newcomers.

### Key Innovations:

- **Multi-Token Architecture**: Native support for both blockchain-native currencies (ETH, FLOW) and ERC-20 tokens, with special integration for PayPal's PYUSD stablecoin
- **Cross-Chain Compatibility**: Seamless operation across multiple blockchains with a unified user interface
- **Social Authentication**: Web3Auth integration enables social login alongside traditional wallet connections
- **ENS Integration**: Support for Ethereum Name Service across multiple chains for human-readable addresses
- **Progressive Web App**: Mobile-responsive design that works across all devices

### Target Audience:

- Crypto enthusiasts looking for safer payment methods
- DeFi newcomers wanting risk-free exposure to decentralized finance
- Businesses needing secure, programmable payment solutions
- Users who want to bridge traditional finance (PayPal) with DeFi

## How It's Made

SafeWallet Pay represents a sophisticated integration of multiple cutting-edge technologies, each chosen for specific benefits and capabilities.

### Core Technology Stack:

**Frontend Architecture:**
- **React 18+ with TypeScript**: Provides type safety and modern component architecture
- **Tailwind CSS**: Enables rapid, responsive UI development with a consistent design system
- **Wagmi & Viem**: Industry-standard libraries for Ethereum interactions, providing type-safe contract interactions
- **React Router**: Client-side routing for seamless single-page application experience

**Smart Contract Development:**
- **Solidity**: Core smart contract language for business logic implementation
- **Hardhat**: Development environment providing testing, debugging, and deployment capabilities
- **OpenZeppelin**: Battle-tested contract libraries for security and standardization
- **Custom Escrow Logic**: Proprietary smart contract architecture for secure P2P payments

### Partner Technology Integration:

**PYUSD by PayPal:**
PayPal's PYUSD integration was a strategic choice that bridges traditional finance with DeFi. PYUSD provides:
- Regulatory compliance and institutional backing
- Price stability crucial for payments
- Familiar brand recognition for mainstream adoption
- Seamless integration with existing PayPal ecosystems

The integration required custom decimal handling (6 decimals vs. standard 18) and specialized formatting logic to ensure accurate transaction displays and calculations.

**ENS (Ethereum Name Service):**
ENS integration extends beyond Ethereum to provide cross-chain name resolution:
- Custom resolver implementation for multi-chain support
- Client-side caching for improved performance
- Fallback mechanisms for networks without native ENS support
- User-friendly address abstraction

**Blockchain Integration:**

**Sepolia Testnet:**
- Primary development and testing network
- Full ERC-20 token support including PYUSD
- Comprehensive smart contract deployment
- ENS integration testing

**Flow Testnet:**
- Alternative blockchain implementation
- Custom token deployment (Mock COIN)
- Cross-chain compatibility validation
- Different architecture testing (account-based vs. UTXO)

### Technical Innovations & Hacks:

**1. Multi-Decimal Token Handler:**
Created a sophisticated decimal handling system that automatically detects and formats different token types:
```typescript
// Custom decimal formatting for different tokens
if (isNative) {
  formattedAmount = formatEther(amount); // 18 decimals
} else {
  // Dynamic decimal detection for ERC-20 tokens
  const decimals = getTokenDecimals(tokenAddress);
  formattedAmount = formatUnits(amount, decimals);
}
```

**2. Universal Transaction ID System:**
Implemented a hybrid system that extracts contract-generated transaction IDs from event logs rather than using blockchain transaction hashes:
```typescript
// Extract actual transaction ID from contract events
const decoded = decodeEventLog({
  abi: SafePayContractABI,
  data: log.data,
  topics: log.topics,
});
return decoded.args.transactionId; // Contract-generated ID
```

**3. Cross-Chain ENS Resolution:**
Built a resolver that works across multiple blockchains by implementing ENS-like functionality on non-Ethereum chains:
```typescript
// Multi-chain ENS resolution
const resolveAddress = async (ensName: string, chainId: number) => {
  if (chainId === mainnet.id) {
    return await ensResolve(ensName);
  } else {
    return await customResolver(ensName, chainId);
  }
};
```

**4. Smart Contract Event Parsing:**
Developed a robust event parsing system that handles multiple contract versions and network differences:
```typescript
// Enhanced transaction details with token information
const [transactionId, sender, recipient, amount, timestamp, status, note, tokenAddress, isNative] = contractResult;
```

### Architecture Decisions:

**Wagmi Configuration:**
Chose Wagmi over web3.js for its TypeScript-first approach and React hooks integration, significantly reducing boilerplate code and improving developer experience.

**Component Architecture:**
Implemented a modular component system with clear separation of concerns:
- Shared components for cross-platform functionality
- Feature-specific components for specialized logic
- Custom hooks for business logic abstraction

**State Management:**
Used React's built-in state management with custom hooks rather than Redux to reduce complexity and improve performance for this use case.

## Technical Details

### Prerequisites

- Node.js 20+
- npm or yarn
- Web3Auth Client ID
- MetaMask or compatible Web3 wallet

### Installation & Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd react-web3-auth-payment
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Environment Configuration**
   Create a `.env` file in the root directory:
   ```bash
   VITE_WEB3AUTH_CLIENT_ID=your_web3auth_client_id_here
   ```

4. **Start the development server**
   ```bash
   npm run dev
   # or
   yarn dev
   ```

5. **Access the application**
   Open your browser and navigate to `http://localhost:3000`

### Project File Structure

```
react-web3-auth-payment/
├── src/
│   ├── components/           # Reusable UI components
│   │   ├── shared/          # Cross-platform components
│   │   │   └── MainHeader.tsx
│   │   ├── safe-pay/        # P2P payment components
│   │   │   ├── SendTransfer.tsx
│   │   │   ├── ClaimTransfer.tsx
│   │   │   ├── TokenSelector.tsx
│   │   │   └── TransactionHistory.tsx
│   │   └── zero-risk-pot/   # Lottery components
│   │       ├── TabNavigation.tsx
│   │       └── ...
│   ├── pages/               # Main application pages
│   │   ├── HomePage.tsx     # Landing page
│   │   ├── payment/         # P2P payment pages
│   │   │   └── safe-transfer.tsx
│   │   └── zero-risk-pot-pages/ # Lottery pages
│   │       ├── pot-home.jsx
│   │       ├── BuyTickets.jsx
│   │       ├── ClaimFunds.jsx
│   │       └── AdminPanel.jsx
│   ├── utils/               # Utility functions
│   │   ├── safe-payblockchain-call.ts  # Blockchain interactions
│   │   ├── contract-address/           # Contract addresses
│   │   │   ├── safePay-address.json
│   │   │   ├── safePay-tokens.json
│   │   │   └── lottery-address.json
│   │   └── errorHandler.ts
│   ├── hooks/               # Custom React hooks
│   │   ├── useTokenConfig.ts
│   │   ├── useTokenApproval.ts
│   │   └── useTransactionType.ts
│   ├── artifacts/           # Smart contract ABIs
│   │   └── safePay-address.json
│   └── styles/              # CSS and styling files
├── backend/                 # Smart contract development
│   ├── contracts/           # Solidity smart contracts
│   │   ├── SafePay.sol      # Main P2P payment contract
│   │   ├── ZeroLossLottery.sol
│   │   └── Coin.sol         # Test token contract
│   ├── scripts/             # Deployment scripts
│   │   └── safepay-enhanced-deploy.js
│   └── hardhat.config.js    # Hardhat configuration
└── package.json
```

### Smart Contract Addresses

#### Sepolia Testnet
- **Network ID**: 11155111
- **SafePay Enhanced Contract**: `0xdEE61D7ECc13404c26DE0813C921A32b424b1d70`
- **PYUSD Token**: `0xCaC524BcA292aaade2DF8A05cC58F0a65B1B3bB9`
- **Features**: Native ETH + ERC-20 tokens (PYUSD)
- **Block Explorer**: [Sepolia Etherscan](https://sepolia.etherscan.io/)

#### Flow Testnet
- **Network ID**: 545
- **SafePay Basic Contract**: `0x5e6c03E14002aF759680cd86ad4534D4b8FA0648`
- **Mock COIN Token**: `0xd2Cab77F7A111f77b2113Fb3CA5824db535D63e3`
- **ZeroLoss Lottery**: `0x[lottery-address]`
- **Features**: Native FLOW + Mock COIN tokens
- **Block Explorer**: [Flow Testnet Explorer](https://testnet.flowscan.org/)

#### Citea Testnet
- **Network ID**: 5115
- **SafePay Enhanced Contract**: `0x5e6c03E14002aF759680cd86ad4534D4b8FA0648`
- **Native Currency**: CBTC (Citea BTC) - 18 decimals
- **Features**: Native CBTC + ERC-20 token support
- **Block Explorer**: [Citea Testnet Explorer](https://explorer.testnet.citrea.xyz/)

### Supported Tokens

#### Sepolia
```json
{
  "chainId": "11155111",
  "nativeCurrency": {
    "symbol": "ETH",
    "decimals": 18,
    "name": "Ethereum"
  },
  "supportedTokens": [
    {
      "address": "0xCaC524BcA292aaade2DF8A05cC58F0a65B1B3bB9",
      "symbol": "PYUSD",
      "name": "PayPal USD",
      "decimals": 6
    }
  ]
}
```

#### Flow Testnet
```json
{
  "chainId": "545",
  "nativeCurrency": {
    "symbol": "FLOW",
    "decimals": 18,
    "name": "Flow"
  },
  "supportedTokens": [
    {
      "address": "0xd2Cab77F7A111f77b2113Fb3CA5824db535D63e3",
      "symbol": "COIN",
      "name": "Mock Coin",
      "decimals": 18
    }
  ]
}
```

#### Citea Testnet
```json
{
  "chainId": "5115",
  "nativeCurrency": {
    "symbol": "CBTC",
    "decimals": 18,
    "name": "Citea BTC"
  },
  "supportedTokens": []
}
```

### Development Commands

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Run tests
npm run test

# Deploy contracts (backend)
cd backend
npx hardhat run scripts/safepay-enhanced-deploy.js --network sepolia
npx hardhat run scripts/safepay-enhanced-deploy.js --network flow

# Verify contracts
npx hardhat verify --network sepolia <contract-address>
```

### Environment Variables

Required environment variables for full functionality:

```bash
# Web3Auth Configuration
VITE_WEB3AUTH_CLIENT_ID=your_web3auth_client_id

# Optional: Custom RPC endpoints
VITE_SEPOLIA_RPC_URL=your_sepolia_rpc_url
VITE_FLOW_RPC_URL=your_flow_rpc_url

# Optional: Analytics
VITE_ANALYTICS_ID=your_analytics_id
```

### Network Configuration

The application automatically detects and configures supported networks:

```typescript
// Automatic network detection
const networks = chains.map(chain => ({
  id: chain.id,
  name: chain.name,
  symbol: chain.nativeCurrency?.symbol || 'ETH'
}));
```

This enables seamless multi-chain functionality without hardcoded network parameters.
