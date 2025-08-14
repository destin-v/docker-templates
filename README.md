<p align="center">
  <a href="https://github.com/destin-v">
    <img src="https://raw.githubusercontent.com/destin-v/destin-v/main/docs/pics/logo.gif" alt="drawing" width="500"/>
  </a>
</p>

# 📒 Description
<p align="center">
  <img src="docs/pics/program_logo.png" alt="drawing" width="300"/>
</p>

<p align="center">
  <a href="https://github.com/pre-commit/pre-commit">             <img alt="" src="https://img.shields.io/badge/pre--commit-enabled-blue?logo=pre-commit"></a>
  <a href="https://sphinx-book-theme.readthedocs.io/en/stable/">  <img alt="" src="https://img.shields.io/badge/Sphinx-^1.1.2-blue?logo=sphinx&logoColor=white"></a>
</p>

<p align="center">
  <a href="https://docs.github.com/en/actions/quickstart">                          <img alt="" src="https://img.shields.io/badge/CI-github-brightgreen?logo=github&logoColor=white"></a>
</p>

Development templates for Docker or Podman containers.  Use these as a starting point for developing applications.

# 🐳 Docker
Install the **Nvidia Container Tool Kit** (CTK) in order to run GPUs inside its containers.
 
 ```bash
 # This needs to be redone every time your Nvidia drivers update.
 sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml      # Generate configuration for Nvidia CTK
 nvidia-ctk cdi list                                             # Ensure you can see all GPUs.
 ```

Install Docker and start running.

```bash
brew install colima # docker virtual machine engine
brew install docker # docker latest
```

Run a test:

```bash
colima start # start the virtual machine
docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```

You should see the following:
```bash
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 535.86.10    Driver Version: 535.86.10    CUDA Version: 12.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   34C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
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
# 🫛 Podman
Install the **Nvidia Container Tool Kit** (CTK) in order to run GPUs inside its containers.
 
 ```bash
 # This needs to be redone every time your Nvidia drivers update.
 sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml      # Generate configuration for Nvidia CTK
 nvidia-ctk cdi list                                             # Ensure you can see all GPUs.
 ```
 
 The official Ubuntu apt package manager uses an older version of Podman.  Use Homebrew if you want the latest.
 
 ```bash
 # To get the latest version of Podman, use Homebrew.
 brew install podman
 ```
 
 Test Podman with a GPU enabled hello-world.
 ```bash
 # Test container with Nvidia hello-world
 $ sudo podman run --rm --device nvidia.com/gpu=all nvidia/cuda:11.0.3-base-ubuntu20.04 nvidia-smi
 ```

 You will see the following:

 ```bash
 +-----------------------------------------------------------------------------+
| NVIDIA-SMI 535.86.10    Driver Version: 535.86.10    CUDA Version: 12.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Tesla T4            On   | 00000000:00:1E.0 Off |                    0 |
| N/A   34C    P8     9W /  70W |      0MiB / 15109MiB |      0%      Default |
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

# 🛠️ Troubleshooting

If you get an error like this:

```bash
Error: crun: cannot stat `/usr/lib/x86_64-linux-gnu/libEGL_nvidia.so.550.144.03`: No such file or directory: OCI runtime     attempted to invoke a command that was not found
```

It means Docker/Podman needs a CDI update:

```bash
sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
```

# 📑 References
* https://podman-desktop.io/docs/podman/gpu
* https://github.com/NVIDIA/nvidia-container-toolkit/issues/450
* https://gist.github.com/jabbany/66e633c3fd30f81159feb46e4da25c55