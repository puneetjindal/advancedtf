# advancedtf
Advanced TensorFlow

<div align="center">
  <img src="https://upload.wikimedia.org/wikipedia/commons/2/2d/Tensorflow_logo.svg"><br><br>
</div>

**TensorFlow** is an open source software library for numerical computation using
data flow graphs.  The graph nodes represent mathematical operations, while
the graph edges represent the multidimensional data arrays (tensors) that flow
between them.  This flexible architecture lets you deploy computation to one
or more CPUs or GPUs in a desktop, server, or mobile device without rewriting
code.  TensorFlow also includes TensorBoard, a data visualization toolkit.

https://www.tensorflow.org/

TensorFlow was originally developed by researchers and engineers
working on the Google Brain team within Google's Machine Intelligence Research
organization for the purposes of conducting machine learning and deep neural
networks research.  The system is general enough to be applicable in a wide
variety of other domains, as well.


# Installation and Setup

## **Step 1:-**

**Audience 1 - Cloud Installation**
**Different sources can be**
* a) Google Cloud
* b) Microsoft Azure Cloud
* c) AWS Cloud
* d) Any third party Infrastructure as a service provider e.g. Digital Ocean e.t.c.

**a)Installation steps on Google Cloud**
* Go to https://cloud.google.com/ and register your account

*Recommended:- Try to use Google free tier for first few videos https://cloud.google.com/free/*

* Now, setup a machine, follow the quick start to setup either a Linux(preferable) or Windows VM. 

Throughout the Sections, i shall be doing it with a machine booted with Linux 16.04 LTS
https://cloud.google.com/compute/docs/

Also you may have to open a support request to increase your quota of gpu in a particular region on google cloud before launching a machine with gpu.
Click here https://console.cloud.google.com/iam-admin/quotas

Also, you can always check the following link around which regions have gpus
*Click here to https://cloud.google.com/compute/docs/gpus/*

* Now we move forward creating a cloud machine on Google cloud platform
* a.	Go to link https://console.cloud.google.com/compute
* b.	Click on create instance
* c.	Add certain details here:-
	* a.	Name your instance (eg tfgpu)
	* b.	Choose region where gpu support is available assuming quota request is already raised
	* c.	Customize machine type (For current section we don’t need heavy machine so we can just choose 2 vCPUs and minimal 6 – 8 GBRAM )
	* d.	To configure machine with GPU click on customize
	* e.	Select a 50 gb standard persistent disk
	* f.	Click save and it might take few seconds to get the machine up and running

* d.Click on ssh to enter into the machine and new browser will open from where you will enter into the terminal of the machine


#### *GPU specific installation*
**Benefits of GPU containerization**
*https://github.com/NVIDIA/nvidia-docker/wiki/Motivation*

```
sudo apt install nvidia-modprobe
```
```
sudo service nvidia-docker start
```
*https://cloud.google.com/compute/docs/gpus/add-gpus#install-driver-script*


**b)Installation steps on Microsoft Azure Cloud**

* Register on Azure cloud by https://portal.azure.com/ where you have to go through their signup process and you will get some initial credits as per terms of conditions. Please check before entering any credit card information.

* After this go to https://docs.microsoft.com/en-us/azure/virtual-machines/ based on Operating system(prefer Linux Ubuntu 16.04 LTS) you are comfortable with

Go to https://azure.microsoft.com/en-in/free/

Signup for N-series GPU machine as per your convenience

**Following are some helpful links**

* a) Follow the below link till connecting to VM with SSH
*https://blogs.msdn.microsoft.com/uk_faculty_connection/2017/03/27/azure-gpu-tensorflow-step-by-step-setup/*

* b)Follow this link to complete GPU driver installation on the machine till  Install nvidia-docker
*https://kampta.github.io/Azure-GPU-VM-Getting-Started/*
or 

Follow the links here
https://github.com/NVIDIA/nvidia-docker/wiki/Deploy-on-Azure*


**3)Installation steps on AWS cloud**

*https://docs.docker.com/machine/examples/aws/*

* Step 1. Sign up for AWS and configure credentials

* Step 2. Use Machine to create the instance

* Step 3. Run Docker commands on the instance

or 
*Follow the below nicely explained link till "Setup nvidia-docker"
https://medium.com/towards-data-science/how-to-set-up-deep-learning-machine-on-aws-gpu-instance-3bb18b0a2579*



**Audience 2 - Students with a local machine with GPU on it.**
* Machine can be Linux, Mac or Windows
*They should directly move to setting up docker as per the respective machine environment*



## Step 2
Setup Docker engine if you still doesn't have docker setup on your machine.

Docker is the world’s leading software container platform. Developers use Docker to eliminate “works on my machine” problems when collaborating on code with co-workers. Operators use Docker to run and manage apps side-by-side in isolated containers to get better compute density. Enterprises use Docker to build agile software delivery pipelines to ship new features faster, more securely and with confidence for both Linux, Windows Server, and Linux-on-mainframe apps.

To get to know about the basic concepts on docker visit https://docs.docker.com/engine/docker-overview/

Setup Docker irrespective of whether you are running setting up environment on local or cloud machine
a) Windows

b) OS X

c) Linux
https://docs.docker.com/engine/installation/linux/docker-ce/ubuntu/#uninstall-old-versions
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-16-04

```
sudo apt-get remove docker docker-engine docker.io
```

Update the apt package index:
```
sudo apt-get update
```

```
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

```
sudo apt-key fingerprint 0EBFCD88
```

```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

```
sudo apt-get update
```

```
sudo apt-get install docker-ce
```

## Step 3
Create a volume to enable persistence so that even after shutting down the system, work is saved
```
sudo docker volume create vol_tf
```
Here volume created is *vol_tf*
Refer https://docs.docker.com/engine/reference/commandline/volume/ for better understanding


Pull the docker image and start the container with all the environment completely setup
```
sudo docker run -it -p 8888:8888 -p 6006:6006 -v test_vol:/notebooks tensorflow/tensorflow:latest-py3
```
Explanation on the command
1. Docker command is pulling image tagged as "tensorflow:latest-py3" on tensorflow repository on dockerhub
2. The argument with -v says thats test_vol on the host machine should be mounted to the /notebooks directory inside the container
3. 
Refer https://docs.docker.com/engine/reference/run/ for more details


## Step 4
Try your first TensorFlow program
$ python3

>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> sess.run(hello)
'Hello, TensorFlow!'
>>> a = tf.constant(10)
>>> b = tf.constant(32)
>>> sess.run(a + b)
42
>>> sess.close()

## Step 5
Open a browser
Go to http:<ip-address>:8888 and you should be able to open Jupyter Notebook environment in the browser
Go to http:<ip-address>:6006 and you should be able to open Tensorboard environment in the browser


