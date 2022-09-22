### MASTER

#### 1. Config network device in virtual box
```shell
#Adapter1:
Bridge Adapter
#Adapter2:
NAT
#IPV4
Adress: 192.168.10.2 
Network: 255.255.255.0
Gateway: 192.168.10.1
```
#### 2. Setup protocol
```shell
a) sudo nano /etc/hosts:
+ 192.168.10.2 master
+ 192.168.10.3 slave
b) setup server: sudo apt-get install nfs-server
c) create workspace mirror
+ sudo mkdir /mirror
+ echo "/mirror *(rw,sync)" | sudo tee -a /etc/exports
+ sudo service nfs-kernel-server restart
+ sudo touch /mirror/sampleFileForMySlaves
```

#### 3. Setup MPI 
```shell
+ sudo apt-get install openssh-server
+ sudo adduser --home /mirror --uid 1100 mpi
+ su - mpi
+ ssh-keygen -t rsa
+ cd .ssh & cat id_rsa.pub >> authorized_keys
```

#### 4. Install other package
```shell
+ build-in other terminal
+ sudo apt-get install build-essential
+ sudo apt-get install mpich
```

#### 5. Copy file and nano port
```shell
#nano machinefile
192.168.10.2:4
192.168.10.3:4
#copyfile C or C++ to handle#include <stdio.h>
```
#### 6. Build and run file
```shell
mpicc mpi_hello.c -o mpi_hello
mpiexec -n 8 -f machinefile ./mpi_hello
```