# vagrant-blackarch

[BlackArch Linux][blackarch-linux-full] as a [Vagrant][vagrant] box: all the persistance of bare metal with the convenience of a live USB.

* Uses the [official `ph20/blackarch-full-x86_64` Vagrant box](https://app.vagrantup.com/ph20/boxes/blackarch-full-x86_64) as the base box.
* Mounts the current directory into the VM as a shared folder at `/vagrant/`. Sync more folders at will.
* Vagrant auto-NATs the VM with the host machine: networking should be automagic.

Currently requires [VirtualBox][virtualbox].

## Usage

### Setting Up SSHFS

Install SSHFS support for shared folder `vagrant plugin install vagrant-sshfs`

[Optional] -- If having issues with too many keys in ssh-agent i.e SSHFS mount fails, too many keys in agent
in your ssh-config..

```
Host 127.0.0.1
  AddKeysToAgent no
```

```console
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
...
$ vagrant ssh
vagrant@blackarch:~$ su - root
Password:
root@kali:~#
```

* Line endings of any config files shared to the Vagrant box should have Unix-style/LF line endings.
* VM settings (CPU/RAM allocation, no GUI, etc.) can be changed by modifying the `Vagrantsettings.yaml`.
* The `custom.sh` script can be modified to add packages/custom code.

[blackarch-linux]: https://blackarch.org/
[vagrant]: https://www.vagrantup.com/
[virtualbox]: https://www.virtualbox.org/
