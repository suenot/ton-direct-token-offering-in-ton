# TON Direct Token Offering (DTO) in TON

**⚠️ WARNING: This code is under active development and is not recommended for use in production environments without thorough auditing and testing. ⚠️**

A smart contract for the TON blockchain that facilitates direct token offerings at a fixed price. This contract allows token issuers to sell their tokens directly to investors using native TON coins, operating on a "first come, first served" basis.

## Features

- Exchange TON for project tokens at a fixed rate
- Owner can withdraw accumulated TON
- Owner can withdraw remaining project tokens
- Owner can change the exchange rate
- Minimum transaction amount to prevent spam
- Security checks to ensure proper operation
- Simplified implementation using native TON instead of USDT

## How It Works

1. The contract owner deploys the contract with the following parameters:
   - Owner wallet address
   - Project token address
   - Exchange rate (how many project tokens per 1 TON)

2. The owner sends project tokens to the contract

3. Investors send TON to the contract and automatically receive project tokens at the configured rate

4. The owner can withdraw accumulated TON at any time

## Setup

1. Clone this repository
2. Install dependencies:
```bash
npm install
```
3. Create a `.env` file based on the `.env.example` template
4. Fill in your environment variables in the `.env` file

## Compilation and Deployment

To compile the contract:

```bash
npm run build
```

To compile TypeScript files:

```bash
npm run compile
```

To deploy the contract to the TON blockchain:

```bash
npm run deploy
```

## Contract Operations

### For Investors

Investors can participate in the token offering by sending TON to the contract address. The minimum amount is 0.1 TON.

### For Contract Owner

The contract owner can perform the following operations by sending a message with the appropriate operation code:

1. Change Rate (op code 1):
   - Allows changing the exchange rate for project tokens

2. Withdraw TON (op code 2):
   - Withdraws all accumulated TON to the owner's address

3. Withdraw Project Tokens (op code 3):
   - Withdraws specified amount of project tokens to the owner's address

### Get Methods

The contract provides the following get methods for querying its state:

- `get_mm_to_ton_rate()` - Returns the current exchange rate
- `get_owner_address()` - Returns the owner's address
- `get_mm_address()` - Returns the project token address
- `get_seqno()` - Returns the current sequence number

## Security Considerations

- Only the owner can withdraw accumulated TON or remaining project tokens
- Only the owner can change the exchange rate
- The contract enforces a minimum transaction amount (0.1 TON) to prevent gas drain attacks
- The contract ensures it always has enough TON to continue operations
- All sensitive operations are protected by sender address verification

## Environment Variables

Create a `.env` file with the following variables:

```
# Owner wallet address
OWNER_ADDRESS=EQ...

# Project token address
PROJECT_TOKEN_ADDRESS=EQ...

# Exchange rate: how many project tokens per 1 TON
PROJECT_TOKEN_TO_TON_RATE=100

# Wallet mnemonic for deploying the contract
MNEMONIC=your wallet seed phrase here

# Optional: TON API endpoint
TON_API_ENDPOINT=https://toncenter.com/api/v2/jsonRPC

# Optional: TON Center API key
TON_API_KEY=
```

## Technical Details

The contract is implemented in FunC version 0.4.0 and utilizes the TON blockchain's native features for efficient operation. It has been optimized for gas usage and security.

Key technical aspects:
- Uses native TON for transactions
- Compatible with TEP-74 standard tokens
- Minimal dependencies for increased security
- Gas-efficient implementation

## License

MIT
