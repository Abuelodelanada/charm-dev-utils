# Charm development utils

A repository to collect initiatives around making the life of a [charm](https://juju.is/docs/sdk) author easy.

## cloud-init

In the `cloud-init` directory you will find some cloud-init scripts to launch reusable VMs to everyday charm development.



### `charm-dev-juju-3.0.yaml`

This script will create a VM with:

- [juju](https://juju.is) stable 3.0
- [microk8s](https://juju.is/docs/sdk) 1.25-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [bira theme](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes#bira) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - juju
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.


### `charm-dev-juju-2.9.yaml`

This script will create a VM with:

- juju stable 3.0
- microk8s 1.25-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [bira theme](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes#bira) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - juju
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.


### `charm-dev-juju-latest-edge.yaml`

This script will create a VM with:

- juju latest/edge
- microk8s 1.25-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [bira theme](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes#bira) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - juju
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.



## How to launch a VM using cloud-init script

Let's say you need to launch a VM using [Multipass](https://multipass.run/) that runs `juju 3.0/stable` with:

- 4G RAM
- 3 CPUs
- 30G disk
- and mounting your `repos` directory inside the ubuntu user home directory

you may run:

```
multipass launch --cloud-init charm-dev-juju-3.0.yaml \
--timeout 1200 \
--name charm-dev-juju-3 \
--mem 4G \
--cpus 3 \
--disk 30G \
--mount /home/jose/trabajos/canonical/repos:/home/ubuntu/repos
```

Once the VM is ready you will see:

```
Launched: charm-dev-juju-3
Mounted '/home/jose/trabajos/canonical/repos' into 'charm-dev-juju-3:/home/ubuntu/repos'
```

Now you can jump into the new VM:

```
multipass shell charm-dev-juju-3
```

```
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-52-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


0 updates can be applied immediately.


*** System restart required ***
╭─ubuntu@charm-dev-juju-3 ~
╰─$
```

And voilà, you have a VM with all you need to start developing Charmed Operators!
