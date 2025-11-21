# SafeWallet Pay

A secure P2P payment platform on Hedera Hashgraph with escrow protection, refund capabilities, and bulk transaction management. Built on Hedera testnet and powered by Web3Auth for seamless user onboarding.

## 📋 Problem Statement

Traditional peer-to-peer cryptocurrency payments face several critical challenges:

- **No Escrow Protection**: Funds are sent directly, leaving senders vulnerable to scams and recipients unable to verify funds before claiming
- **No Refund Mechanism**: Once a transaction is initiated, senders have no way to recover funds if recipients don't claim them
- **Inefficient Bulk Payments**: Sending payments to multiple recipients requires multiple transactions, leading to high gas fees and time consumption
- **Complex Wallet Setup**: Traditional crypto wallets require seed phrases and complex setup processes, creating barriers to entry
- **Insufficient Financial Infrastructure in Africa**: Many African regions lack robust payment systems that support both micro-transactions and bulk payments efficiently

## 💡 Our Solution

SafeWallet Pay provides a comprehensive decentralized payment solution that addresses these challenges through:

1. **Escrow-Based Secure Payments**: Funds are held in smart contracts until recipients explicitly claim them, ensuring both sender and recipient protection
2. **Refund System**: Senders can refund unclaimed transactions, giving them control over their funds
3. **Bulk Transaction Manager**: Send payments to multiple recipients in a single transaction, reducing costs and improving efficiency
4. **Hedera Hashgraph Integration**: Leveraging Hedera's fast, low-cost, and energy-efficient network for optimal performance
5. **Web3Auth Integration**: Social login support (Google, Facebook, etc.) and traditional wallet connections for easy onboarding

## ✨ Features

### 🔐 Secure P2P Payments

- **Escrow Protection**: Funds held securely in smart contracts until claimed
- **Wallet Address or User ID**: Send payments to wallet addresses or registered user IDs
- **Native & ERC-20 Support**: Support for native HBAR and ERC-20 tokens (HUSD)
- **Refund Capability**: Senders can refund unclaimed transactions anytime

### 👥 Bulk Transaction Manager

- **Multiple Recipients**: Send payments to up to 50 recipients in a single transaction
- **Recipient Management**: Add, edit, and delete recipients from your address book
- **Contact Details**: Store recipient names, relations, wallet addresses, and user IDs
- **Transaction History**: Track all bulk transfers with detailed history
- **Cost Efficient**: Single transaction for multiple payments reduces gas fees

### 🔑 Authentication & Security

- **Web3Auth Integration**: Social logins (Google, Facebook, Twitter, etc.)
- **Traditional Wallets**: MetaMask, WalletConnect, and other Web3 wallets
- **Reentrancy Protection**: OpenZeppelin security standards
- **Ownable Contracts**: Access control for contract administration

## 🌍 Empowering Hedera Africa

SafeWallet Pay leverages Hedera Hashgraph's unique advantages to empower financial transactions across Africa:

### Low Transaction Costs

- **Ultra-Low Fees**: Hedera's fee structure (typically $0.0001 USD) makes micro-transactions economically viable
- **Accessible Payments**: Enables affordable remittances and peer-to-peer transfers for users with limited resources

### Fast Finality

- **3-5 Second Finality**: Transactions are confirmed within seconds, enabling real-time payment scenarios
- **High Throughput**: Hedera can handle thousands of transactions per second, supporting large-scale adoption

### Energy Efficiency

- **Sustainable Technology**: Hedera uses a hashgraph consensus mechanism that is significantly more energy-efficient than proof-of-work blockchains
- **Carbon-Negative**: Hedera network is carbon-negative, supporting sustainable financial infrastructure

### Financial Inclusion

- **Easy Onboarding**: Web3Auth integration removes barriers to entry, allowing users without technical knowledge to participate
- **Mobile-First Design**: Responsive interface optimized for mobile devices, accessible to users with smartphones
- **Local Currency Support**: Support for stablecoins and tokens that can represent local currencies

### Remittance & Bulk Payments

