# kub-er - > is who work by kubernetes.

Thera is a simple ansible playbook just to initail and install **K8S**. This is just a Lab excersise and not production.

### Before start

 * Some Virtualization hypervisor such as KVM, Virtualbox etc...
 * Three Virtual machins
   - CPU: 2
   - RAM: 2
   - HDD: 20G
 * OS: Debian 9 [(Stretch)](https://shgn.ir/images/debian-9.13.0-amd64-xfce-CD-1.iso)
 
 ### How to do it!
 
 It is so simple, Just clone the repo, install ansible and play with it:
 
      ansible-playbook -i hosts  main.yml
 
 Of course! You need and inventory file for ansible:
 
    [masters]
    master ansible_host=192.168.2.48 ansible_user=root

    [workers]
    worker1 ansible_host=192.168.22.143 ansible_user=root
    worker2 ansible_host=192.168.22.147 ansible_user=root

    [all:vars]
    ansible_python_interpreter=/usr/bin/python3
    
### Adding new worker to cluster

Just add the new VM info to inventory file:

    [masters]
    master ansible_host=192.168.2.48 ansible_user=root

    [workers]
    worker1 ansible_host=192.168.2.43 ansible_user=root
    worker2 ansible_host=192.168.2.47 ansible_user=root
    worker3 ansible_host=192.168.2.34 ansible_user=root

    [all:vars]
    ansible_python_interpreter=/usr/bin/python3

And then play:

    ansible-playbook -i hosts --tags new-worker main.yml
    
## TODO

This playbook is not complete, so we need these:

 * Handeling Certs
 * Loadbalancer
 * Manage Storage
