# User Management

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

For non-sudoers, do the following instead

```bash
sudo mkdir /mnt/raid0nvme1/<username>
sudo chown <username>:<username> /mnt/raid0nvme1/<username>
```

**IMPORTANT**: Home directory is only for downloads, compilation. Put data on NVMe SSD under `/mnt/raid0nvme1`

## Remote Access

For users want to have ssh access by public/private key pair

```bash
ssh-copy-id <username>@gala1   # execute on local machine with key pair
ssh <username>@gala1
```

## Software Stack

Add user to anaconda group

```bash
sudo usermod -aG anaconda3 <username>
sudo usermod -aG docker <username>      # docker access
sudo usermod -aG microk8s <username>    # standalone k8s accress
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


```bash
sudo usermod -aG gurobi <username>

export GUROBI_HOME="/home/gala1/gurobi951/linux64"
export PATH="${PATH}:${GUROBI_HOME}/bin"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
```


## CUDA

```bash
export CUDA_HOME=/usr/local/<cuda version>
export PATH=${CUDA_HOME}/bin:$PATH
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
```

## Disks

(Thu 31 Aug 2023 05:21:42 PM BST)

```text
/dev/sda3       1.8T  1.2T  491G  71% /
/dev/md0        7.0T  4.7T  2.0T  72% /mnt/raid0nvme1
/dev/sdb1       3.6T  2.7T  737G  79% /mnt/data
/dev/md1         15T  4.7T  9.8T  33% /mnt/raid0sata1
...
```

Please do not download dataset directly to /home directory.