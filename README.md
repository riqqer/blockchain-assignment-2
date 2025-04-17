# Solana Hello World Program

## Project Overview

This repository contains a minimal Solana program written in Rust that logs a message to the program log when invoked. It also includes a Rust client example for deploying and invoking this program on a local Solana validator.

## Requirements

- Rust (rustc and Cargo) v1.65 or higher (install via https://rustup.rs)
- Solana CLI v1.18.x (install instructions: https://docs.solana.com/cli/install-solana-cli-tools)
- `cargo-build-sbf` and `cargo-test-sbf` subcommands for building and testing SBF programs
- Unix-like shell (Linux/macOS/WSL) or Windows terminal

## Repository Structure

```text
blockchain-assignment-2/       # Rename as needed
├── Cargo.toml                 # Cargo manifest with dependencies
├── Cargo.lock                 # Locked dependency versions
├── src/lib.rs                 # Solana program entrypoint and logic
├── examples/client.rs         # Rust client for deploy & invocation
└── .gitignore
```

## Step 1: Clone the Repository

```bash
git clone https://github.com/riqqer/blockchain-assignment-2.git
cd blockchain-assignment-2
```

## Step 2: Build the SBF Program

Compile the Solana program into SBF format:

```bash
cargo build-sbf
```

Upon success, `target/deploy/` will contain:

- `hello_world.so` — the compiled program
- `hello_world-keypair.json` — the keypair file containing the program ID

## Step 3: Start the Local Validator

In a separate terminal, run:

```bash
solana-test-validator
```

This launches a local Solana cluster at `http://localhost:8899`.

## Step 4: Configure the Solana CLI

Point the CLI to your local validator:

```bash
solana config set --url http://localhost:8899
```

## Step 5: Retrieve Your Program ID

Print the public key from the generated keypair:

```bash
solana address -k target/deploy/hello_world-keypair.json
```

Copy this `Program ID` for later use.

## Step 6: Fund Your Wallet (Airdrop SOL)

Request some test SOL for transaction fees:

```bash
solana airdrop 2
```

Verify your balance:

```bash
solana balance
```

## Step 7: Deploy the Program

With the validator still running, execute:

```bash
solana program deploy target/deploy/hello_world.so
```

Take note of the returned `Program Id`.

## Step 8: Configure the Client Example

Open `examples/client.rs` and replace the placeholder with your deployed Program ID:

```diff
- let program_id = Pubkey::from_str("4Ujf5fX...FfMz").unwrap();
+ let program_id = Pubkey::from_str("YOUR_PROGRAM_ID").unwrap();
```

## Step 9: Run the Client

Build and run the client example:

```bash
cargo run --example client
```

This script will:

1. Generate a new keypair for paying transaction fees
2. Request an airdrop of SOL
3. Create and sign a transaction invoking your program
4. Send the transaction and print its signature

## Step 10: Verify Program Logs

In the validator terminal logs, you should see:

```
Program log: Hello, world!
```

This confirms that your program executed the `msg!` macro correctly.

## Step 11: Update the Program

To change the logged message:

1. Modify `src/lib.rs`:
  ```diff
  - msg!("Hello, world!");
  + msg!("Hello, Solana!");
  ```
2. Rebuild and redeploy:
   ```bash
   cargo build-sbf
   solana program deploy target/deploy/hello_world.so
   ```
3. Rerun the client to see the updated log message.

## Step 12: Close the Program

When you no longer need the program, reclaim its SOL balance:

```bash
solana program close YOUR_PROGRAM_ID --bypass-warning
```

**Warning:** This operation is irreversible. After closing, the Program ID cannot be reused.

---
