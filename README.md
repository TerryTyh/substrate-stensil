<div align="center">

  <h1><code>substrate-stencil</code></h1>

  <strong>A template for kick starting a Rust and Blockchain project using <a href="https://github.com/paritytech/substrate">Substrate</a>.</strong>

  <h3>
    <a href="https://substrate.io/">Docs</a>
    <span> | </span>
    <a href="https://matrix.to/#/!HzySYSaIhtyWrwiwEV:matrix.org?via=matrix.parity.io&via=matrix.org&via=web3.foundation">Chat</a>
  </h3>

</div>

## Features

This template includes the minimum required components to start a PoS testnet, inspired by [substrate-node-template](https://github.com/substrate-developer-hub/substrate-node-template).

* Consensus related pallets: Babe & GRANDPA
* Staking related pallets: staking, session, authorship, im-online, offences, utility
* Governance related pallets: collective, membership, elections-phragmen, democracy, treasure

**Notes:** The code is un-audited and not production ready, use it at your own risk.

## Getting Started

Follow the steps below to get started.

### Rust Setup

First, complete the [Dev Docs Installation](https://docs.substrate.io/v3/getting-started/installation/).

### Build and Run

Use the following command to build the node and run it after build successfully:

```sh
cargo build --release
./target/release/substrate-stencil --dev
```

## 生成chain_spec
  ```sh
  ./target/release/substrate-stencil build-spec --chain staging > stencil-staging.json
  ```
## 编译chain_spec
  ```sh
  ./target/release/substrate-stencil build-spec --chain=stencil-staging.json --raw > stencil-staging-raw.json
  ```
## 创建node_key
  ```sh
  ./target/release/substrate-stencil key generate-node-key
  ```
<img width="763" alt="image" src="https://github.com/TerryTyh/substrate-stensil/assets/120092281/1fe0ad1c-c9cb-4f02-8932-7d65fcc2a40b">

## 启动bootnodes
  ```sh
  ./target/release/substrate-stencil \
       --node-key d51308ed26068c08a37bcf6b828146839cc0e6504e3771426c585c1dfb8e8521 \
       --base-path /tmp/bootnode1 \
       --chain stencil-staging-raw.json \
       --name bootnode1
  ```
  <img width="871" alt="image" src="https://github.com/TerryTyh/substrate-stensil/assets/120092281/2cd99a4b-613f-4ef4-9b91-f5090236f6c3">
   
## 启动验证节点validators
  ```shell
  ./target/release/substrate-stencil \
      --base-path  /tmp/validator1 \
      --chain   stencil-staging-raw.json \
      --bootnodes  /ip4/192.168.110.86/tcp/30333/p2p/12D3KooWD5VWTpY2euzJvRLbRDtp2WeiCe7JkTDKxMqPnmU8LRGo \
        --port 30336 \
        --ws-port 9947 \
        --rpc-port 9936 \
      --name  validator1 \
      --validator
  ```
<img width="822" alt="image" src="https://github.com/TerryTyh/substrate-stensil/assets/120092281/44c127fb-c7b7-4364-88df-9b79e24a67a3">

## 验证人节点启动后，在该验证节点添加用户Babe和Grandpa所使用的Key
  ```shell
// Babe使用的key
./target/release/substrate-stencil key insert --base-path /tmp/node01 \
  --chain stencil-staging-raw.json \
  --scheme sr25519 \
  --suri 0x861c6d95051f942bb022f13fc2125b2974933d8ab1441bfdee9855e9d8051556\
  --key-type babe
// GRANDPA使用的key
./target/release/substrate-stencil key insert --base-path /tmp/node01 \
  --chain stencil-staging-raw.json \
  --scheme ed25519 \
  --suri 0xac8fdba5bbe008f65d0e85181daa5443c2eb492fea729a5981b2161467f8655c\
  --key-type gran
  ```
<img width="612" alt="image" src="https://github.com/TerryTyh/substrate-stensil/assets/120092281/293bca4c-8991-46c5-b0d2-66d41e250195">

## Then
* Attract enough validators from community in waiting
* Call force_new_era in staking pallet with sudo, rotate to PoS validators
* Enable governance, and remove sudo
* Enable transfer and other functions
