# 0G-DA-Node Install Guide

## System Requirements
| Category | Requirements |
| ------------ | ------------ |
| CPU | 2+ cores |
| RAM | 8+ GB |
| Bandwidth | 100 MBps for Download / Upload |

### System Update
```bash
sudo apt-get update
sudo apt-get install git cargo clang cmake build-essential pkg-config openssl libssl-dev protobuf-compiler
```
### Install Go
```bash
cd $HOME && \
ver="1.22.0" && \
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz" && \
sudo rm -rf /usr/local/go && \
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz" && \
rm "go$ver.linux-amd64.tar.gz" && \
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile && \
source ~/.bash_profile && \
go version
```
### Git Clone The Source Code
```bash
git clone -b v1.0.0-testnet https://github.com/0glabs/0g-da-client.git
```
### Run
```bash
cd ~/0g-da-client
make build
```

### Run combined server

<change input>
Config <run_combined> 

```bash
cd ~/0g-da-client/disperser
```
```bash
nano Makefile
```
Find run_combined then follow edit below
--chain.rpc https://rpc-testnet.0g.ai \
--chain.private-key <Your_private_key> \
--combined-server.storage.node-url http://0..0.0.0:5678 \ if you have url storage node
--combined-server.storage.flow-contract 0x8873cc79c5b3b5666535C825205C9a128B1D75F1 \

### Run
```bash
make run_combined
```
 
### Log ex
```bash
INFO [07-16|15:37:55.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:37:55.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:37:56.458|github.com/0glabs/0g-data-avail/disperser/apiserver/server.go:414]          [apiserver] latest finalized block number updated number=278,402 caller=server.go:414
INFO [07-16|15:37:57.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:37:57.211|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:37:59.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:37:59.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:38:00.210|github.com/0glabs/0g-data-avail/disperser/batcher/batcher.go:193]           [batcher] Creating batch                 ts=2024-07-16T15:38:00+0000 caller=batcher.go:193
INFO [07-16|15:38:01.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:38:01.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:38:01.462|github.com/0glabs/0g-data-avail/disperser/apiserver/server.go:414]          [apiserver] latest finalized block number updated number=278,403 caller=server.go:414
INFO [07-16|15:38:03.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:38:03.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:38:05.210|github.com/0glabs/0g-data-avail/disperser/batcher/batcher.go:193]           [batcher] Creating batch                 ts=2024-07-16T15:38:05+0000 caller=batcher.go:193
INFO [07-16|15:38:05.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:155] [encodingstreamer] requesting processing blobs.. caller=encoding_streamer.go:155
INFO [07-16|15:38:05.210|github.com/0glabs/0g-data-avail/disperser/batcher/encoding_streamer.go:170] [encodingstreamer] no new metadatas to encode caller=encoding_streamer.go:170
INFO [07-16|15:38:06.466|github.com/0glabs/0g-data-avail/disperser/apiserver/server.go:414]          [apiserver] latest finalized block number updated number=278,403 caller=server.go:414
```

```

 
