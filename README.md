# <p align="center">Docker Swarm</p>
### <p align="center">A deployment method and collection of basic docker swarm stacks.</p>

## tl;dr
```
sudo groupadd docker && sudo usermod -aG docker $USER && newgrp docker
```
```
rm deploy.sh && curl -fsSL https://raw.githubusercontent.com/suodrazah/docker_swarm/main/deploy.sh -o deploy.sh && sh deploy.sh
```

## Prerequisites:
* **_Tested on_ Ubuntu Server 20.04 LTS Local or [VPS](https://ca.ovh.com/au/order/vps/) Server**
  * If using OVH, in the Dashboard go the the IP tab and configure your firewall.
* **SSH Access**
* **Firewall configured to allow 80, 443, 22**
* **Public, static IP**
* **[Domain](https://domains.google.com/) pointing to servers public IP address**

## Notes:
* **Designed to be executed on a fresh platform**
* **All updates are handled**
* **Wait a minute or so for Traefik to come up after the script finishes**

## Deployment:
* **This will bring up Traefik and Portainer on a primary Docker Swarm node**
```
sudo groupadd docker
```
```
sudo usermod -aG docker $USER
```
```
newgrp docker
```
```
curl -fsSL https://raw.githubusercontent.com/suodrazah/docker_swarm/main/deploy.sh -o deploy.sh && sh deploy.sh
```

## Add Nodes (same private IPv4 LAN)
* Primary node:
```
docker swarm join-token manager
```  
* Worker node:
```
docker swarm join-token worker
```  
* Execute the resulting code on the node to be added
* Add a label to the new node
   * `Portainer`
   * `Swarm`
   * `<node>`
   * `+Label`
   * `Name` - <Node Name> e.g. worker1
   * `Value` - "True"

## Extension:
* Create a new stack
   * `Portainer`
   * `Stacks`
   * `Add Stack`
   * `Name` - e.g. client1-ignition
   * `Web editor` - copy contents of stack.yml file
   * `Environment variables` - as described by the stack comments

## Update:
* Take a snapshot or backup
* Run the script again
```
rm deploy.sh && curl -fsSL https://raw.githubusercontent.com/suodrazah/docker_swarm/main/deploy.sh -o deploy.sh && sh deploy.sh
```
