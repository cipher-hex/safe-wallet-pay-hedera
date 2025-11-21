# SafeWallet Pay

A secure Hedera-based P2P payment platform with **escrow**, **refunds (including wrong-address sends)**, and **bulk transaction management**.  
Built on **Hedera testnet (296)** with **Web3Auth** onboarding and a modern React UI.

---

## 📋 Problem Statement

Traditional crypto payments have critical issues, especially for everyday users and businesses in :

- **No protection for wrong-address transfers**
  - If you paste or type the wrong wallet address, the funds are gone forever.
  - There is **no native “undo” or refund option** once a transaction is broadcast.
- **No escrow / claim process**
  - Funds are sent directly to the recipient with no “claim step”, making disputes and trust hard to manage.
- **No sender-controlled refunds**
  - Even if the recipient never uses or even sees the funds, the sender has no way to pull them back.
- **Inefficient bulk payouts**
  - Paying salaries, vendors, community members or grant recipients needs many on-chain transactions, increasing cost and complexity.
- **Complex onboarding & UX**
  - Seed phrases, network configuration, and raw hex addresses are intimidating for new users.
- **Infrastructure gaps in**
  - Many users need low-fee, fast, programmable payments for micro‑transactions, remittances, and bulk payouts, but don’t get that from traditional rails.

---

## 💡 Our Solution

SafeWallet Pay adds a **smart-contract escrow layer** and rich UI on top of Hedera:

1. **Escrow-first payments**
   - Funds are locked in the `SafePay` contract instead of going directly to the recipient.
2. **Claim-based receiving**
   - Recipients explicitly **claim** funds (HBAR or ERC‑20) with a transaction ID.
3. **Refunds for unclaimed & misdirected funds**
   - If a payment is never claimed, the **sender can refund** and recover the funds.
   - This gives a safety net for **wrong-address transfers**, as long as the funds remain unclaimed in escrow.
4. **Bulk Transaction Manager**
   - Send many payments in a single transaction to save cost and simplify operations.
5. **Human-readable names**
   - Resolve `.eth` via ENS (on Sepolia) and `.hbar` via HNS on Hedera to avoid copying raw addresses.
6. **Smooth onboarding**
   - Web3Auth enables social logins alongside traditional wallets.

Result: a safer, more forgiving payment flow that still feels like normal crypto.

---

## ✨ Core Features

### 1. 🔐 Safe P2P Escrow Payments

- Funds always go **into escrow first**, not directly to the recipient.
- Recipients **claim** funds using a transaction ID.
- Senders can **refund unclaimed payments**, including:
  - Mistaken transfers to a wrong recipient address that never claims.
- Send by:
  - **Wallet address**, or
  - **Registered user ID**.
- Supported assets:
  - Native **HBAR**.
  - ERC‑20 style tokens like **HUSD** on Hedera testnet.

### 2. 👥 Bulk Transaction Manager

- Create **bulk payouts** in one transaction:
  - Configure individual amounts per recipient.
  - Suitable for payroll, bounties, vendor payments, and airdrops.
- Bulk transaction history to audit and review previous payouts.

### 3. 🧾 Refund & History Layer

- View all:
  - **Pending** (escrowed, not yet claimed),
  - **Claimed**, and
  - **Refunded** transactions.
- Trigger refunds for unclaimed escrow payments via UI.
- Clear, human-readable statuses for every transaction.

### 4. 🌐 Name Resolution (ENS & HNS)

- **ENS Resolver (Sepolia)**
  - Resolve `.eth` names to EVM addresses.
- **HNS Resolver (Hedera)**
  - Resolve `.hbar` names to:
    - Hedera **account ID**, and
    - Associated **EVM address**
  - Uses:
    - `https://api.hashgraph.name/api/v1/domains/resolve/{domain}` (HNS REST API),
    - Hedera Mirror Node for account → EVM address.
- Each resolver only appears on the **network where it makes sense**.

### 5. 🔑 Authentication & UX

- **Web3Auth** for:
  - Social logins (Google, Twitter, etc.),
  - Key management abstraction.
- Support for **MetaMask** and other Web3 wallets.
- Mobile-first, responsive UI with Tailwind CSS and Framer Motion.

---

## 🌍 How It Empowers Hedera the World

- **Ultra‑low fees & micro‑transactions**
  - Hedera’s low, predictable fees make it practical to send very small payments.
- **Fast finality**
  - 3–5 second finality enables real‑time retail payments and remittances.
- **Refundable escrow in trust‑poor environments**
  - Users and SMEs can send money with the confidence that unclaimed or misdirected escrow payments can be refunded.
- **Efficient bulk payouts**
  - SMEs, cooperatives, DAOs, and NGOs can pay many people at once — salaries, rewards, grants, and more.
- **Inclusive onboarding**
  - Web3Auth and name services (ENS/HNS) reduce the cognitive load of using crypto.

---

## 🛠️ Architecture & Tech Stack

### Frontend

- **React 18 + TypeScript**
- **Vite** for dev/build.
- **Tailwind CSS** for styling.
- **Wagmi v2 & Viem** for RPC and contract calls.
- **Framer Motion** for animations.
- **React Router** for client-side routing.

### Smart Contracts (Backend)

- **Solidity 0.8.x** with **Hardhat**.
- `SafePay.sol`
  - Escrow-based payments.
  - Claim + refund logic (HBAR and ERC‑20).
  - User ID registry & lookup.
- `BulkTransactionManager.sol`
  - Bulk native & ERC‑20 transfers.
  - Transaction history storage.
- Uses **OpenZeppelin**:
  - `ReentrancyGuard`, `Ownable`, `SafeERC20`, `IERC20`.

### Authentication & Network

