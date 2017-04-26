## Decred Wallet Dockerfile

This repository maintains the [Decred wallet](http://decred.org/) **Dockerfile** for [Docker](https://www.docker.com/).

The repo [automatically builds](https://hub.docker.com/r/reiuiji/dcrwallet/) and publishes the docker image to the [Docker Hub Registry](https://hub.docker.com/).

### Base Docker Image

* [CentOS:Latest](https://github.com/docker-library/docs/tree/master/centos)

### Installation

1. Install [Docker](https://www.docker.com/).

2. Run [Decred Daemon](https://github.com/Reiuiji/docker-dcrd) local or on another machine. Follow Decred [dcrd setup guide](https://docs.decred.org/getting-started/user-guides/dcrd-setup/) to configure RPC credentials.

3. Download [automated build](https://hub.docker.com/r/reiuiji/dcrwallet/) from public [Docker Hub Registry](https://www.docker.com/):

    `docker pull reiuiji/dcrwallet`

   (alternatively, you can build an image from Dockerfile)

### Building
To build this docker container run the following commands after you edited the dcrwallet.conf file
````bash
docker build -t="reiuiji/dcrwallet" github.com/reiuiji/dcrwallet
````

### Usage
This docker image can either be configured before build or attach the config.

#### If you want to change the provided dcrwallet.conf, you should do the following:
````bash
docker cp /path/to/your/dcrwallet.conf:/data/dcrwallet.conf
````
#### Run your dcrwallet container

````bash
docker run -d --name="dcrwallet" reiuiji/dcrwallet
````
#### If you need to expose RPC ports 9110 for dcrctl 

````bash
docker run -d -p 9110:9110 -name dcrwallet reiuiji/dcrwallet
````
**NOTE**: exposing port can be vary bad, make sure your RPC credentials are strong(32+).

#### If you only want to tweak the dcrwallet.conf, you can run a temp link:

````bash
docker run -d -p 9109:9109 -name dcrwallet -v /path/to/your/dcrwallet.conf:data/dcrwallet.conf reiuiji/dcrwallet
````
#### If you want to run with the built in volume of the entire dcrwallet daemon:

````bash
docker run -d --name="dcrwallet" -v /path/to/your/.dcrwallet/data:/data reiuiji/dcrwallet
````
**NOTE**: Make sure the directory on your system have the `dcrwallet.conf` file

### Checking if it works
To check if `dcrwallet` is working you can check the docker logs

````bash
docker logs dcrwallet
````
### Shutting down the docker container
If you need to close down the docker container you can run the following:

````bash
docker kill --signal=SIGINT dcrwallet
````
**NOTE**: sending a SIGINT (crtl+c) will have `dcrwallet` shutdown safely

### Referances
 * [docker cheat sheet](https://github.com/wsargent/docker-cheat-sheet)

### License
This code is under the MIT License.

### Donation
If you like this and want to see more, please donate :)

DsXSh151DsJpEA8mrAW5gCfVVqNCK8vQAss
