```markdown
# LuckyScriptions

**LuckyScriptions** is a versatile JavaScript tool for interacting with the [LuckyCoin](https://luckycoin.org/) blockchain. It provides functionalities to manage wallets, mint inscriptions, deploy and transfer tokens, and run a local server to extract data from transactions. Additionally, it supports delegate minting, allowing users to associate inscriptions with delegate transaction IDs.

## Table of Contents

- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
  - [Commands](#commands)
  - [Minting Inscriptions](#minting-inscriptions)
  - [Delegate Minting](#delegate-minting)
  - [Wallet Management](#wallet-management)
  - [Deploying and Managing Tokens](#deploying-and-managing-tokens)
  - [Running the Server](#running-the-server)
- [Examples](#examples)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- **Wallet Management**: Create, sync, check balance, send, and split LKY funds.
- **Minting Inscriptions**: Mint regular and delegate inscriptions on the LuckyCoin blockchain.
- **Token Deployment**: Deploy and manage custom tokens (e.g., LKY-20).
- **Transaction Broadcasting**: Broadcast transactions with retry mechanisms and handle pending transactions.
- **Local Server**: Run a server to extract and serve data from transactions.
- **Delegate Minting**: Associate inscriptions with delegate transaction IDs for enhanced functionality.

## Prerequisites

- **Node.js**: Ensure you have Node.js (v12 or higher) installed. [Download Node.js](https://nodejs.org/)
- **LuckyCoin Node**: Access to a LuckyCoin node with RPC enabled.
- **Git**: For cloning the repository. [Download Git](https://git-scm.com/)

## Installation

1. **Clone the Repository**

   ```bash
   git clone https://github.com/yourusername/luckyscriptions.git
   cd luckyscriptions
   ```

2. **Install Dependencies**

   Navigate to the `luckyscriptions` directory and install the required npm packages:

   ```bash
   cd luckyscriptions
   npm install
   ```

## Configuration

Create a `.env` file in the root directory to configure environment variables. Here's a sample configuration:

```env
# .env

# RPC Configuration
NODE_RPC_URL=http://localhost:22555
NODE_RPC_USER=your_rpc_username
NODE_RPC_PASS=your_rpc_password

# Network Configuration
TESTNET=false

# Fee Configuration
FEE_PER_KB=100000000

# Wallet Configuration
WALLET=.wallet.json

