# sound_event_detection

Sound Event Detection using Deep learning


## All Instructions to reproduce

### Install Anaconda


- [Link](https://linuxize.com/post/how-to-install-anaconda-on-centos-7/) to install anaconda.



```
sudo yum install wget

wget "https://repo.anaconda.com/archive/Anaconda3-2019.10-Linux-x86_64.sh" -O "Anaconda3-2019.10-Linux-x86_64.sh" -c

bash Anaconda3-2019.10-Linux-x86_64.sh
```

### Commands to install NVIDIA display and CUDA drivers

- [Link to install nvidia drivers and cuda](https://ahelpme.com/linux/centos7/install-cuda-and-nvidia-video-driver-under-centos-7/)

```
sudo yum update -y

sudo yum install -y yum-utils

sudo yum-config-manager --add-repo http://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/cuda-rhel7.repo

sudo yum install -y epel-release

sudo yum clean all

sudo yum -y install nvidia-driver-latest-dkms

sudo yum install kernel-devel

dkms status
```

- Now cd to /usr/src/

- *and use build similar to this*

```
dkms build nvidia/418.87.00

wget "https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda_9.0.176_384.81_linux-run"

sudo sh cuda_9.0.176_384.81_linux.run
```

*To uninstall the CUDA Toolkit, run the uninstall script in /usr/local/cuda-9.0/bin*

*To uninstall the NVIDIA Driver, ```run nvidia-uninstall```*


*[Link](https://github.com/deepinsight/insightface/wiki/INSTALL-Cuda9-ON-Centos7) to remove Nvidia drivers and cuda when things go wrong*

### Creating GCP bucket, GPU quota request and transfering files

```
git clone https://github.com/Kikyo-16/Sound_event_detection.git

git clone https://github.com/turpaultn/DCASE2019_task4.git
```

- GCP - IAM  - Quota - GPU quota increase

- *Created a bucket*

- *Transfer files from google drive to bucket*

```gcloud auth login (Updated to gcloud init)```

### Installing gcsfuse to mount bucket

- *Install GCSFuse from [here](https://github.com/GoogleCloudPlatform/gcsfuse/blob/master/docs/installing.md).*
```
gcsfuse kisha_bucket /kisha/data_bucket

sudo yum install unzip

sudo yum install dnf

sudo dnf install unrar
```

### Unzip and Unrar everything to their folders,
```
unrar e  unlabel_in_domain.rar /home/kisharenee123/data/

unzip test.zip -d /home/kisharenee123/data/

sudo chmod -R 777 Sound_event_detection/data/wav/ (To tackle permission error if necessary)
```
- *then move every wav file to wav folder in data using mv command*

### conda env creation and dependencies installation, all in this one script
```
sh conda_create_environment.sh

conda activate dcase2018

cd Sound_event_detection/data
```
### Renaming feature and label files and creating their respective folders
```
mv feature feature_txt

mv label label_txt

mkdir feature

mkdir label
```
### Edit scripts/gen_feature-2019.sh and scripts/gen_label-2019.sh, remove eval line
```
sh scripts/gen_feature-2019.sh

sh scripts/gen_label-2019.sh

sudo conda install jupyterlab

jupyter lab --ip=0.0.0.0 --no-browser --port=5000
```
- [Link](http://34.82.176.163:5000) to open Jupyter lab


### Reproduce DCASE2019 Task4 challenge results

- run

```
sh scripts/reproduce_Lin_ICT_task4_1.sh

sh scripts/reproduce_Lin_ICT_task4_2.sh

sh scripts/reproduce_Lin_ICT_task4_3.sh (the first place)

sh scripts/reproduce_Lin_ICT_task4_4.sh
```
### See details in challenge_results.
