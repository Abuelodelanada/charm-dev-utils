# Charm development utils

A repository to collect initiatives around making the life of a [charm](https://juju.is/docs/sdk) author easier.

<!-- markdown-toc start - Don't edit this section. Run M-x markdown-toc-refresh-toc -->
**Table of Contents**

- [Charm development utils](#charm-development-utils)
  - [cloud-init](#cloud-init)
  - [How to launch a VM using cloud-init script](#how-to-launch-a-vm-using-cloud-init-script)
    - [Using Multipass](#using-multipass)
    - [Using LXD](#using-lxd)
  - [zsh_themes](#zsh_themes)

<!-- markdown-toc end -->


## cloud-init

In the `cloud-init` directory you will find the following cloud-init scripts to launch reusable VMs to everyday charm development:

- `charm-dev-juju-3.6.yaml`


These script will create a VM with:

- [juju](https://juju.is) (stable `3.6`)
- [Canonical Kubernetes](https://snapcraft.io/k8s) 1.35-classic/stable
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [just](https://github.com/casey/just)
- [goss + kgoss](https://github.com/goss-org/goss)



## How to launch a VM using cloud-init script

### Using Multipass

Let's say you need to launch a VM using [Multipass](https://multipass.run/) that runs `juju 3.6/stable` with:

- 4G RAM
- 3 CPUs
- 30G disk
- and mounting your `repos` directory inside the ubuntu user home directory
- an IP address provide

you may run:

```shell
multipass launch --cloud-init charm-dev-juju-3.6.yaml \
--timeout 1200 \
--name charm-dev-36 \
--memory 4G \
--cpus 3 \
--disk 30G \
--mount /home/jose/trabajos/canonical/repos:/home/ubuntu/repos \
--network enp1s0
```

Once the VM is ready you will see:

```
Launched: charm-dev-36
Mounted '/home/jose/trabajos/canonical/repos' into 'charm-dev-36:/home/ubuntu/repos'
```

Now you can jump into the new VM:

```shell
multipass shell charm-dev-36
```

```shell
Welcome to Ubuntu 24.04.1 LTS (GNU/Linux 6.8.0-51-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro


Expanded Security Maintenance for Applications is not enabled.

0 updates can be applied immediately.

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


Last login: Thu Jan  9 09:49:25 2025 from 10.169.97.1
╭─ubuntu@charm-dev-36 ~ [lxd:null]
╰─$
```

And voilà, you have a VM with all you need to start developing Charmed Operators!


### Using LXD

Let's say you need to launch a VM using [LXD](https://canonical.com/lxd) that runs `juju 3.6/stable` with:

- 4G RAM
- 3 CPUs
- 30G disk
- and mounting your `repos` directory inside the ubuntu user home directory
- an IP provided by the DHCP present in the host network

you need to run:

```shell
lxc init ubuntu:24.04 charm-dev-36 --vm \
  -c limits.memory=4GB \
  -c limits.cpu=3 \
  -c cloud-init.user-data="$(cat charm-dev-juju-3.6.yaml)" \
  -c environment.LXC_START_COMMAND="/bin/zsh --login -c 'su - ubuntu'" \
  -s default
```

```shell
lxc config device set charm-dev-36 root size=30GB
```

```shell
lxc config device add charm-dev-36 repos disk \
  source=/home/jose/trabajos/canonical/repos \
  path=/home/ubuntu/repos
```

```shell
lxc config device add charm-dev-36 eth0 nic \
  nictype=bridged \
  parent=br-enp1s0
```


```shell
lxc start charm-dev-36
```

Now you can jump into the new VM:

```shell
lxc exec charm-dev-36 -- su ubuntu

╭─ubuntu@charm-dev-36 /root [lxd:null]
╰─$
```
And voilà, you have a VM with all you need to start developing Charmed Operators!



## zsh_themes

In the `zsh_themes` directory you will find a `juju.zsh-theme` that uses the [`juju`](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju) plugin to show a prompt with juju information about controller and model.

![prompt](https://user-images.githubusercontent.com/939888/227611569-23372d45-0963-4e2e-98da-8109e2dcbd8f.png)
