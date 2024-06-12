# Nexus-ZKVM-Tutorial---NODE

# Nexus ZKVM Tutorial

This tutorial guides you through setting up and running Nexus ZKVM on a VPS.

## Recommended VPS Specifications

- **CPU**: 2 Cores
- **RAM**: 4 GB

## Step-by-Step Guide

### Step 1: Install Required Packages

First, update your system and install the necessary packages:

```sh
sudo apt update -y && sudo apt upgrade -y && sudo apt install cmake -y && sudo apt install build-essential -y
```

Next, install Rust:
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Wait for the installation to complete and follow the on-screen instructions.

Step 2: Set Up Cargo
Set up the Cargo environment and install additional components:
```sh
. "$HOME/.cargo/env" && rustup target add riscv32i-unknown-none-elf
```

Install the Nexus tools using Cargo:
```sh
cargo install --git https://github.com/nexus-xyz/nexus-zkvm nexus-tools --tag 'v1.0.0'
```

Create a new Nexus project and navigate to the source directory:
```sh
cargo nexus new nexus-project && cd nexus-project && cd src
```

Step 3: Create a Sample Program
Remove the existing main.rs file and create a new one with the following content:
```sh
rm -rf main.rs && cat <<EOT >> main.rs
#![no_std]
#![no_main]

fn fib(n: u32) -> u32 {
    match n {
        0 => 0,
        1 => 1,
        _ => fib(n - 1) + fib(n - 2),
    }
}

#[nexus_rt::main]
fn main() {
    let n = 7;
    let result = fib(n);
    assert_eq!(result, 13);
}
EOT
```

Step 4: Run the Program
To run your program, use the following command:
```sh
cargo nexus run
```

Step 5: Generate a Proof
Generate a proof for your program with this command:
```sh
cargo nexus prove
```

Step 6: Verify Your Proof
Verify the generated proof using:
```sh
cargo nexus verify
```

Step 7: Save Your Proof
Save the proof locally on your phone or PC. For detailed instructions, you can refer to the video provided.
