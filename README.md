# Smart Cache Script

## Setup Instructions

### 1. Create New Project Folder

Create a new folder and open it in your Cursor or VSCode IDE.

### 2. Initialize Smart Cache Project

**Important Note**: All commands including cd commands must be run in WSL (Windows Subsystem for Linux) only. If you're on Windows, make sure to use WSL terminal for all operations.

Open the WSL terminal and run:
```bash
cargo stylus new smartcache
```

Then navigate into the project directory:
```bash
cd smartcache
```

### 3. Install Dependencies and Add Cache Functionality

**Important Note**: All cargo commands must be run in WSL (Windows Subsystem for Linux) only. If you're on Windows, make sure to use WSL terminal for all cargo operations.

Install the stylus cache SDK:
```bash
cargo add stylus-cache-sdk
```

Then add the following code in your `lib.rs` file:

```rust
use stylus_cache_sdk::{is_contract_cacheable};

#[public]
impl Counter {
    pub fn is_cacheable(&self) -> bool {
        is_contract_cacheable()
    }
}
```

**Important**: Just like this example, in the `impl` block of your contract, you must include the `is_cacheable` function. Make sure that the function must be exactly like this.

### 4. Make Your Contract Unique

Change the name of any function in your contract to make it unique. For example, if you are working on the counter challenge, in the `impl Counter` block you will have all the defined functions. Change the function name like this:

- If the function name is `set_number`, change it to `set_number_meet`
- Simply append your name so that the contract can be unique for everyone

### 5. Deploy Your Contract

Run the following command in WSL only (if you are on Windows):

```bash
cargo stylus deploy --endpoint='https://sepolia-rollup.arbitrum.io/rpc' --private-key="<YOUR_PRIVATE_KEY>" --no-verify
```

**Troubleshooting**: If you get any issue related to `wasm32-unknown-unknown`, run the command:
```bash
rustup target add wasm32-unknown-unknown
```

Then run the `cargo stylus deploy` command again.

**Important**: If you see output like this:
```
deployed code at address: <add>
deployment tx hash: <tx_hash>
wasm already activated!
```

It means the transaction hash is not unique and must be unique to activate the program. In this case, you need to modify the function name again (change any function name to something unique) and try to deploy the contract again.

**Expected Output**: When successful, you should see output like this:
```
deployed code at address: <contract_address>
deployment tx hash: <some_hash>
contract activated and ready onchain with tx hash: 0x737795c1545039fe0477cbd40869318662e6c26c029453c9e687c4781fa54b71
```

### 6. Initialize Smart Cache

**Important Note**: From step 6 onwards, make sure to run all commands in a new terminal using PowerShell or bash (not WSL).

In that same challenge's code in your IDE, open a new terminal and run:

```bash
npm unlink -g smart-cache-cli
```

If you have installed smart-cache previously, then run:
```bash
npm install -g smart-cache-cli
```

Then run:
```bash
smart-cache init
```

This will create a new `smartcache.toml` file.

### 7. Configure Smart Cache

In the `smart-cache.toml` file, add:
- The contract address which you just deployed on Arbitrum Sepolia
- The deployed address of the private key which you used to deploy the contract on Arbitrum Sepolia

### 8. Add Contract to Cache

Run the command:
```bash
smart-cache add
```

This command will be running in your terminal and the contract will be cached to optimize gas usage.
