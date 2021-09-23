# OTS-Artery

This repository contains the 

## System requirements

## Instructions

### Build a docker image of Artery
1. Install docker for Windows and test it using the following code:
```
docker ps
```
2. Git Clone the Artery project located at https://github.com/riebl/artery.git

3. Move to artery folder with contains the 'Dockerfile':
```
cd artery
```
4. Now execute the following code:
```
git submodule update --init --recursive
```
5. Build the docker image using the following code:
```
docker build --tag docker-artery
```
6. Display the docker images using the following code:
```
docker images
```

We should be able to see the 'docker-artery' image.

### Install OpenTrafficSim (OTS)
OpenTrafficSim (OTS) can be setup by following the [instructions](https://github.com/salilrsharma/OTS-Artery/blob/main/install_OTS.md). For further help with designing and running a traffic simulation case, please refer to the [user manual of OpenTrafficSim](https://opentrafficsim.org/manual/).

### Run OTS-Artery
1. Navigate to Artery directory and launch the CACC configuration of Artery by running the following command:
```
docker run -it --mount type=bind,source=$PWD/scenarios/ots-demo,target=/scenario --net host docker-artery -c cacc
```
2. Open a new terminal window and run the traffic simulation instance either directly from eclipse or using a jar file.
