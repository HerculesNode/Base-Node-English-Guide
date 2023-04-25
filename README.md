![image](https://user-images.githubusercontent.com/101635385/224575552-0347013d-400d-44a0-8ea7-955bb2fde062.png)


<h1 align="center"> Base Node </h1>
<h1 align="center"> Base Node installation guide <br> << Hercules >>
</h1>

## 🟢 information

There is no incentive for Base Node. 
Base is a Coinbase Brand, so I think every transaction is important. <br>


### link
 * [Hercules Node Telegram](https://t.me/HerculesNode)
 * [Hercules Twitter](https://twitter.com/Hercules4413)
 * [Base Dc](https://discord.gg/buildonbase)
 
 ## 🟢 Hardware requirements

 * at least 16 GB RAM
 * an SSD drive with at least 100 GB free
 
 
## :one: System Update
```shell
sudo apt update
```

```shell
sudo apt upgrade
```


## :two: Docker Setup

```shell
apt install docker-compose
```

```shell

sudo apt-get update && sudo apt install jq && sudo apt install apt-transport-https ca-certificates curl software-properties-common -y && curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - && sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable" && sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin && sudo apt-get install docker-compose-plugin

```
<br><br>

## :three: Clone Base Files.

```
git clone https://github.com/base-org/node.git
```

## :four: Screen create
```
screen -S base
```

## 5️⃣ Base directory
```
cd node
```

## 6️⃣ Let's edit the Compose file

We will log in to the docker-compose.yml file and add only ETH-Goerli RPC here.


<br><br>
Modify this field : OP_NODE_L1_ETH_RPC=`https://ethereum-goerli-rpc.allthatnode.com`
<br>
Replace it with the RPC you received here and save with ctrl + x.


```
nano docker-compose.yml
```

![image](https://user-images.githubusercontent.com/101635385/234244308-142ad22a-fd18-4399-a441-b10a174ebdce.png)



## 7️⃣ Let's start our node.

<br>

this process will take a while, wait. You will get a printout like in the picture. <br>

```
docker compose up
```

![image](https://user-images.githubusercontent.com/101635385/224575974-59704a03-6f97-4831-9461-03fee8d00793.png)


After the operations are finished, you will see a log in this way Synchronising. That's it for now

![image](https://user-images.githubusercontent.com/101635385/224576077-60d2aae7-5dbc-42a5-8881-42e7a29afb62.png)



## 🟢 v0.1.1 Update
```shell
docker-compose stop
``` 

```shell
docker-compose build
``` 

```shell
docker-compose up
``` 
 

<br>

#### 🟢 Useful commands


After doing `docker compose up` , come to the main directory. Do not do it in Screen. Enter the command below and you should get output as in the picture.

```
curl -d '{"id":0,"jsonrpc":"2.0","method":"eth_getBlockByNumber","params":["latest",false]}' \
  -H "Content-Type: application/json" http://localhost:8545
```
![image](https://user-images.githubusercontent.com/101635385/224576325-64d53939-3ea7-4527-84b9-e9f8f0aec477.png)

<br>


Do the command to look at the synchronisation progress in the main directory, do not do it in the base screen, you can exit with ctrl + a + d.

```
echo Latest synced block behind by: $((($(date +%s)-$( \
  curl -d '{"id":0,"jsonrpc":"2.0","method":"optimism_syncStatus"}' \
  -H "Content-Type: application/json" http://localhost:7545 | \
  jq -r .result.unsafe_l2.timestamp))/60)) minutes
```


don't forget to like and Fork :)
