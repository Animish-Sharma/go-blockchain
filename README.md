# Go Blockchain

A minimal blockchain implementation written in Go for learning and experimenting with blockchain fundamentals. This project showcases core components like blocks, transactions, wallets, and a command-line interface (CLI) for interaction.

---

## 🚀 Features

- Blockchain structure with persistent storage  
- Proof-of-Work (PoW) mining  
- UTXO-based transaction model  
- Merkle tree for transaction verification  
- Wallet and address generation using elliptic curve cryptography  
- Comprehensive CLI to interact with the blockchain  
- Optional peer-to-peer node server (experimental)

---

## 🧱 How the Blockchain Works

### Block Structure

Each block includes:
- Hash
- Previous block's hash
- Transactions
- Timestamp
- Nonce (for PoW)

```go
type Block struct {
    Timestamp     int64
    Transactions  []*Transaction
    PrevBlockHash []byte
    Hash          []byte
    Nonce         int
}
```

### Proof-of-Work

To add a block, miners must solve a PoW puzzle:

```go
func (pow *ProofOfWork) Run() (int, []byte) {
    var hashInt big.Int
    var hash [32]byte
    nonce := 0

    for nonce < maxNonce {
        data := pow.prepareData(nonce)
        hash = sha256.Sum256(data)
        hashInt.SetBytes(hash[:])

        if hashInt.Cmp(pow.target) == -1 {
            break
        } else {
            nonce++
        }
    }

    return nonce, hash[:]
}
```

---

## 💸 Transaction Model (UTXO)

Transactions are composed of inputs and outputs.

```go
type Transaction struct {
    ID   []byte
    Vin  []TXInput
    Vout []TXOutput
}
```

### Create a New Transaction

```go
func NewUTXOTransaction(from, to string, amount int, bc *Blockchain) *Transaction {
    // Find spendable outputs, create inputs and outputs
}
```

---

## 🔐 Wallets and Addresses

Wallets use ECDSA (Elliptic Curve Digital Signature Algorithm) for key generation.

```go
type Wallet struct {
    PrivateKey ecdsa.PrivateKey
    PublicKey  []byte
}
```

### Generate a New Wallet

```bash
./blockchain createwallet
```

### List Addresses

```bash
./blockchain listaddresses
```

---

## 🛠️ Installation

### Prerequisites

- Go 1.18 or higher

### Build

```bash
git clone https://github.com/yourusername/go-blockchain.git
cd go-blockchain
go build -o blockchain main.go
```

---

## 💻 CLI Usage

### Create a Blockchain

```bash
./blockchain createchain -address YOURADDRESS
```

### Get Balance

```bash
./blockchain getbalance -address YOURADDRESS
```

### Send Coins

```bash
./blockchain send -from FROM -to TO -amount 10
```

### Print the Blockchain

```bash
./blockchain printchain
```

---

## 🔁 UTXO Reindexing

Rebuilds the UTXO set from scratch:

```bash
./blockchain reindexutxo
```

---

## 🌐 Networking (Experimental)

Start a node with a miner address:

```bash
./blockchain startnode -miner MINERADDRESS
```

---

## 📁 Project Structure

```
go-blockchain/
├── main.go                  # Entry point
├── block.go                 # Block structure and hashing
├── blockchain.go            # Blockchain management
├── blockchain_iterator.go   # Iterator to traverse the blockchain
├── transaction.go           # Transaction structure and validation
├── transaction_input.go     # Inputs for transactions
├── transaction_output.go    # Outputs for transactions
├── merkle_tree.go           # Merkle Tree logic
├── proofofwork.go           # Proof-of-Work implementation
├── utxo_set.go              # UTXO set and persistence
├── wallet.go                # Wallet and address generation
├── wallets.go               # Wallet management
├── base58.go                # Base58 encoding for addresses
├── utils.go                 # Utility functions
├── server.go                # Network server (optional)
├── cli.go                   # CLI dispatcher
├── cli_*.go                 # CLI commands (send, balance, etc.)
```

---

## 📦 Dependencies

Built with standard Go packages:
- `crypto/elliptic`, `crypto/sha256`
- `encoding/gob`, `encoding/hex`
- `math/big`, `fmt`, `os`, `log`

---

## 📚 Educational Purpose

This project is intended for educational purposes to understand the core principles of blockchain development. Not suitable for production use.

---

## Thank You
~ Animish Sharma