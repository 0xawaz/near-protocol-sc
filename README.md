# dAGI Hackathon

## Learning smart contract with rust

https://medium.com/@bloqarl/getting-started-with-rust-549f24097bed

install binaries

# Install Rust: https://www.rust-lang.org/tools/install
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# Contracts will be compiled to wasm, so we need to add the wasm target
rustup target add wasm32-unknown-unknown

# Install NEAR CLI-RS to deploy and interact with the contract
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/near/near-cli-rs/releases/latest/download/near-cli-rs-installer.sh | sh

# Install cargo near to help building the contract
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/near/cargo-near/releases/latest/download/cargo-near-installer.sh | sh

cargo near new hello

# test sc
cargo test

# Replace <your-account-id.testnet> with a custom name
near account create-account sponsor-by-faucet-service hello-w.testnet autogenerate-new-keypair save-to-keychain network-config testnet create

# deploy sc
cargo near build

near contract deploy hello-w.testnet use-file ./target/wasm32-unknown-unknown/release/hello.wasm without-init-call network-config testnet sign-with-keychain send

https://testnet.nearblocks.io/txns/Btpd2BwqVYC9q566LDiy4StamaWzcztZ1ccxfeq9RSEL

# interacting with sc

near contract call-function as-read-only hello-w.testnet get_greeting json-args {} network-config testnet now

near contract call-function as-transaction hello-w.testnet set_greeting json-args '{"greeting": "Hola"}' prepaid-gas '100.0 Tgas' attached-deposit '0 NEAR' sign-as hello-w.testnet network-config testnet sign-with-keychain send

--- Logs ---------------------------
Logs [hello-w.testnet]:
  Saving greeting: Hola

