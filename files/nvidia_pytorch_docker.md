# Nvidia Pytorch Docker Installation

Please install nvidia docker as [_this_](nvidia_docker.md) first.
---
Check your docker version:
---
```
$ docker -v
```
And the version should larger than 19.02. 

Pull pytoch docker by:
---
```
$ docker pull nvcr.io/nvidia/pytorch:20.11-py3
```
Run docker by:
---
```
$ docker run --gpus all -it --rm -v local_dir:container_dir nvcr.io/nvidia/pytorch:xx.xx-py3
# xx should be your image version.
```