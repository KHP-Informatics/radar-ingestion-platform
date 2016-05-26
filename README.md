# radar-ingestion-platform

###dependencies
- Docker
- Java version >=1.7
- Git

## This package includes
- Shimmer
- Confluent 3.0.0

## Start by cloning this repo

`git clone https://github.com/cbitstech/radar-ingestion-platform`

##install and sshimmer
These steps will install a Docker container with nginx, MongoDB, OpenJDK, and a preconfigured Shimmmer instance.
For more information on Shimmer visit [http://www.getshimmer.co/]

Prepare environment variables, replacing host with the IP or domain name of your Docker host.

`eval "$(docker-machine env host)`

If in Docker <=1.4 compose your Docker files using the included shell script

`./shimmer/update-compose-files.sh`

Download and start the containers by running (If you want to see logs and keep the containers in the foreground, omit the -d.)

`shimmer/docker-compose up -d`

Access your active Shimmer instance at:

`http://<your-docker-host-ip>:8083`

##install and start confluent platform

This






