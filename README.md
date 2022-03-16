# cluster-info

## Create User

```bash
sudo useradd -m -G sudo <user name> # user WITH root privileges
sudo useradd -m <user name>         # user WITHOUT root privileges

sudo passwd <user name>             # set user password
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
