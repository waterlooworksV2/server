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
git clone https://github.com/waterlooworksV2/frontend.git
git clone https://github.com/waterlooworksV2/backend.git
cd frontend && yarn install && yarn build-css
cd ../backend && yarn install
```
## Running Steps

### `pm2`
```
cd backend
pm2 start npm --name "backend" -- start
cd ../frontend
pm2 start npm --name "frontend" -- start
```

<!-- ### -->
<!-- `ssh -L 192.168.0.10:8080:10.0.0.10:80 root@10.0.0.10` -->
