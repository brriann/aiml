# Nvidia driver update

## torch output
print(f"GPU is available: {torch.cuda.is_available()}")

GPU is available: False

/home/ubuntu/dev/.venvs/torch/lib/python3.10/site-packages/torch/cuda/__init__.py:129: UserWarning: CUDA initialization: The NVIDIA driver on your system is too old (found version 11040). Please update your GPU driver by downloading and installing a new version from the URL: http://www.nvidia.com/Download/index.aspx Alternatively, go to: https://pytorch.org to install a PyTorch version that has been compiled with your version of the CUDA driver. (Triggered internally at /pytorch/c10/cuda/CUDAFunctions.cpp:109.)
  return torch._C._cuda_getDeviceCount() > 0

## pytorch and nvidia GPU info

pytorch==2.6.0

```bash
nvidia-smi -L

>> GPU 0: NVIDIA GeForce RTX 2060 SUPER (UUID: GPU-73a45cb1-6182-6fe2-76a5-3174f029af7e)
```

driver version 570.153.02

https://www.nvidia.com/en-us/drivers/details/245669/


https://documentation.ubuntu.com/server/how-to/graphics/install-nvidia-drivers/index.html

```bash
cat /proc/driver/nvidia/version

>> NVRM version: NVIDIA UNIX x86_64 Kernel Module  470.256.02  Thu May  2 14:37:44 UTC 2024
   GCC version:  gcc version 11.4.0 (Ubuntu 11.4.0-1ubuntu1~22.04) 
```

```bash
sudo ubuntu-drivers list

sudo ubuntu-drivers install
```

## fix network drivers missing after Nvidia driver install

https://ubuntuforums.org/showthread.php?t=2482696

```bash
uname -r
>> 5.15.0-140-generic

sudo dpkg -s linux-modules-extra-$(uname -r) | grep Status

>> not installed
```

reboot
GNU Grub > Ubuntu Advanced Options
choose kernel 5.15.0-139

```bash
sudo apt update
sudo apt install -y linux-modules-extra-5.15.0-140-generic
```

reboot as normal (no GNU GRUB interactions), network drivers restored