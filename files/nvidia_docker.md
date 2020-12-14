# Nvidia Docker Installation

Reference [Here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
---

Step 1:
---
Docker-CE on Ubuntu can be setup using Docker’s official convenience script:
```
$ curl https://get.docker.com | sh \
    && sudo systemctl start docker \
    && sudo systemctl enable docker
```

Step 2:
---
Setup the stable repository and the GPG key:
```
$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
    && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
    && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
```

Step 3:
---
Install the nvidia-docker2 package (and dependencies) after updating the package listing:
```
$ sudo apt-get update
$ sudo apt-get install -y nvidia-docker2
```

Step 4:
---
Restart the Docker daemon to complete the installation after setting the default runtime:
```
$ sudo systemctl restart docker
```
At this point, a working setup can be tested by running a base CUDA container:
```
$ sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi  # replace "cuda:11.0" with your version.
```
This should result in a console output shown below:
```
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 455.23.04    Driver Version: 455.23.04    CUDA Version: 11.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  GeForce RTX 3090    Off  | 00000000:05:00.0 Off |                  N/A |
| 39%   30C    P0   101W / 350W |      0MiB / 24268MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   1  GeForce RTX 3090    Off  | 00000000:09:00.0 Off |                  N/A |
|  0%   39C    P0   106W / 350W |      0MiB / 24268MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   2  GeForce RTX 3090    Off  | 00000000:85:00.0 Off |                  N/A |
| 38%   33C    P0   108W / 350W |      0MiB / 24268MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
|   3  GeForce RTX 3090    Off  | 00000000:89:00.0 Off |                  N/A |
|  0%   32C    P0    67W / 350W |      0MiB / 24268MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

_NOTICE_:
---
Please modify the docker scource (USTC or Aliyun).
```
$ sudo vi /etc/docker/daemon.json
```
Update content:
```
{
  	"registry-mirrors": ["https://docker.mirrors.ustc.edu.cn"]
}
```
Then reload daemon and restart docker service.
```
$ sudo systemctl daemon-reload
$ sudo service docker restart
```