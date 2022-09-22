### Slave

#### 1. Config network device in virtual box
```shell
#Adapter1:
Bridge Adapter
#Adapter2:
NAT
#IPV4
Adress: 192.168.10.3 
Network: 255.255.255.0
Gateway: 192.168.10.1
```
#### 2. Setup protocol
```shell
a) sudo nano /etc/hosts:
+ 192.168.10.2 master
+ 192.168.10.3 slave
b) setup server: sudo apt-get install nfs-client
c) create workspace mirror
+ sudo mkdir /mirror
+ sudo mount master:/mirror /mirror
+ sudo gedit /etc/fstab
+ master:/mirror /mirror nfs
+ echo "master:/mirror    /mirror    nfs" | sudo tee -a /etc/fstab
```

#### 3. Setup MPI 
```shell
+ sudo apt-get install openssh-server
+ sudo adduser --home /mirror --uid 1100 mpi
```

#### 4. Install other package
```shell
+ build-in other terminal
+ sudo apt-get install build-essential
+ sudo apt-get install mpich
```