# 0G-DA-Node Upgrade Install Guide

## System Requirements
| Category | Requirements |
| ------------ | ------------ |
| CPU | 2+ cores |
| RAM | 8+ GB |
| Bandwidth | 100 MBps for Download / Upload |

### Stop service
```bash
sudo systemctl stop da
```
### Update
```bash
git clone https://github.com/0glabs/0g-da-node.git
cd 0g-da-node
git checkout tags/v1.0.2 -b v1.0.2
```
```bash
cargo build --release
```

### Setup config.toml
```bash
rm -rf $HOME/0g-da-node/config.toml && mv $HOME/0g-da-node/config_example.toml $HOME/0g-da-node/config.toml && nano $HOME/0g-da-node/config.toml
```
- Add this line to your `config.toml`

```bash
# miner eth account private key, (could be the same as `signer_eth_private_key`, but not recommended)
miner_eth_private_key = ""
```
- Miner Private Keys = `could be the same as signer_eth_private_key, but not recommended`

![image](https://github.com/user-attachments/assets/56e587af-f62e-4a8d-bb5b-3ff879888bc5)

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


 
