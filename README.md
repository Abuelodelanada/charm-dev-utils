# Charm development utils

A repository to collect initiatives around making the life of a [charm](https://juju.is/docs/sdk) author easier.

## cloud-init

In the `cloud-init` directory you will find the following cloud-init scripts to launch reusable VMs to everyday charm development:

- `charm-dev-juju-3.4.yaml`
- `charm-dev-juju-3.3.yaml`
- `charm-dev-juju-3.2.yaml`
- `charm-dev-juju-3.1.yaml`
- `charm-dev-juju-2.9.yaml`
- `charm-dev-juju-latest-edge.yaml`



These script will create a VM with:

- [juju](https://juju.is) (stable `3.4`, `3.3`, `3.2`, `3.1`, `2.9` or `latest-edge`)
- [microk8s](https://microk8s.io/) 1.29-strict
- ZSH as a default SHELL with [oh-my-zsh](https://ohmyz.sh/) and [juju theme](https://github.com/Abuelodelanada/charm-dev-utils/blob/main/zsh_themes/juju.zsh-theme) with plugins:
  - [autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
  - [syntax highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
  - [juju](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju)
- [Pietro's](https://github.com/PietroPasotti/) amazing [jhack](https://github.com/PietroPasotti/jhack) tool.
- [Scenario `snapshot` cli tool](https://github.com/canonical/ops-scenario#snapshot).



## How to launch a VM using cloud-init script

Let's say you need to launch a VM using [Multipass](https://multipass.run/) that runs `juju 3.4/stable` with:

- 4G RAM
- 3 CPUs
- 30G disk
- and mounting your `repos` directory inside the ubuntu user home directory

you may run:

```shell
multipass launch --cloud-init charm-dev-juju-3.4.yaml \
--timeout 1200 \
--name charm-dev-juju-34 \
--memory 4G \
--cpus 3 \
--disk 30G \
--mount /home/jose/trabajos/canonical/repos:/home/ubuntu/repos
```

Once the VM is ready you will see:

```
Launched: charm-dev-juju-34
Mounted '/home/jose/trabajos/canonical/repos' into 'charm-dev-juju-34:/home/ubuntu/repos'
```

Now you can jump into the new VM:

```shell
multipass shell charm-dev-juju-34
```

```shell
Welcome to Ubuntu 22.04.4 LTS (GNU/Linux 5.15.0-92-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro

 * Strictly confined Kubernetes makes edge and IoT secure. Learn how MicroK8s
   just raised the bar for easy, resilient and secure K8s cluster deployment.

   https://ubuntu.com/engage/secure-kubernetes-at-the-edge

Expanded Security Maintenance for Applications is not enabled.

8 updates can be applied immediately.
8 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable

Enable ESM Apps to receive additional future security updates.
See https://ubuntu.com/esm or run: sudo pro status


╭─ubuntu@charm-dev-juju-34 ~ [lxd:null]
╰─$ 
```

And voilà, you have a VM with all you need to start developing Charmed Operators!


## zsh_themes

In the `zsh_themes` directory you will find a `juju.zsh-theme` that uses the [`juju`](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/juju) plugin to show a prompt with juju information about controller and model.

![prompt](https://user-images.githubusercontent.com/939888/227611569-23372d45-0963-4e2e-98da-8109e2dcbd8f.png)