- **Efficient Remittances**: Fast, low-cost cross-border payments for African diaspora sending money home
- **Business Payments**: Bulk transaction feature enables businesses to pay employees, vendors, and customers efficiently
- **SME Support**: Small and medium enterprises can manage multiple payments cost-effectively

## 🛠️ Tech Stack

### Frontend

- **React 18**: Modern UI library with hooks and functional components
- **TypeScript**: Type-safe development for better code quality
- **Tailwind CSS**: Utility-first CSS framework for responsive design
- **Vite**: Fast build tool and development server
- **Wagmi & Viem**: React hooks and utilities for Ethereum-compatible chains
- **Framer Motion**: Smooth animations and transitions
- **React Router**: Client-side routing

### Backend & Smart Contracts

- **Solidity 0.8.20**: Smart contract programming language
- **Hardhat**: Development environment, testing, and deployment framework
- **OpenZeppelin**: Battle-tested security libraries (Ownable, ReentrancyGuard, SafeERC20)

### Authentication

- **Web3Auth**: Social login and wallet connection infrastructure

### Blockchain Network

- **Hedera Testnet** (Chain ID: 296) - Optimized for HBAR transactions with ultra-low fees

## 📁 Project Structure

```
Hedera-Payment-interface/
├── src/                          # Frontend source code
│   ├── components/              # React components
│   │   ├── bulk-transaction/   # Bulk payment components
│   │   │   ├── AddRecipient.tsx
│   │   │   ├── BulkTransferForm.tsx
│   │   │   ├── RecipientsList.tsx
│   │   │   ├── TransactionHistory.tsx
│   │   │   └── BulkTransactionStats.tsx
│   │   ├── safe-pay/           # Safe payment components
│   │   │   ├── SendTransaction.tsx
│   │   │   ├── ClaimTransaction.tsx
│   │   │   ├── TransactionHistory.tsx
│   │   │   ├── TokenSelector.tsx
│   │   │   ├── RegisterUserid.tsx
│   │   │   └── EnsResolver.tsx
│   │   └── shared/             # Shared components
│   │       └── MainHeader.tsx
│   ├── pages/                  # Page components
│   │   ├── HomePage.tsx
│   │   ├── App.tsx
│   │   └── payment/
│   │       └── safe-transfer.tsx
│   ├── hooks/                  # Custom React hooks
│   │   ├── useBulkTransaction.ts
│   │   ├── useTokenConfig.ts
│   │   ├── useTransactionType.ts
│   │   └── useTokenApproval.ts
│   ├── utils/                  # Utility functions
│   │   ├── safe-payblockchain-call.ts  # SafePay contract interactions
│   │   ├── bulk-transaction/   # Bulk transaction utilities
│   │   │   ├── contract-calls.ts
│   │   │   └── validation.ts
│   │   ├── contract-address/   # Contract addresses per network
│   │   │   ├── safePay-address.json
│   │   │   ├── safePay-tokens.json
│   │   │   └── bulk-transaction-addresses.json
│   │   ├── formatAmount.ts     # Amount formatting utilities
│   │   └── errorHandler.ts
│   ├── artifacts/              # Contract ABIs
│   │   ├── SafePay.json
│   │   └── BulkTransactionManager.json
│   ├── context/                # React context providers
│   │   └── WalletContext.tsx
│   ├── types/                  # TypeScript type definitions
│   │   └── bulk-transaction.ts
│   └── main.tsx               # Application entry point
│
├── backend/                    # Smart contract development
│   ├── contracts/             # Solidity contracts
│   │   ├── SafePay.sol       # Main escrow payment contract
│   │   └── BulkTransactionManager.sol  # Bulk payment contract
│   ├── scripts/               # Deployment scripts
│   │   ├── safepay-deploy.js
│   │   └── deploy-bulk-transaction.js
│   ├── artifacts/             # Compiled contracts
│   ├── contract-address/      # Deployment addresses
│   │   └── safePay-address.json
│   └── hardhat.config.js      # Hardhat configuration
│
├── package.json               # Frontend dependencies
├── backend/package.json       # Backend dependencies
└── README.md                  # This file
```

## 🚀 Getting Started

### Prerequisites

