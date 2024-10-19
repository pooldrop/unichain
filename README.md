# Unichain Node 

## Hardware requirements:

| **Hardware** | **Minimum Requirement** |
|--------------|-------------------------|
| **CPU**      | 6 Cores                 |
| **RAM**      | 8 GB                    | 
| **Disk**     | 100  GB  SSD            |

---

## Install Docker

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version
```

- Y Enter

## Install Docker-Compose

```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
## Docker Permission to User

```
sudo groupadd docker
sudo usermod -aG docker $USER
```
## Clone UniChain Node

```
git clone https://github.com/Uniswap/unichain-node
cd unichain-node
```

## Update to new releases

```
git stash
git pull
```
## Edit env file

```
nano .env.sepolia
```



- Get [Endpoints](https://ethereum-sepolia.publicnode.com/)

> Replace `OP_NODE_L1_ETH_RPC` with `Sepolia RPC`  

> Replace `OP_NODE_L1_BEACON` with `Sepolia Beacon API` 

- CTRL X Y Enter to save the file

## Start Node

```
docker compose up -d
```

## Save Node PrivateKey
```
cat $HOME/unichain-node/geth-data/geth/nodekey
```
## Unichain Status:

```
curl -d '{"id":1,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' -H "Content-Type: application/json" http://localhost:8545
```

## How to update to new releases

```
docker compose down
git stash
git pull
```
- After this you need to edit .env.sepolia and docker file again
