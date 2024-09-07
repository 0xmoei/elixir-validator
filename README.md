# elixir-validator


## System Requirements (Minimum-Recommended)
| Ram | cpu     | disk                      |
| :-------- | :------- | :-------------------------------- |
| `4 GB`      | `8 Core` | `30 GB SSD` |

## 1- Install Dependecies
```console
sudo apt update && sudo apt upgrade -y 
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```

## 2- Install docker
```console
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Docker version check
docker --version
```

## 3- Validator Private Key Generation
Create an EVM metamask wallet and write its private and public keys
> In Metamask, this can be done by clicking the "My Accounts" icon in the top right, and clicking "+ Create Account." You can obtain the private key by clicking Account Details from the ellipsis menu, and then clicking "Export private key".

## 4- Delegate MOCK Tokens To Your Validator
1. **Enter the [dashboard](https://testnet-3.elixir.xyz/)**
2. **Connect the wallet you created in step 3**
3. **Mint MOCK tokens**
4. **Stake them**
5. **Click `CUSTOM VALIDATOR` and enter your wallet public address and sign the tx**

## 5- Running Your Validator

1. **Pull the docker images**
```console
docker pull elixirprotocol/validator:v3
```

2. **Run Validator**
```
docker run -d \
  --env-file /path/to/validator.env \
  --name elixir \
  --restart unless-stopped \
  elixirprotocol/validator:v3
```
