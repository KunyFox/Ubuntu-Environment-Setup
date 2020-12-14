# MXNet Docker Installation
Here we chose the dockers from [_LINK_](https://ngc.nvidia.com/catalog/containers), which contain MXNet, CUDA and Horovod. And [nvidia docker](nvidia_docker.md) should be install first.

VERSION:
---
```
+---------------+--------------+------------------------------------------------+
|     MXNet     |     CUDA     |                     command                    |
|===============+==============+================================================|
|     1.5.1     |     10.1     |  docker pull nvcr.io/nvidia/mxnet:19.12-py3    |
+---------------+--------------+------------------------------------------------+
|     1.6.0     |     10.2     |  docker pull nvcr.io/nvidia/mxnet:20.03-py3    |
+---------------+--------------+------------------------------------------------+
|     1.6.0     |     11.0     |  docker pull nvcr.io/nvidia/mxnet:20.06-py3    |
+---------------+--------------+------------------------------------------------+
|     1.8.0     |     11.1     |  docker pull nvcr.io/nvidia/mxnet:20.11-py3    |
+---------------+--------------+------------------------------------------------+
```

Installation and Run
---
```
$ docker pull nvcr.io/nvidia/mxnet:XX.XX-py3    # xx should be replaced by your version.
$ docker run --gpus all -it --rm -v /data0:/data0 nvcr.io/nvidia/mxnet:xx.xx-py3    
```
