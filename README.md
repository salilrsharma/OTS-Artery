# OTS-Artery

This repository contains the 

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

### Install OpenTrafficSim
OpenTrafficSim (OTS) can be setup by following the instruction at https://opentrafficsim.org/old/index.php/setting-up-eclipse

### Run OTS-Artery
1. Navigate to Artery directory and launch the CACC configuration of Artery by running the following command:
```
docker run -it --mount type=bind,source=$PWD/scenarios/ots-demo,target=/scenario --net host docker-artery -c cacc
```
2. Open a new terminal window and run the traffic simulation instance either directly from eclipse or using a jar file.
