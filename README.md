# `server` setup instructions
> mostly so that I don't forgot what I have to do

## Installation steps

### Install Node.js/NPM
Instructions [here](https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions-enterprise-linux-fedora-and-snap-packages)

### Install `yarn`
`npm i yarn`

### Install `pm2`
`npm install pm2@latest -g`

### Install ElasticSearch
`wget` the DEB url [here](https://www.elastic.co/downloads/elasticsearch)

### Install MongoDB
Instructions [here](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/)

### SCP database file
`scp local/path/to/dump:dump root@IP:remote/path/to/dump`

<!-- ## Running Steps -->
