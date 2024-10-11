# Solana PDAs Example

This Solana program demonstrates the use of **Program Derived Addresses (PDAs)** in Anchor. It provides functionality to create a bank account, deposit funds, and withdraw funds securely, using Anchor's framework for Solana.

## Features
- Create a bank account tied to a user's wallet.
- Deposit funds into the bank account.
- Withdraw funds from the bank account, with checks on ownership and rent exemption.

## Program Overview

The program consists of three core functions:

1. **create**: Initializes a new bank account associated with the user's wallet, assigning a name, an initial balance of 0, and the user as the owner.
2. **deposit**: Transfers funds from the user's wallet into the bank account, updating the balance.
3. **withdraw**: Allows the user to withdraw funds from the bank, with ownership checks and checks for sufficient rent to avoid account deletion.

## PDA Mechanism
Program Derived Addresses (PDAs) are used to create secure, deterministic addresses based on program logic. In this program, the bank account is created using a PDA based on the user's public key and a constant seed.

### Example PDA Creation
```rust
#[account(
    init, 
    payer = user, 
    space = 5000, 
    seeds = [b"bankaccount", user.key().as_ref()], 
    bump
)]
pub bank: Account<'info, Bank>,
