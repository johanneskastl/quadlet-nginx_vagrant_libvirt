# Vagrant setup for running nginx via quadlet

This setup prepares on CentOS9 Stream VM and then runs
an Ansible playbook, inspired by ygalblum's
[quadlet-demo](https://github.com/ygalblum/quadlet-demo).

This will install Podman on the VM and then configure
things using Quadlet, so in the end there is a Nginx
container listening on port 8080.

To reach the container from the machine running vagrant
you need to find out the Vagrant VM's IP address, e.g.
by using the vagrant address plugin or roaming through
the Ansible inventory file in
`.vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory`.

Then run a simple `curl IP:8080` and you get the
default NGINX page. Hooray!

## Vagrant

1. You need vagrant obviously. And Ansible.
2. Fetch the box, per default this is `generic/centos9s`, using `vagrant box add generic/centos9s`.
3. Make sure the git submodules are fully working by issuing `git submodule init && git submodule update`
4. Run `vagrant up`
5. Run a curl command against the VM's IP address on port 8080.
6. Party!

## Disabling the Ansible provisioning

In case you do not want Ansible to setup Podman (because you want to install it yourself), just comment out the following lines in the `Vagrantfile`:
```
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision
```
