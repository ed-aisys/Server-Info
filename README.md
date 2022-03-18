# cluster-info

- 4U server - PCIe 4.0 (Chassis similar to Gigabyte G482-Z54)
- CPU: 2 x 28 CPU cores (AMD EPYC Zen 3, 7453)
- GPU: 8 x Nvidia A5000 (NVLinked, 4 pairs)
- Memory: 1TB DDR4 3200MHz (16 x 64GB)
- NVMe SSD: 2 x 3.84TB (Intel P5510, PCIe 4.0)
- SATA SSD: 1.92TB (Intel S4510)
- 1 Gbps NIC (Future expansion to have InfiniBand)


## Create User

```bash
sudo useradd -m -G sudo <user name> # user WITH root privileges
sudo useradd -m <user name>         # user WITHOUT root privileges

sudo passwd <user name>             # set user password
```

## Storage

```bash
sudo usermod -aG storage <user name>
```

## Anaconda

Add user to anaconda group

```bash
sudo usermod -aG anaconda3 <user name>
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
export PATH=/usr/local/<cuda version>/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/<cuda version>/lib64:$LD_LIBRARY_PATH
```


