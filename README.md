# cair-gpu
Dockerfiles for use with cair's GPU servers.
Coordinate changes on Slack: <https://cair-gpu.slack.com>

## Getting access
Contact [Sigurd Brinch](mailto:sigurd.k.brinch@uia.no) to get access

## Available resources

## Guidelines
* All experiments must be run in [docker containers](https://docs.docker.com/get-started/).
* The containers must be prepared to run on the [NVIDIA Docker Engine](https://nvidia.github.io/nvidia-docker/).
* Important notices:
  * *While docker containers provide isolated environments, they also provide root access to the host machine.*
  * *Assume that all users have access to all data stored on the servers.*
  * *All users have access to all containers, do not mess with other people’s work*

## Using docker
1. Check for available GPUs:
```bash
nvidia-smi
```
```bash
sigurdkb@cair-gpu04:~$ nvidia-smi
Fri Nov  2 10:11:54 2018
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 410.48                 Driver Version: 410.48                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  Tesla V100-SXM3...  On   | 00000000:34:00.0 Off |                    0 |
| N/A   30C    P0    50W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   1  Tesla V100-SXM3...  On   | 00000000:36:00.0 Off |                    0 |
| N/A   30C    P0    49W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   2  Tesla V100-SXM3...  On   | 00000000:39:00.0 Off |                    0 |
| N/A   34C    P0    52W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   3  Tesla V100-SXM3...  On   | 00000000:3B:00.0 Off |                    0 |
| N/A   36C    P0    53W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   4  Tesla V100-SXM3...  On   | 00000000:57:00.0 Off |                    0 |
| N/A   32C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   5  Tesla V100-SXM3...  On   | 00000000:59:00.0 Off |                    0 |
| N/A   35C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   6  Tesla V100-SXM3...  On   | 00000000:5C:00.0 Off |                    0 |
| N/A   32C    P0    50W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   7  Tesla V100-SXM3...  On   | 00000000:5E:00.0 Off |                    0 |
| N/A   35C    P0    52W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   8  Tesla V100-SXM3...  On   | 00000000:B7:00.0 Off |                    0 |
| N/A   30C    P0    49W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   9  Tesla V100-SXM3...  On   | 00000000:B9:00.0 Off |                    0 |
| N/A   31C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  10  Tesla V100-SXM3...  On   | 00000000:BC:00.0 Off |                    0 |
| N/A   34C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  11  Tesla V100-SXM3...  On   | 00000000:BE:00.0 Off |                    0 |
| N/A   35C    P0    52W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  12  Tesla V100-SXM3...  On   | 00000000:E0:00.0 Off |                    0 |
| N/A   30C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  13  Tesla V100-SXM3...  On   | 00000000:E2:00.0 Off |                    0 |
| N/A   30C    P0    50W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  14  Tesla V100-SXM3...  On   | 00000000:E5:00.0 Off |                    0 |
| N/A   37C    P0    50W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|  15  Tesla V100-SXM3...  On   | 00000000:E7:00.0 Off |                    0 |
| N/A   35C    P0    51W / 350W |      0MiB / 32480MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+
```

2. List available docker images:
```bash
docker images
```
```bash
sigurdkb@cair-gpu04:~/cair-gpu$ docker images
REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
nvcr.io/uiatekreal/cair     latest              85fda4a62ad5        21 hours ago        4.59GB
nvcr.io/nvidia/tensorflow   18.10-py3           18ada165593c        11 days ago         4.57GB
ubuntu                      latest              ea4c82dcd15a        2 weeks ago         85.8MB
busybox                     latest              59788edf1f3e        4 weeks ago         1.15MB
nvcr.io/nvidia/cuda         latest              f072016d63a4        4 weeks ago         2.24GB
nvcr.io/nvidia/cuda         9.2-devel           07a948073127        4 weeks ago         2.28GB
nvcr.io/nvidia/tensorflow   18.07-py3           8289b0a3b285        4 months ago        3.34GB
```

3. Run a container:
```bash
docker run -it --rm --runtime=nvidia --name sigurdkb nvcr.io/uiatekreal/cair
  -it    ->    Run interactively
  --rm   ->    Delete the container when finished (should always be used to avoid cluttering the server with dead containers)
  --name ->    Arbitrary name to identify the container (should be your username)
```
```bash
sigurdkb@cair-gpu04:~/cair-gpu$ docker run -it --rm --runtime=nvidia --name sigurdkb nvcr.io/uiatekreal/cair

================
== TensorFlow ==
================

NVIDIA Release 18.10 (build 785222)

Container image Copyright (c) 2018, NVIDIA CORPORATION.  All rights reserved.
Copyright 2017 The TensorFlow Authors.  All rights reserved.

Various files include modifications (c) NVIDIA CORPORATION.  All rights reserved.
NVIDIA modifications are covered by the license terms that apply to the underlying project or file.

NOTE: Detected MOFED driver 4.4-2.0.7; attempting to automatically upgrade.

(Reading database ... 16727 files and directories currently installed.)
Preparing to unpack .../ibverbs-utils_41mlnx1-OFED.4.4.2.0.1.44207_amd64.deb ...
Unpacking ibverbs-utils (41mlnx1-OFED.4.4.2.0.1.44207) over (1.2.1mlnx1-OFED.4.0.0.1.3.40101) ...
Preparing to unpack .../libibverbs-dev_41mlnx1-OFED.4.4.2.0.1.44207_amd64.deb ...
Unpacking libibverbs-dev (41mlnx1-OFED.4.4.2.0.1.44207) over (1.2.1mlnx1-OFED.4.0.0.1.3.40101) ...
Preparing to unpack .../libibverbs1_41mlnx1-OFED.4.4.2.0.1.44207_amd64.deb ...
Unpacking libibverbs1 (41mlnx1-OFED.4.4.2.0.1.44207) over (1.2.1mlnx1-OFED.4.0.0.1.3.40101) ...
Preparing to unpack .../libmlx5-1_41mlnx1-OFED.4.4.2.0.1.44207_amd64.deb ...
Unpacking libmlx5-1 (41mlnx1-OFED.4.4.2.0.1.44207) over (1.2.1mlnx1-OFED.4.0.0.1.1.40101) ...
Setting up libibverbs1 (41mlnx1-OFED.4.4.2.0.1.44207) ...
Setting up libmlx5-1 (41mlnx1-OFED.4.4.2.0.1.44207) ...
Setting up ibverbs-utils (41mlnx1-OFED.4.4.2.0.1.44207) ...
Setting up libibverbs-dev (41mlnx1-OFED.4.4.2.0.1.44207) ...
Processing triggers for libc-bin (2.23-0ubuntu10) ...

root@e3324070677e:/workspace#            
```

