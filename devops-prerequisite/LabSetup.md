## Virtual box ->

1. virtualisation softwares or hypervisors
2. `VMware ESX servers` are used for running and managing virtual machines in a virtualized environment. These are called type-1 hypervisors. These are directly installed on bare metal(laptop or server) and then VMs are created on that
3. These are used in production environment where we need to create and manage large number of virtual machines and these hypervisors have high resource requirements. They also need to be installed and configured directly on the laptop and they are expensive
4. SO if we have system with high resources we can use it.
5. `type 2 hypervisors` -> These run on existing OS like oracle virtual box and VMware work station, with we can start working with virtual machine easily without installing any other OS or reimage our laptop
6. `type-1 hypervisors` -> baremetal(server) -> hypervisor -> OS -> VMs
7. `type-2 hypervisors` -> baremetal(server) -> OS -> hypervisor -> VMs
8. We can manage resources by allocating only required resources to VM and using lightweight image of OS instead of full blown OS Image
9. The VM itself and the disc of VM are stored as a file on the host OS
10. In new machine hard disks are blank so there is no OS on it, so you need to install an OS on it using OS CD. SO just like we install OS on a laptop we will install it in VM
11. But we will use disk with preconfigured and prebuilt OS. SO when the VM boots it will have the OS. We don't have to manually install the OS
12. these disks or images are there on internet on websites like OSboxes.org. They have list of images for all kind of OS. Once the image is downloaded use it as virtual hard disk file while creating VM

## Install Virtual box and create VM template -> watch video again

## Virtual box connectivity, connecting to VM -> watch video again

1. We created the centOS image on our host system
2. NAT privat IP not accessed by public
3. but with Network Address Translation these VM can reach the outer world
4. since the guest doesn't have an IP we will do `port forwarding`
5. We will forward port on our localhost to port on VM
6. we cannot forward 22 on our hosts to VM, so we will configure another port 2222 on our host to forward to port 22 on VM

## Virtual box networking -> 

1. `host only network` -> VMs are on internal private network, all VMs can see each other but cannot connect to outside world. SO we will do IP forwarding, and doing `IP forwarding` makes our laptop as a router. THe other way is we can create another adapter and attach it to NAT

2. we can create multiple host only networks `????`
3. With NAT(network address translation) VMs can talk to outer world
4. NAT Is a default setting of a VM in a virtual box, VMs were in network of NAT router
5. in NAT network, each VM is isolated and given its own NAT router
6. But both in NAT and NAT nework external host cannot access VMs
7. We don't need to create `bridge nework` like we created `host-only network` and `NAT network`. Bridge network is an extension of LAN network, so bridge network is always there
8. with `NAT` VMs can reach internet if host is connected to internet. host acts as a gateway, sending traffic from the VMs to the Internet and vice versa
9.  a `switch` is often connected to a `router`. The router serves as the `gateway` to the `Internet`, while the switch connects devices to the router, allowing them to access the Internet
10. SO to debug network connectivity issues -> `no. of interfaces configured on VM `,`what type of network they are attached to`, `check if those interfaces have IP assigned`, `apply common sense why we did not reach the internet`
11. `port forwarding` -> allows us to map a port on the host to a port on the guest. SO any traffic that comes on port 80 on host is forwarded on port 80 on guest
12. sending response from VM to external hosts `????`
13. ssh from host to guest. But if we don't know IP address of VM , we can map port 22 of guest to port 2222 on host and then when we do ssh 127.0.0.1 -p 2222, it will connect to VM . port 22 because for ssh connection
14. This way we can have multiple VM and multiple services running on them and `you can map those services to port on the host`
15. this port forwarding is done in VM network settings
15. TCP protocol for port forwarding `????` and do we need to specify the `protocol` too 

## Creat multiple VMs and networking between them -> 

1. create multiple VM -> clone existing VM
2. full clone -> creates full copy of disk used by existing VM, consuming equal amount of new space
3. linked clone -> use disk of existing VM and only consumes space for the changes made in the new VM 
4. But when you move VM from one system to another in case of linked clone, you will have to copy disk of the original VM also
5. If you don't plan to copy your VM then `linked clone` is a good option
6. ALl the settings gets cloned
7. `host only network`, `NAT` 
8. with `host only network`, no need to port forward, ssh from host to guest. Guest cannot reach outside internet
9. `demo: multiple vm and networking` -> `time 7:23` for networking chart
10. `snapshot` -> create backup of your VM's state at a particular point in time and then restore to that backup in a later point in time. Useful when testing different software and functionality on VM like making a major change to VM like upgrading verison of software or package
11. restore the snapshot state and then detachable start the VM
12. Can also clone new VM from snapshot, same process we followed earlier


## Vagrant -> 

1. vagrant init ubuntu
2. vagrant up
3. vagrant -> lists all available commands and options
4. if vagrant file is changed then `vagrant reload` to reload the VM
5. vagrant ssh -> ssh into the VM, vagrant will identify the port configured for port forwarding and use that to ssh
6. vagrant also sets up ssh key based auth
7. we can customize the VM in vagrantfile, and share file to others and VM will boot up the same way with same configurations for everyone
8. In file we can configure directory sync b/w host and guest, so we can easily move files from host to VM
9. can configure CPU and memory, can do that in the provider virtual box block
10. can configure a shell script to run at bootup with shell provision block
11. we can include multiple VMs in this. Automated the deployment of complex environment such as clusters of popular systems
12. there are boxes that have automated clusters such as kubernetes clusters which has multiple VMs
13. we can also use vagrant in VMware environemnt such as VMware workstation and VMware fusion, microsoft huper-V environment
14. so easily create and deploy virtual machines / local lab env and save all the work we did in configuration in vagrantfile