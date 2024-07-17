# 0G-DA-Node Install Guide

## System Requirements
| Category | Requirements |
| ------------ | ------------ |
| CPU | 8+ cores |
| RAM | 16+ GB |
| Storage | 1 TB NVME SSD |
| Bandwidth | 100 MBps for Download / Upload |

### System Update
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install curl git wget htop tmux build-essential jq make lz4 gcc unzip -y
```
### Git download
```bash
git clone https://github.com/0glabs/0g-da-node.git
```
### Install Rust & Check Version
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
rustc --version
```
### lib install
```bash
sudo apt-get update
```
```bash
sudo apt install libssl-dev
```
```bash
sudo apt install pkg-config
```
```bash
sudo apt-get install protobuf-compiler
```
```bash
sudo apt-get install clang
```
```bash
sudo apt-get install llvm llvm-dev
```

### build
```bash
cd && cd 0g-da-node
```
```bash
cargo build --release
```
### amt download
```bash
cd dev_support
```
```bash
./download_params.sh
```
```bash
sudo cp -R /root/0g-da-node/dev_support/params /root/0g-da-node/target/release
```
### Bls key gen
```bash
cd
cd 0g-da-node
```
```bash
cargo run --bin key-gen
```
<change input>
DONT FORGET TO COPY YOUR BLS KEY!!!
 
### config.toml set
```bash
mv /root/0g-da-node/config_example.toml /root/0g-da-node/config.toml
sudo nano /root/0g-da-node/config.toml
```

- grpc_listen_address = "0.0.0.0:34000" 
- eth_rpc_endpoint = "http://Validator rpc ip:8545" 
- socket_address = "your node ip:34000" 
- da_entrance_address = "0xDFC8B84e3C98e8b550c7FEF00BCB2d8742d80a69" 
- start_block_number = 802 
- signer_bls_private_key = "Bls key gen paste" 
- signer_eth_private_key = "validator eth private key"

### Systemd create
```bash
sudo tee /etc/systemd/system/da.service > /dev/null <<EOF
[Unit]
Description=DA Node
After=network.target

[Service]
User=root
WorkingDirectory=$HOME/0g-da-node/target/release
ExecStart=$HOME/0g-da-node/target/release/server --config $HOME/0g-da-node/config.toml
Restart=on-failure
RestartSec=10
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
### Systemd start
```bash
sudo systemctl daemon-reload && \
sudo systemctl enable da && \
sudo systemctl start da
```
### System log
```bash
sudo journalctl -u da -f -o cat
```

 
