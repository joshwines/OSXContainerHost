OSXContainerHost
================

A Vagrant provisioned VM to run Docker containers in.

## Prerequisites

* Vagrant
* Vagrant BindFS
	* `$ vagrant plugin install vagrant-bindfs`
* VirtualBox
* Ansible

## Usage

```
$ git clone git@github.com:joshwines/OSXContainerHost.git
$ vagrant up
$ vagrant ssh
```

Run your docker/fig commands.

#### NFS Share
By default your entire /Users directory is shared via NFS to /Users on the guest. Note: the host NFS config only allows the guest to mount this share. Feel free to change this as you require in the `Vagrantfile`. Once ssh'd into the VM you can run your fig commands from within. For ease I set up a symlink to my workspace folder in the home directory. Do with it as you please.
```
$ ln -s /Users/{username}/workspace ~/workspace
```

## Things to be wary of

* NFS is configured to map all activity in `/Users/` to the uid and gid you run Vagrant as. This will also affect volumes in containers if they are mounted from the `/Users/` folder (which I imagine most will be...). Realistically, for most use-cases this shouldn't be a problem, but it is something to be aware of. Please suggest a better solution if there is one.
* Docker containers are created inside the VM, the images are downloaded inside the VM. Everything happens in there; therefore, if you remove and recreate the VM you will lose all of your existing containers.
