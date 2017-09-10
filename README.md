# advancedtf
Advanced TensorFlow

<div align="center">
  <img src="https://www.tensorflow.org/images/tf_logo_transp.png"><br><br>
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


### Installation and Setup
## Step 1:-
# Audience 1 - Students without a local machine with GPU
Acquire the machine:-
Different sources can be 
a) Google Cloud
b) Microsoft Azure Cloud
c) AWS Cloud
d) Any third party Infrastructure as a service provider

a)
Installation steps on Google Cloud
Go to https://cloud.google.com/ and register your account
Recommended:- Try to use Google free tier for first few videos https://cloud.google.com/free/

Now to setup a machine, follow the quick start to setup either a Linux or Windows VM. Throughout the Sections, i shall be doing it with a machine booted with Linux 16.04 LTS
https://cloud.google.com/compute/docs/

Also on google cloud to launch a machine with gpu it might be that you may have to open a support request to increase your quota of gpu in a particular region. 
https://console.cloud.google.com/iam-admin/quotas


Also, you can always check the following link around which regions have gpus
https://cloud.google.com/compute/docs/gpus/

Now we move forward creating a cloud machine on Google cloud platform
a.	Go to link https://console.cloud.google.com/compute
b.	Click on create instance
c.	Add certain details here:-
	a.	Name your instance (eg tfgpu)
	b.	Choose region where gpu support is available assuming quota request is already raised
	c.	Customize machine type (For current section we don’t need heavy machine so we can just choose 2 vCPUs and minimal 6 – 8 GBRAM )
	d.	To configure machine with GPU click on customize
	e.	Select a 50 gb standard persistent disk
	f.	Click save and it might take few seconds to get the machine up and running

d.Click on ssh to enter into the machine and new browser will open from where you will enter into the terminal of the machine


# Audience 2 - Students with a local machine with GPU on it.
Machine can be Linux, Mac or Windows
They should directly move to setting up docker as per the respective machine environment



## Step 2
Setup Docker irrespective of whether you are running setting up environment on local or cloud machine
a) Windows

b) OS X

c) Linux


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


