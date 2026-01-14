# Manteia Protocol Documentation Outline

This outline mirrors the structure of `docs.reflect.money`, adapted for Manteia's Revenue-Based Financing (RBF) & ZK-RWA stack.

## I. Introduction

### Welcome to Manteia
**"Capital Built on Math, Not Pitch Decks."**
*   **Concept**: Manteia is a permissionless, zero-knowledge protocol that converts recurring revenue (SaaS, Creators) into liquid capital (FlowNFTs) without revealing sensitive business data.
*   **The Paradigm Shift**: Moving from "Trust-based Financing" (Banks, VCs) to "Truth-based Financing" (ZK Proofs, On-chain History).
*   **The Asset**: "FlowNFT" – A tradable, yield-bearing asset backed by real-world revenue streams.

### Why Manteia?
*   **For Founders**:
    *   **Privacy-First**: Your customer list and bank logs never leave your device unencrypted.
    *   **Speed**: Solvency is verified programmatically in milliseconds.
    *   **Control**: Non-dilutive capital. Keep your equity.
*   **For Lenders**:
    *   **Real Yield**: Returns come from actual business revenue, not token inflation.
    *   **Transparency**: Protocol solvency is verifiable on-chain 24/7.
*   **Comparison**: Manteia vs. Stripe Capital vs. Traditional Factoring.

### FAQs
*   *Is my data safe?* (Explain ZK Architecture briefly).
*   *What happens if a business defaults?* (Explain Repayment Enforcement / Slashing).
*   *Where does the yield come from?* (Real-world revenue splits, not Ponzinomics).

---

## II. Protocol Mechanics (The "Strategies")

*Analogous to "Interest-Generating Dollars" in Reflect Docs.*

### FlowNFTs (The Asset Class)
*   **Definition**: A standard ERC-721 token representing a claim on a future revenue stream.
*   **Lifecycle**:
    1.  **Mint**: Founder connects data -> Generates Proof -> Mints NFT.
    2.  **Fund**: `LendingVault` purchases NFT -> Founder gets USDC.
    3.  **Repay**: Revenue flows to `0xSplits` -> Lenders get repaid + Yield.
    4.  **Burn**: Loan fully repaid -> NFT burned/archived.

### The Lending Vault (Liquidity)
*   **Mechanism**: A pooled liquidity contract (`LendingVault.sol`) that automatically allocates capital to verified FlowNFTs.
*   **Yield Source**:
    *   **Base Yield**: funds sitting in the pool (e.g., converted to USDY via Ondo).
    *   **RWA Yield**: High-APY returns from funded businesses (FlowNFTs).
*   **Auto-Allocation**: How the protocol matches liquidity to borrowers based on risk scores.

---

## III. Risk Management & Privacy

*Analogous to "Risk Management" in Reflect Docs.*

### The "Blind" Oracle (ZK Architecture)
*   **Core Concept**: The oracle sees *that* the data is valid, without seeing *what* the data is.
*   **`revenue_check.circom`**:
    *   How the ZK Circuit works.
    *   **Inputs**: API Secret, Revenue History (Private).
    *   **Outputs**: Average MRR, Risk Score, Integrity Hash (Public).
*   **Data Provenance**: Using TLSNotary / Reclaim Protocol (Future scope) to prove the data came from Stripe.github.

### On-Chain Security
*   **Solvency Verification**: The `Verifier.sol` contract ensuring only valid proofs allow minting.
*   **Smart Contract Audits**: (Placeholder for future audit reports).
*   **Emergency Pause**: Governance controls for halting protocol in black swan events.

### Default Risk
*   **Repayment Enforcement**: How `0xSplits` ensures revenue is diverted before it hits the founder's wallet.
*   **Collateralization**: Why revenue history acts as "reputational collateral".

---

## IV. Integration & SDKs

*Analogous to "API Reference" in Reflect Docs.*

### Founder SDK (Client-Side)
*   **Data Connectors**:
    *   `@manteia/stripe`: Connecting specific endpoints (`/balance/history`, `/charges`).
    *   `@manteia/shopify`: Connecting specific endpoints (`/orders`).
*   **Proof Generation**:
    *   Generating `proof.json` and `publicSignals.json` in the browser.
    *   Hardware requirements (WASM optimization).

### Lender SDK (Dashboard Integration)
*   **`useLenderStats`**: Hook for fetching Net Worth, APY, and Active Loans.
*   **Subgraphs**: querying the Manteia subgraph for historical loan performance.

---

## V. Protocol References

### Smart Contracts Addresses
*   **Mantle Sepolia / Mainnet**:
    *   `LendingVault`: `0x...`
    *   `ManteiaFactory`: `0x...`
    *   `Verifier`: `0x...`
    *   `MockUSDC`: `0x...` (Testnet only)

### Glossary
*   **MRR**: Monthly Recurring Revenue.
*   **FlowNFT**: The core financial instrument.
*   **ZK-SNARK**: The cryptographic proof method used.
