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
git clone -b v1.0.2 https://github.com/0glabs/0g-da-node.git
```
```bash
cd $HOME/0g-da-node
git stash
git fetch --all --tags
git checkout 31060b7 
git submodule update --init
cargo build --release
```

### Setup config.toml
```bash
rm -rf $HOME/0g-da-node/config.toml && mv $HOME/0g-da-node/config_example.toml $HOME/0g-da-node/config.toml && nano $HOME/0g-da-node/config.toml
```

- Miner Private Keys = `could be the same as signer_eth_private_key, but not recommended`


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


 
