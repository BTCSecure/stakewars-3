## Deploying a smart contract
Would you like to contribute to other projects running a validator? Deploy a smart contract on the owner account of a staking pool.
This contract will allow users to split their rewards on multiple accounts.

## Steps
* Install cargo and Rust in case you don't have it. This command is for Linux or MacOS.
```
curl --proto '=https' --tlsv1.2 https://sh.rustup.rs -sSf | sh
source $HOME/.cargo/env
```

* Add the `wasm32-unknown-unknown` toolchain:
```
rustup target add wasm32-unknown-unknown
```
* Clone the project found [here](https://github.com/zavodil/near-staking-pool-owner):
```
git clone https://github.com/zavodil/near-staking-pool-owner
```

* Compile smart contract:
```
cd near-staking-pool-owner/contract
cargo build --target wasm32-unknown-unknown --releas
```

* Deploy smart contract on your owner account. Adjust the path to .wasm file if required:
```
NEAR_ENV=shardnet near deploy <OWNER_ID>.shardnet.near --wasmFile target/wasm32-unknown-unknown/release/contract.wasm
```

* Initialize the smart contract picking accounts for splitting revenue:
```
CONTRACT_ID=<OWNER_ID>.shardnet.near
# Change numerator and denomitor to adjust the % for split.
NEAR_ENV=shardnet near call $CONTRACT_ID new '{"staking_pool_account_id": "<STAKINGPOOL_ID>.factory.shardnet.near", "owner_id":"<OWNER_ID>.shardnet.near", "reward_receivers": [["<SPLITED_ACCOUNT_ID_1>.shardnet.near", {"numerator": 3, "denominator":10}], ["<SPLITED_ACCOUNT_ID_2>.shardnet.near", {"numerator": 70, "denominator":100}]]}' --accountId $CONTRACT_ID
```
> **Example:**
> 
> ```
> CONTRACT_ID=btcsecure.shardnet.near
> NEAR_ENV=shardnet near call $CONTRACT_ID new '{"staking_pool_account_id": "btcsecure.factory.shardnet.near", "owner_id":"btcsecure.shardnet.near", "reward_receivers": [["maelstrom.shardnet.near", {"numerator": 6, "denominator":10}], ["iamamiwhoami.shardnet.near", {"numerator": 40, "denominator":100}]]}' --accountId $CONTRACT_ID
> ```

* Wait until you start receiving rewards on your node staking pool. Do a withdraw of rewards:
```
CONTRACT_ID=<OWNER_ID>.shardnet.near
NEAR_ENV=shardnet near call $CONTRACT_ID withdraw '{}' --accountId $CONTRACT_ID --gas 200000000000000
```
> **Example:**
> 
> ```
> CONTRACT_ID=btcsecure.shardnet.near
> NEAR_ENV=shardnet near call $CONTRACT_ID withdraw '{}' --accountId $CONTRACT_ID --gas 200000000000000
> ```
***
**Link to our successful transaction: <https://explorer.shardnet.near.org/transactions/5Z21wsQCgCFeY3F8xobw85HKUbYsdFjgQFJHavziJC2B>**
***

* **If you can't open the link in your browser, you can always use Near-CLI:**
```
near tx-status <hash> --accountId <accountid>.shardnet.near
```
> **Example:**
> 
> ```
> near tx-status 5Z21wsQCgCFeY3F8xobw85HKUbYsdFjgQFJHavziJC2B --accountId btcsecure.shardnet.near
> ```


**In confirmation that we have done everything correctly, we will see the following:**
![](https://github.com/BTCSecure/stakewars-3/blob/main/images/challenge-008/23-smart.png)