- **Web3Auth** for social & wallet-based login.
- Primary target network:
  - **Hedera Testnet (Chain ID: 296)**.

---

## 📁 Project Structure (High Level)

```txt
Hedera-Payment-interface/
├── src/
│   ├── components/
│   │   ├── safe-pay/                 # SafePay escrow UI (send, claim, history, resolvers)
│   │   ├── bulk-transaction/         # Bulk transfer UI
│   │   └── shared/                   # Shared header/layout components
│   ├── pages/                        # Route-level pages
│   ├── hooks/                        # Custom React hooks
│   ├── utils/                        # Contract calls, validation, config
│   ├── artifacts/                    # Frontend ABIs (SafePay, BulkTransactionManager)
│   ├── context/                      # Wallet & Web3Auth context providers
│   └── main.tsx                      # App entry & provider wiring
│
├── backend/
│   ├── contracts/                    # Solidity contracts
│   ├── scripts/                      # Hardhat deployment scripts
│   ├── artifacts/                    # Compiled ABIs & build info
│   ├── contract-address/             # Deployed address JSON
│   └── hardhat.config.js             # Hardhat & network config
│
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js **v18+**
- `pnpm` or `npm`
- A Web3 wallet (e.g. MetaMask)
- Web3Auth client ID

### 1. Clone & Install

```bash
git clone <your-repo-url>
cd Hedera-Payment-interface

# Frontend
pnpm install        # or: npm install

# Backend
cd backend
pnpm install        # or: npm install
cd ..
```

### 2. Environment Variables

Create `.env` in the **project root**:

```bash
VITE_WEB3AUTH_CLIENT_ID=your_web3auth_client_id
```

Create `.env` in the **backend** folder for deployments:

```bash
PRIVATE_KEY=your_deployer_private_key   # EVM-compatible deployer on Hedera
```

### 3. Run the Frontend

```bash
pnpm dev       # or: npm run dev
```

App will run at `http://localhost:5173`.

### 4. Build for Production

```bash
pnpm build     # or: npm run build
```

Production assets will be generated in `dist/`.

---

## 📝 Smart Contract Deployment (Hedera Testnet)

### 1. Deploy SafePay

```bash
cd backend
npx hardhat run scripts/safepay-deploy.js --network hedera-testnet
```

### 2. Deploy BulkTransactionManager

```bash
cd backend
npx hardhat run scripts/deploy-bulk-transaction.js --network hedera-testnet
```

### 3. Update Frontend Addresses

After deployment, update:

- `src/utils/contract-address/safePay-address.json`
- `src/utils/contract-address/bulk-transaction-addresses.json`

### 4. Copy ABIs to Frontend

```bash
# SafePay ABI
cp backend/artifacts/contracts/SafePay.sol/SafePay.json \
   src/artifacts/SafePay.json

# BulkTransactionManager ABI
cp backend/artifacts/contracts/BulkTransactionManager.sol/BulkTransactionManager.json \
   src/artifacts/BulkTransactionManager.json
```

---

## 📍 Current Hedera Testnet Deployment

### SafePay (Escrow Contract)

- **Address**: `0x472d036dCCd902CD874c6467E6eD0aF3d7843BF0`
- **Chain ID**: `296`
- **Tokens**:
  - Native: **HBAR** (18 decimals)
  - ERC‑20: **HUSD** (`0x0000000000000000000000000000000000068cda`, 6 decimals)

### BulkTransactionManager

- **Address**: `0xeFca10882Cd20060FD51E9c8418822b52f8C51f4`
- **Chain ID**: `296`

These addresses are also configured in:

- `src/utils/contract-address/safePay-address.json`
- `src/utils/contract-address/bulk-transaction-addresses.json`
- `src/utils/contract-address/safePay-tokens.json`

---

## 🔒 Security & Design Considerations

- **Escrow & Refund Logic**
  - Payments are **claim-based**; funds remain in escrow until claimed.
  - Senders can **refund unclaimed funds**, reducing damage from wrong-address mistakes.
- **Reentrancy & Safe Transfers**
  - `ReentrancyGuard` on state-changing functions.
  - `SafeERC20` for token transfers.
- **Access Control**
  - `Ownable` for admin operations and controlled upgrades.
- **Input & Amount Validation**
  - Frontend and contract-level checks for amounts, arrays, and addresses.
- **Hedera Benefits**
  - Low fees, fast finality, and carbon‑negative infrastructure.

---

## 🗺️ Future Roadmap

- **Universal Payment Solution (Cross‑Chain, Any Token)**
  - Allow users to **create and manage payment requests** with:
    - Preferred blockchain (e.g. Hedera, EVM L2s, etc.),
    - Preferred token (HBAR, stablecoins, or ERC‑20s),
    - Total amount to receive.
  - Generate a **payment link** that can be shared with the payer.
  - The receiver connects their wallet; if their funds are on **another chain or in another token**, the platform:
    - Requests **allowance** on the payer’s chosen token/chain,
    - Automatically orchestrates **swap + bridge** steps behind the scenes,
    - Delivers funds to the receiver in their **preferred token on their preferred blockchain**.
  - Goal: make crypto payments feel like a single, universal payment network, regardless of where liquidity lives.
- **Unified Balance System**
  - Show a **single aggregated balance view** across multiple chains and tokens.
  - Normalize balances into a common unit (e.g. USD equivalent) while still showing per‑asset details.
  - Power better UX for the universal payment solution and future cross‑chain features.
- Better **UX messaging** around wrong-address mistakes and refund windows.
- Additional **tokens** and **stablecoins** on Hedera.
- **Fiat on‑ramp/off‑ramp** integration.
- Bulk payout analytics & CSV export.

SafeWallet Pay brings **safer, refundable and scalable bulk crypto payments** to Hedera — tailored for real users and businesses across the World.
