# Charm development utils

A repository to collect initiatives around making the life of a [charm](https://juju.is/docs/sdk) author easier.

## cloud-init

In the `cloud-init` directory you will find some cloud-init scripts to launch reusable VMs to everyday charm development.


### `charm-dev-juju-3.1.yaml`

This script will create a VM with:

- [juju](https://juju.is) stable 3.1
- [microk8s](https://juju.is/docs/sdk) 1.26-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [Scenario `snapshot` cli tool](https://github.com/canonical/ops-scenario#snapshot).


### `charm-dev-juju-3.0.yaml`

This script will create a VM with:

- [juju](https://juju.is) stable 3.0
- [microk8s](https://juju.is/docs/sdk) 1.26-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [Scenario `snapshot` cli tool](https://github.com/canonical/ops-scenario#snapshot).


### `charm-dev-juju-2.9.yaml`

This script will create a VM with:

- juju stable 2.9
- microk8s 1.26-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [Scenario `snapshot` cli tool](https://github.com/canonical/ops-scenario#snapshot).


### `charm-dev-juju-latest-edge.yaml`

This script will create a VM with:

- [juju](https://juju.is) latest/edge
- microk8s 1.26-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [Scenario `snapshot` cli tool](https://github.com/canonical/ops-scenario#snapshot).



## How to launch a VM using cloud-init script

Let's say you need to launch a VM using [Multipass](https://multipass.run/) that runs `juju 3.0/stable` with:

- 4G RAM
- 3 CPUs
- 30G disk
- and mounting your `repos` directory inside the ubuntu user home directory

you may run:

```shell
multipass launch --cloud-init charm-dev-juju-3.0.yaml \
--timeout 1200 \
--name charm-dev-juju-3 \
--memory 4G \
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

```shell
multipass shell charm-dev-juju-3
```

```shell
Welcome to Ubuntu 22.04.2 LTS (GNU/Linux 5.15.0-67-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage


 * Introducing Expanded Security Maintenance for Applications.
   Receive updates to over 25,000 software packages with your
   Ubuntu Pro subscription. Free for personal use.

     https://ubuntu.com/pro

Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


Last login: Fri Mar 24 15:40:53 2023 from 192.168.122.1
╭─ubuntu@charm-dev-juju-29 ~ [microk8s:controller]
╰─$
```

And voilà, you have a VM with all you need to start developing Charmed Operators!


## zsh_themes

In the `zsh_themes` directory you will find a `juju.zsh-theme` that uses the [`juju`](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju) plugin to show a prompt with juju information about controller and model.

![prompt](https://user-images.githubusercontent.com/939888/227611569-23372d45-0963-4e2e-98da-8109e2dcbd8f.png)
