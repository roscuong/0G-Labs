# Upgrade Your Storage Node v0.3.3 to v0.3.4

## System Requirements
| Category | Requirements |
| ------------ | ------------ |
| CPU | 4+ cores |
| RAM | 16+ GB |
| Storage | 500GB / 1T NVME SSD |
| Bandwidth | 500 MBps for Download / Upload |

### Stop Your Node first
```bash
sudo systemctl stop zgs
```
### Git Download
```bash
cd $HOME
rm -rf /root/0g-storage-node
git clone https://github.com/0glabs/0g-storage-node.git
cd $HOME/0g-storage-node
git stash
git fetch --all --tags
git tag -d v0.3.4
git checkout 5b6a4c716174b4af1635bfe903cd4f82894e0533
git submodule update --init
sudo apt install cargo
```
### Then Build It
```bash
cargo build --release
```

### Check Your Version After Git Download
```bash
$HOME/0g-storage-node/target/release/zgs_node --version
```
<change input>
Its has to be in v0.3.4

### Check Your Config.toml
```bash
nano $HOME/0g-storage-node/run/config.toml
```
<change input>
Its the same as the previous file `config.toml` IN V0.3.3
 
### Restart Your Node
```bash
sudo systemctl restart zgs
```

### Check Your Log
```bash
tail -f ~/0g-storage-node/run/log/zgs.log.$(TZ=UTC date +%Y-%m-%d)
```
### Check Peers Connected
```bash
curl -X POST http://localhost:5678 -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"zgs_getStatus","params":[],"id":1}'  | jq
```
### CONGRATULATIONS MATE!!!

 
