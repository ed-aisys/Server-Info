# cluster-info

- 4U server - PCIe 4.0 (Chassis similar to Gigabyte G482-Z54)
- CPU: 2 x 28 CPU cores (AMD EPYC Zen 3, 7453)
- GPU: 8 x Nvidia A5000 (NVLinked, 4 pairs)
- Memory: 1TB DDR4 3200MHz (16 x 64GB)
- NVMe SSD: 2 x 3.84TB (Intel P5510, PCIe 4.0)
- SATA SSD: 1.92TB (Intel S4510)
- 1 Gbps NIC (Future expansion to have InfiniBand)

![G482-Z54](https://www.gigabyte.com/FileUpload/Global/Microsite/547/innergigabyteimages/G482-Z54_BlockDiagram_.png)

**IMPORTANT**: The server can only be accessed within Informatics firewall through Ethernet cables in side building or proxy jump through `ssh.inf.ed.ac.uk`

## Create User

```bash
sudo useradd -m -s /usr/bin/bash -G sudo <username> # user WITH root privileges
sudo useradd -m -s /usr/bin/bash <username>         # user WITHOUT root privileges

sudo passwd <username>             # set user password
```

After the default passward is set for users, they can login and change their own password by `passwd`

## Storage

```bash
sudo usermod -aG storage <username>
```

**IMPORTANT**: Home directory is only for downloads, compilation. Put data on NVMe SSD under `/mnt/raid0nvme1`

## Remote Access

For users want to have ssh access by public/private key pair
```bash
ssh-copy-id <username>@gala1   # execute on local machine with key pair
ssh <username>@gala1
```

## Anaconda

Add user to anaconda group

```bash
sudo usermod -aG anaconda3 <username>
```

Add the following to .bashrc or .zshrc
```bash
# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/gala1/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/gala1/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/gala1/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/gala1/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<
```

## CUDA

```bash
export CUDA_HOME=/usr/local/<cuda version>
export PATH=${CUDA_HOME}/bin:$PATH
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
```


