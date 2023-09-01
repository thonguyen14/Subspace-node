# Install docker and other support software
# !/bin/bash
```
     sudo apt update && sudo apt upgrade -y
     sudo apt install curl build-essential git wget jq make gcc ack tmux ncdu -y
     sudo wget -qO /usr/local/bin/yq https://github.com/mikefarah/yq/releases/download/v4.27.3/yq_linux_amd64 && chmod +x /usr/local/bin/yq
     apt update && apt install git sudo unzip wget -y
     curl -fsSL https://get.docker.com -o get-docker.sh
     sudo sh get-docker.sh
     curl -SL https://github.com/docker/compose/releases/download/v2.5.0/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
     sudo chmod +x /usr/local/bin/docker-compose
     sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
# Create folder and copy file docker-compose.yaml and change name , port as you like
```
    cd $HOME
    mkdir subspace1
    cd subspace1
    wget -O docker-compose.yaml https://raw.githubusercontent.com/thonguyen14/Subspace-node/main/Gemini3/docker-compose.yaml
```
# edit docker-compose.yaml file as you like
```
vi docker-compose.yaml
```
# you can check which port you are using by this command ̣( subspace use ports Node Port:30333 ,Node DSN Port:30433 ,Farmer Port:30533 )
```
    lsof -i -P -n | grep LISTEN
```
# start a node
```
    cd subspace1
    docker compose up -d
```
# show all docker running
```
    docker ps
```
# show logs
```
    docker compose logs -f --tail=100 | grep subspace1
```
# stop a node
```
    docker compose down
```
# If you want run the second node or n node, just change the code here, subspace2 --> subspacen
```
    cd $HOME
    mkdir subspace2
    cd subspace2
    wget -O docker-compose.yaml https://raw.githubusercontent.com/thonguyen14/Subspace-node/main/Gemini3/docker-compose.yaml
```
# Change ports, name, reward address inside docker-compose.yaml file and start node
```
    vi docker-compose.yaml
```
```
    cd subspace2
    docker compose up -d
```
# delete node
```
    cd subspace1
    docker compose down -v
    cd && rm -rf /root/subspace1/
```