- Node.js (v18 or higher)
- npm or pnpm package manager
- MetaMask or compatible Web3 wallet
- Web3Auth account (for social login features)

### Installation

1. **Clone the repository**

   ```bash
   git clone <your-repo-url>
   cd Hedera-Payment-interface
   ```

2. **Install frontend dependencies**

   ```bash
   npm install
   # or
   pnpm install
   ```

3. **Install backend dependencies**

   ```bash
   cd backend
   npm install
   # or
   pnpm install
   cd ..
   ```

4. **Configure environment variables**

   Create a `.env` file in the root directory:

   ```bash
   VITE_WEB3AUTH_CLIENT_ID=your_web3auth_client_id
   ```

   Create a `.env` file in the `backend` directory for contract deployment:

   ```bash
   PRIVATE_KEY=your_deployer_private_key
   ```

5. **Run the development server**

   ```bash
   npm run dev
   # or
   pnpm dev
   ```

   The application will be available at `http://localhost:5173`

### Building for Production

```bash
npm run build
# or
pnpm build
```

The production build will be in the `dist` directory.

## 📝 Smart Contract Deployment

### Deploy SafePay Contract

```bash
cd backend
npx hardhat run scripts/safepay-deploy.js --network hedera-testnet
```

### Deploy BulkTransactionManager Contract

```bash
cd backend
npx hardhat run scripts/deploy-bulk-transaction.js --network hedera-testnet
```

After deployment, update the contract addresses in:

- `src/utils/contract-address/safePay-address.json`
- `src/utils/contract-address/bulk-transaction-addresses.json`

### Copy Contract ABIs

After deployment, copy the compiled ABIs to the frontend:

```bash
# Copy SafePay ABI
cp backend/artifacts/contracts/SafePay.sol/SafePay.json src/artifacts/SafePay.json

# Copy BulkTransactionManager ABI
cp backend/artifacts/contracts/BulkTransactionManager.sol/BulkTransactionManager.json src/artifacts/BulkTransactionManager.json
```

## 📍 Contract Addresses

### Hedera Testnet

#### SafePay Contract

- **Address**: `0x472d036dCCd902CD874c6467E6eD0aF3d7843BF0`
- **Chain ID**: 296
- **Features**: Native HBAR & ERC-20 token support (HUSD)
- **Version**: Enhanced

#### BulkTransactionManager Contract

- **Address**: `0xeFca10882Cd20060FD51E9c8418822b52f8C51f4`
- **Chain ID**: 296
- **Deployed**: October 23, 2025

#### Supported Tokens

- **Native**: HBAR (18 decimals)
- **ERC-20**: HUSD (0x0000000000000000000000000000000000068cda, 6 decimals)

## 🔧 Configuration

### Network Configuration

Hedera Testnet is configured in:

- `backend/hardhat.config.js` - For contract deployment (Hedera testnet RPC: `https://testnet.hashio.io/api`)
- `src/utils/contract-address/safePay-address.json` - SafePay contract address for Hedera
- `src/utils/contract-address/bulk-transaction-addresses.json` - BulkTransactionManager address for Hedera
- `src/utils/contract-address/safePay-tokens.json` - Token configuration for Hedera (HBAR & HUSD)

## 📚 Key Features Explained

### Escrow System

- Funds are locked in the smart contract until claimed
- Senders can refund unclaimed transactions
- Recipients must explicitly claim funds using transaction ID

### Bulk Transactions

- Add recipients to your address book with contact details
- Select multiple recipients and amounts
- Execute all transfers in a single transaction
- Automatic refund of unused funds for native currency transfers

### Refund Mechanism

- Senders can refund native currency transactions if unclaimed
- Senders can refund ERC-20 token transactions if unclaimed
- Funds are returned to sender's wallet address

## 🔒 Security Considerations

- **Reentrancy Protection**: All state-changing functions use ReentrancyGuard
- **Access Control**: Ownable pattern for administrative functions
- **Safe Token Transfers**: SafeERC20 for ERC-20 token transfers
- **Input Validation**: Comprehensive validation of all user inputs
- **Gas Optimization**: Efficient contract design to minimize transaction costs
