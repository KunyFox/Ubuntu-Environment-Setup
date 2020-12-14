# Horovod Installation
Here we will install NCCL from source code, and install horovod with "pip".
## Step 1: Install NCCL 
Run
```
$ git clone https://github.com/NVIDIA/nccl 
$ cd nccl
$ sudo make install
```

## Step 2: Install Horovod
Run
```
$ HOROVOD_GPU_ALLREDUCE=NCCL HOROVOD_WITH_TENSORFLOW=1  pip install --no-cache-dir horovod
```