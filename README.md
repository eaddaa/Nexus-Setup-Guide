# Nexus-Setup-Guide

# Rust installation

# Choose option 1
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

# After Rust is installed, run:
```
. "$HOME/.cargo/env"
rustup target add riscv32i-unknown-none-elf
```

# Installing Nexus tool

# This may take some time, don't worry if you encounter errors.
```
cargo install --git https://github.com/nexus-xyz/nexus-zkvm cargo-nexus --tag 'v0.2.3'
```
# Create a Nexus project
```
cargo nexus new nexus-project
```

# Navigate to the project directory
```
cd nexus-project
```

# Edit the `main.rs` file
```
nano ./src/main.rs
```
# Delete the existing code and insert the following block:
```
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
```

# Run the contract
```
cargo nexus run
cargo nexus run -v
```

# Wait for the proofing process to finish
```
cargo nexus prove
```

# Complete the verification process
```
cargo nexus verify
```

# Save the nexus-proof file in this directory for later.

Network CLI
```
screen -S nexus
curl https://cli.nexus.xyz/ | sh
```
