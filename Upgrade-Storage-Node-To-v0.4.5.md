# Upgrade Your Storage Node to v0.4.5

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
### Then Backup Your File Config.toml
```bash
mv /root/0g-storage-node/run/config-testnet-turbo.toml /root/config-testnet-turbo_backup.toml
```
### 1. Git Download
```bash
cd $HOME/0g-storage-node
git stash
git fetch --all --tags
git checkout 6cf05d2d50e7e84a631c858cf38d97430030c830 
git submodule update --init
```
### 2. Then Build It
```bash
cargo build --release
```

### 3. Check Your Version After Git Download
```bash
$HOME/0g-storage-node/target/release/zgs_node --version
```
<change input>
Its has to be in v0.4.5

### 4. Move Config.toml Back
```bash
mv /root/config-testnet-turbo_backup.toml /root/0g-storage-node/run/config-testnet-turbo.toml
```
- Its the same as the previous file config.toml  
- No changes are required in config.toml compared 
 
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

 
