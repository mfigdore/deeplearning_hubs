Bootstrap: docker
From: tensorflow/tensorflow:1.8.0-gpu-py3

%environment
  # use bash as default shell
  SHELL=/bin/bash
  export SHELL

  # add CUDA paths
  CPATH="/usr/local/cuda/include:$CPATH"
  PATH="/usr/local/cuda/bin:$PATH"
  LD_LIBRARY_PATH="/usr/local/cuda/lib64:$LD_LIBRARY_PATH"
  CUDA_HOME="/usr/local/cuda"
  export CPATH PATH LD_LIBRARY_PATH CUDA_HOME
  
  # make conda accessible
  PATH=/opt/conda/envs/pytorch-py3.6/bin:$PATH
  export PATH

%setup
  # runs on host - the path to the image is $SINGULARITY_ROOTFS

%post
  # post-setup script

  # load environment variables
  . /environment

  # use bash as default shell
  echo 'SHELL=/bin/bash' >> /environment

  # make environment file executable
  chmod +x /environment

  # default mount paths
  mkdir /scratch /data /work-zfs 
  touch /usr/bin/nvidia-smi

  # user requests (contact marcc-help@marcc.jhu.edu)
  # load in extra packages for python
  apt-get update && apt-get -y install locales
  locale-gen en_US.UTF-8
  apt-get install -y git wget python3-dev python3-pip
  apt-get clean

  apt-get install -y libcupti-dev
  pip install --upgrade pip
  pip install keras
  pip install numpy scipy scikit-learn pandas 
  pip install pytest opencv tensorboard scikit-image spectrum nibabel tqdm
  
%runscript
  # executes with the singularity run command
  # delete this section to use existing docker ENTRYPOINT command

%test
  # test that script is a success
