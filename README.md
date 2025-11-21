# SafeWallet Pay

A secure, escrow-based P2P payment platform built on Hedera Hashgraph. SafeWallet Pay solves the critical issues of irreversible crypto transactions and inefficient bulk payments, offering a safer way to send funds with built-in refund capabilities and bulk transfer management.

## 🚨 Problem Statement

The current state of peer-to-peer cryptocurrency payments is fraught with risks and inefficiencies:

1.  **Irreversibility of Transactions**: Once crypto is sent, it is gone forever. If you send funds to the **wrong address** or a **scam wallet**, there is absolutely **no option to refund** or recover your assets.
2.  **Lack of Transaction Safety**: Senders have no assurance that the recipient is the intended party before the funds are irrevocably transferred.
3.  **Inefficient Bulk Payments**: Paying multiple people (e.g., payroll, dividends) requires executing individual transactions for each recipient, resulting in high gas fees and wasted time.
4.  **Complex Onboarding**: Managing private keys and seed phrases prevents mainstream adoption, especially in emerging markets like Africa.

## 💡 Our Solution

SafeWallet Pay introduces a "Safety Layer" to crypto transactions:

- **Escrow-First Architecture**: Funds are not sent directly to the recipient's wallet. Instead, they are held in a secure smart contract.
- **Refund Guarantee**: If a transaction is sent to the wrong person or remains unclaimed, the **sender can fully refund the amount** back to their wallet.
- **Claim-Based Receipt**: Recipients must explicitly "claim" the funds, ensuring active participation and verification.
- **Bulk Transaction Manager**: A unified interface to send native HBAR or ERC-20 tokens to up to 50 recipients in a single on-chain transaction.
- **Identity Resolution**: Integrated **Hedera Name Service (HNS)** and **ENS** resolvers allow users to send funds to human-readable names (e.g., `alice.hbar`) instead of error-prone hex addresses.

## ✨ Key Features

### 🛡️ Secure P2P Payments

- **Escrow Protection**: Funds are locked in the `SafePay` contract until claimed.
- **Refund Mechanism**: Total control remains with the sender until the moment of claim.
- **Flexible Sending**: Send to wallet addresses or registered **SafeWallet User IDs**.
- **Multi-Token Support**: Full support for Native HBAR and ERC-20 tokens (e.g., HUSD).

### 📦 Bulk Transaction Manager

- **Batch Processing**: Execute up to 50 transfers in one transaction.
- **Address Book**: Manage saved recipients with custom nicknames and relations.
- **Smart Validation**: Automatic validation of recipient addresses before submission.
- **History Tracking**: detailed logs of all bulk operations.

### 🌍 Empowering Hedera Africa

SafeWallet Pay leverages Hedera's **$0.0001 fixed fees** and **3-second finality** to provide a viable financial tool for the African market:

- **Remittance Safety**: Diaspora can send funds home without fear of losing money to typos.
- **Micro-payments**: Low fees make even $1 transactions economically viable.
- **Mobile-First**: Optimized for smartphones, the primary access point for many users.

### 🔍 Name Service Integration

- **HNS Resolver**: Auto-resolves `.hbar` domains on Hedera Testnet.
- **ENS Resolver**: Auto-resolves `.eth` domains on Sepolia.
- **Cross-Chain UX**: Seamlessly switches resolvers based on the connected network.

## 🛠️ Technical Architecture

### Frontend

- **Framework**: React 18 + Vite
- **Language**: TypeScript
- **Styling**: Tailwind CSS + Framer Motion
- **Web3**: Wagmi, Viem, Web3Auth (Social Logins)

### Backend & Smart Contracts

- **Network**: Hedera Testnet (Chain ID: 296) & Sepolia
- **Framework**: Hardhat
- **Contracts**:
  - `SafePay.sol`: Handles escrow logic, claims, and refunds.
  - `BulkTransactionManager.sol`: Batches transfers for efficiency.
- **Security**: OpenZeppelin `ReentrancyGuard`, `Ownable`, and `SafeERC20`.

## 🚀 Getting Started

### Prerequisites

- Node.js (v18+)
- pnpm or npm
- MetaMask or Web3Auth-compatible wallet

### Installation

1.  **Clone & Install**

    ```bash
    git clone <repo-url>
    cd Hedera-Payment-interface
    pnpm install
    cd backend && pnpm install && cd ..
    ```

2.  **Environment Setup**
    Create a `.env` file in the root:

    ```env
    VITE_WEB3AUTH_CLIENT_ID=your_client_id
    ```

    Create a `.env` file in `backend/`:

    ```env
    PRIVATE_KEY=your_deployer_private_key
    ```

3.  **Run Development Server**
    ```bash
    pnpm dev
    ```

## 📝 Smart Contracts

### Deployment

```bash
cd backend
# Deploy SafePay
npx hardhat run scripts/safepay-deploy.js --network hedera-testnet

# Deploy Bulk Manager
npx hardhat run scripts/deploy-bulk-transaction.js --network hedera-testnet
```

### Deployed Addresses (Hedera Testnet)

| Contract        | Address                                      | Description                |
| --------------- | -------------------------------------------- | -------------------------- |
| **SafePay**     | `0x472d036dCCd902CD874c6467E6eD0aF3d7843BF0` | Main escrow & refund logic |
| **BulkManager** | `0xeFca10882Cd20060FD51E9c8418822b52f8C51f4` | Batch transfer processor   |

**Supported Tokens:**

- **HBAR** (Native, 18 decimals)
- **HUSD** (`0x00...68cda`, 6 decimals)

## 📂 Project Structure

```
├── src/
│   ├── components/
│   │   ├── safe-pay/        # Escrow, HNS Resolver, Refund UI
│   │   ├── bulk-transaction/# Bulk transfer forms & history
│   │   └── shared/          # Headers, Modals
│   ├── hooks/               # Wagmi & Logic hooks
│   ├── utils/
│   │   ├── hns-resolver.ts  # HNS API Logic
│   │   └── safe-payblockchain-call.ts
│   └── pages/               # Routes
├── backend/
│   ├── contracts/           # Solidity Sources
│   └── scripts/             # Deployment Scripts
└── README.md
```
