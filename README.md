# 🌀 Solana Token Swap (Anchor Bootcamp Project)

This project implements a decentralized escrow-based token swap on Solana using the Anchor framework.

## 📦 Features

- Alice (maker) can offer a specific amount of Token A and request Token B in return.
- Tokens are securely stored in a vault (escrow).
- Bob (taker) accepts the offer by sending Token B and receives Token A.
- Vault closes after successful swap.
- Compatible with SPL Token v1 and Token-2022.

## 🛠️ Tech Stack

- ⚙️ Solana & Anchor framework
- 🧩 `anchor_spl::token_interface` for Token-2022 compatibility
- 🔁 `associated_token` for handling ATAs
- 🧪 Mocha + Chai for integration testing
- 🛡 PDA (Program Derived Addresses) for access control

## 🧪 Running Tests

Run integration tests with:

```bash
anchor test
```

## 🧬 Structure

```
programs/swap/
├── src/
│   ├── lib.rs              # Program entry
│   ├── constants.rs        # Constants used across modules
│   ├── error.rs            # Custom error definitions
│   ├── state/
│   │   └── offer.rs        # Offer account definition
│   └── instructions/
│       ├── make_offer.rs   # Logic for creating an offer
│       ├── take_offer.rs   # Logic for taking an offer
│       └── shared.rs       # Common utility functions
tests/
└── swap.ts                 # JS test suite using Anchor and SPL Token libs
```

## 📜 How It Works

1. Alice (maker) calls makeOffer, specifying:
- Amount of Token A to offer
- Amount of Token B she wants in return

2. Token A is transferred to a vault account (PDA).

3. Bob (taker) calls takeOffer:
- Sends Token B to Alice
- Receives Token A from the vault

4. Vault is closed after a successful swap.

## 🔐 Security Notes

- PDA vaults ensure only the program can move tokens.
- transfer_checked ensures correct decimals and mint match.
- Account constraints (e.g., has_one, seeds) prevent spoofing.
