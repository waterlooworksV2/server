# `server` setup instructions
> mostly so that I don't forgot what I have to do

## Installation steps

### Install Node.js/NPM
Instructions [here](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages)

### Install `yarn`
`npm i yarn -g`

### Install `pm2`
`npm install pm2@latest -g`

### Install and run ElasticSearch
Instructions [here](https://www.elastic.co/guide/en/elasticsearch/reference/current/deb.html)
- Might have to restart after setting up to run on startup

### Install and run MongoDB
Instructions [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)
- failure help on [SO](https://stackoverflow.com/questions/28945921/e-unable-to-locate-package-mongodb-org)
### SCP database file
`scp local/path/to/dump:dump root@IP:remote/path/to/dump`
#### Unzip the file
```
sudo apt-get install unzip
unzip dump.zip
mongorestore dump
```

### Clone repos
```
git clone https://github.com/waterlooworksV2/backend.git
cd backend && yarn install
```
## Running Steps

### Initialise `.env` in the backend repo

### `pm2`
```
pm2 start npm --name "backend" -- start
```

### `certbot-verif`
Instruction [here](https://github.com/waterlooworksV2/certbot-verif/blob/master/instructions.pdf)

### `ufw`
Instructions [here](https://serverfault.com/questions/317595/copy-ufw-rules-between-servers)
`user.rules`
```
### RULES ###

### tuple ### deny any 9200 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 9200 -j DROP
-A ufw-user-input -p udp --dport 9200 -j DROP

### tuple ### deny any 27017 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 27017 -j DROP
-A ufw-user-input -p udp --dport 27017 -j DROP

### tuple ### allow any 22 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 22 -j ACCEPT
-A ufw-user-input -p udp --dport 22 -j ACCEPT

### tuple ### allow any 80 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 80 -j ACCEPT
-A ufw-user-input -p udp --dport 80 -j ACCEPT

### tuple ### allow any 443 0.0.0.0/0 any 0.0.0.0/0 in
-A ufw-user-input -p tcp --dport 443 -j ACCEPT
-A ufw-user-input -p udp --dport 443 -j ACCEPT

### END RULES ###

### LOGGING ###
-A ufw-after-logging-forward -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-I ufw-logging-deny -m conntrack --ctstate INVALID -j RETURN -m limit --limit 3/min --limit-burst 10
-A ufw-logging-deny -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-A ufw-logging-allow -j LOG --log-prefix "[UFW ALLOW] " -m limit --limit 3/min --limit-burst 10
### END LOGGING ###

### RATE LIMITING ###
-A ufw-user-limit -m limit --limit 3/minute -j LOG --log-prefix "[UFW LIMIT BLOCK] "
-A ufw-user-limit -j REJECT
-A ufw-user-limit-accept -j ACCEPT
### END RATE LIMITING ###
COMMIT
```
`user6.rules`
```
### RULES ###

### tuple ### deny any 9200 ::/0 any ::/0 in
-A ufw6-user-input -p tcp --dport 9200 -j DROP
-A ufw6-user-input -p udp --dport 9200 -j DROP

### tuple ### deny any 27017 ::/0 any ::/0 in
-A ufw6-user-input -p tcp --dport 27017 -j DROP
-A ufw6-user-input -p udp --dport 27017 -j DROP

### tuple ### allow any 22 ::/0 any ::/0 in
-A ufw6-user-input -p tcp --dport 22 -j ACCEPT
-A ufw6-user-input -p udp --dport 22 -j ACCEPT

### tuple ### allow any 80 ::/0 any ::/0 in
-A ufw6-user-input -p tcp --dport 80 -j ACCEPT
-A ufw6-user-input -p udp --dport 80 -j ACCEPT

### tuple ### allow any 443 ::/0 any ::/0 in
-A ufw6-user-input -p tcp --dport 443 -j ACCEPT
-A ufw6-user-input -p udp --dport 443 -j ACCEPT

### END RULES ###

### LOGGING ###
-A ufw6-after-logging-forward -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-I ufw6-logging-deny -m conntrack --ctstate INVALID -j RETURN -m limit --limit 3/min --limit-burst 10
-A ufw6-logging-deny -j LOG --log-prefix "[UFW BLOCK] " -m limit --limit 3/min --limit-burst 10
-A ufw6-logging-allow -j LOG --log-prefix "[UFW ALLOW] " -m limit --limit 3/min --limit-burst 10
### END LOGGING ###

### RATE LIMITING ###
-A ufw6-user-limit -m limit --limit 3/minute -j LOG --log-prefix "[UFW LIMIT BLOCK] "
-A ufw6-user-limit -j REJECT
-A ufw6-user-limit-accept -j ACCEPT
### END RATE LIMITING ###
COMMIT
```
<!-- ### -->
<!-- `ssh -L 192.168.0.10:8080:10.0.0.10:80 root@10.0.0.10` -->