# Server Configuration
SERVER_PORT=3000
```

### Environment Variables Explained

- `NODE_RPC_URL`: URL of your LuckyCoin node's RPC interface.
- `NODE_RPC_USER`: RPC username.
- `NODE_RPC_PASS`: RPC password.
- `TESTNET`: Set to `true` to use the testnet.
- `FEE_PER_KB`: Transaction fee per kilobyte in satoshis.
- `WALLET`: Path to the wallet file.
- `SERVER_PORT`: Port number for the local server.

## Usage

Navigate to the `luckyscriptions` directory and execute commands using Node.js:

```bash
node luckyscriptions.js <command> [subcommand] [options]
```

### Commands

- `mint`: Mint a new inscription.
- `mint-luckymap`: Mint multiple inscriptions as a luckymap.
- `deploy-lky`: Deploy LuckyCoin specific functionalities.
- `deploy-lky20`: Deploy LKY-20 tokens.
- `mint-lky20`: Mint LKY-20 tokens.
- `wallet`: Manage wallet operations.
- `server`: Run the local server for transaction extraction.

### Minting Inscriptions

#### Regular Mint

```bash
node luckyscriptions.js mint <address> <contentTypeOrFilename> <hexData>
```

- **address**: Destination address for the inscription.
- **contentTypeOrFilename**: MIME type or filename of the content to mint.
- **hexData**: Hexadecimal data to inscribe.

#### Delegate Mint

```bash
node luckyscriptions.js mint <address> "" "" <delegateTxId>
```

- **address**: Destination address for the delegate inscription.
- **delegateTxId**: Transaction ID to delegate the inscription to.

### Delegate Minting

Delegate minting allows associating an inscription with a specific transaction ID, enabling more advanced functionalities.

#### Example

```bash
node luckyscriptions.js mint LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz "" "" 36b918da97b02ca500526e0c0a4ac8b2ca396ee6c9a2677ba829c5469c585eadi0
```

- **address**: `LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz`
- **contentTypeOrFilename**: `""` (empty for delegate mint)
- **hexData**: `""` (empty for delegate mint)
- **delegateTxId**: `36b918da97b02ca500526e0c0a4ac8b2ca396ee6c9a2677ba829c5469c585eadi0`

### Wallet Management

Manage your wallet with the following subcommands:

- **Create a New Wallet**

  ```bash
  node luckyscriptions.js wallet new
  ```

- **Sync Wallet with the Blockchain**

  ```bash
  node luckyscriptions.js wallet sync
  ```

- **Check Wallet Balance**

  ```bash
  node luckyscriptions.js wallet balance
  ```

- **Send Funds**

  ```bash
  node luckyscriptions.js wallet send <recipientAddress> <amount>
  ```

- **Split Wallet Funds**

  ```bash
  node luckyscriptions.js wallet split <numberOfSplits>
  ```

### Deploying and Managing Tokens

#### Deploy LKY-20 Token

```bash
node luckyscriptions.js deploy-lky20 <address> <ticker> <maxSupply> <limit>
```

- **address**: Address deploying the token.
- **ticker**: Token ticker symbol.
- **maxSupply**: Maximum supply of the token.
- **limit**: Transaction limit.

#### Mint LKY-20 Token

```bash
node luckyscriptions.js mint-lky20 <address> <ticker> <amount> [repeat]
```

- **address**: Recipient address.
- **ticker**: Token ticker symbol.
- **amount**: Amount to mint.
- **repeat**: (Optional) Number of times to repeat the minting.

### Running the Server

Start a local server to extract and serve data from transactions:

```bash
node luckyscriptions.js server
```

The server listens on the port specified in the `.env` file (`SERVER_PORT`). Access transaction data via:

```
http://localhost:<SERVER_PORT>/tx/<txid>
```

#### Example

```
http://localhost:3000/tx/15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62e
```

## Examples

### 1. Creating a New Wallet

```bash
node luckyscriptions.js wallet new
```

**Output:**

```
address LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz
```

### 2. Minting a Regular Inscription

```bash
node luckyscriptions.js mint LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz ./path/to/file.txt
```

### 3. Minting a Delegate Inscription

```bash
node luckyscriptions.js mint LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz "" "" 36b918da97b02ca500526e0c0a4ac8b2ca396ee6c9a2677ba829c5469c585eadi0
```

### 4. Deploying a LKY-20 Token

```bash
node luckyscriptions.js deploy-lky20 LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz mytoken 1000000 100
```

### 5. Minting LKY-20 Tokens

```bash
node luckyscriptions.js mint-lky20 LCHxodkzaKCLjmnG4LP8uH6NKynmntmCNz mytoken 100 5
```

This will mint 100 `mytoken` tokens five times.

### 6. Running the Server

```bash
node luckyscriptions.js server
```

Access a transaction:

```
http://localhost:3000/tx/<txid>
```

## Troubleshooting

- **Wallet Already Exists**

  If you encounter an error stating that the wallet already exists when running `wallet new`, ensure you back up and delete the existing wallet file (`.wallet.json`) if you intend to create a new one.

- **Insufficient Funds**

  Ensure your wallet has enough DOGE balance to perform minting or sending operations. Use `wallet balance` to check your balance.

- **RPC Connection Issues**

  Verify that your LuckyCoin node is running and the RPC credentials (`NODE_RPC_USER`, `NODE_RPC_PASS`, `NODE_RPC_URL`) in the `.env` file are correct.

- **Invalid Delegate Transaction ID**

  Ensure that the delegate transaction ID ends with `i0` as required by the script.

## Contributing

Contributions are welcome! Please fork the repository and submit a pull request for any enhancements or bug fixes.

1. Fork the repository.
2. Create a new branch: `git checkout -b feature/YourFeature`.
3. Commit your changes: `git commit -m 'Add some feature'`.
4. Push to the branch: `git push origin feature/YourFeature`.
5. Open a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

---
```
