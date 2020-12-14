# Nvidia Driver Installation 


Step 1: Download Nvidia Driver 
---
Download the lasted driver from [LINK](https://www.nvidia.cn/Download/index.aspx?lang=cn).

Step 2: Uninstall Original Nvidia Driver
---
If there is an original nvidia driver, uninstall it. \
For example
```
$ sudo ./NVIDIA-Linux-x86_64-384.59.run --uninstall
```

Step 3: Disable Nouveau Driver
---
```
$ sudo vi /etc/modprobe.d/blacklist.conf
```
and add the two lines to the end of the text:
```
blacklist nouveau
options nouveau modeset=0
```
save and run
```
$ sudo update-initramfs -u
$ sudo reboot     # this will reboot your machine
```
then run
```
$ lsmod | grep nouveau
```
and there is no output.

Step 4: Disable X-Windows
---
run
```
$ sudo service lightdm stop
```

Step 5: Install Nvidia Driver
---
run
```
$ sudo chmod +x *.run
$ sudo ./NVIDIA-Linux-x86_64-440.82.run --no-opengl-files --no-x-check 
# replace "NVIDIA-Linux-x86_64-440.82.run" with your .run file.
```

Step 6: Test 
---
run
```
$ nvidia-smi
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