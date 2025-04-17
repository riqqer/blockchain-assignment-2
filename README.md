# Blockchain Assignment 2

This is a simple blockchain implementation written in Rust.  
The project was created as part of a university assignment and is intended for educational purposes. It demonstrates the foundational concepts of how blockchains operate without relying on external libraries.

## What This Project Does

This implementation includes:

- A `Block` struct with timestamp, data, previous hash, and current hash
- A `Blockchain` struct to manage the chain of blocks
- Basic transaction logic (if implemented)
- Hash-based linking between blocks
- Chain validation

## Getting Started

### 1. Install Rust

If you don’t have Rust installed, download and install it from the official website:

```
https://rustup.rs
```

This will install both the Rust compiler (`rustc`) and Cargo (Rust’s package manager and build tool).

### 2. Clone the Repository

Open your terminal and run:

```bash
git clone https://github.com/riqqer/blockchain-assignment-2.git
cd blockchain-assignment-2
```

### 3. Build the Project

Use Cargo to build the project:

```bash
cargo build
```

This will compile the project and check for any errors.

### 4. Run the Example

You can run the basic example with:

```bash
cargo run --example basic
```

You should see output in the terminal showing blocks being created and added to the chain.  
This file (`examples/basic.rs`) demonstrates how the blockchain works in practice.

## Project Structure

```
blockchain-assignment-2/
├── Cargo.toml         # Rust project configuration file
├── src/
│   ├── lib.rs         # Main blockchain logic
│   └── main.rs        # Entry point (can be used for testing or left empty)
├── examples/
│   └── basic.rs       # A working example that uses the blockchain
└── .gitignore         # Git ignore rules
```

## Key Files Explained

- `lib.rs`: Contains all the core logic. Defines how blocks and the blockchain are structured and linked.
- `basic.rs`: Demonstrates creating a blockchain, adding blocks, and printing them.
- `Cargo.toml`: Manages project dependencies and metadata.
