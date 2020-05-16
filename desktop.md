# Notebook Setup

## Download CentOS 8 and Install

1. Get ISO File To boot [http://mirror01.idc.hinet.net/CentOS/8-stream/isos/x86_64/CentOS-Stream-8-x86_64-20191219-boot.iso](http://mirror01.idc.hinet.net/CentOS/8-stream/isos/x86_64/CentOS-Stream-8-x86_64-20191219-boot.iso)
2. With Rufus to prepare a usb boot disk.
3. boot from USB thumb disk.
4. setup LAN.
5. setup Network Install URL [http://mirror01.idc.hinet.net/CentOS/8-stream/BaseOS/x86_64/os/](http://mirror01.idc.hinet.net/CentOS/8-stream/BaseOS/x86_64/os/)
6. Server With GUI


## Initial Config

### 1. Create a common user

```

```

### 2. Setup Openssh-server

```
sudo sed -i '46s/no/yes/' /etc/ssh/sshd_config 
```

### 3. Add Addtional Repositories

```
sudo yum -y install epel-release
```

### 4. install KVM

```
sudo yum -y install qemu-kvm libvirt virt-install
sudo systemctl enable --now libvirtd
sudo yum -y install virt-manager 
```

### 5. setup LAB

```
cd /var/lib/libvirt/images/
wget http://mirror01.idc.hinet.net/CentOS/8-stream/isos/x86_64/CentOS-Stream-8-x86_64-20191219-boot.iso
# Create LAB VM
sudo qemu-img create -f qcow2 workstation.qcow2 80G
sudo qemu-img create -f qcow2  server.qcow2 20G

# create over lay file from QCOW2
sudo qemu-img create -b server.qcow2 -f qcow2 servera.ovl
sudo qemu-img create -b server.qcow2 -f qcow2 serverb.ovl
sudo qemu-img create -b server.qcow2 -f qcow2 serverc.ovl
sudo qemu-img create -b server.qcow2 -f qcow2 serverd.ovl

# NTFS Support
sudo yum -y install epel-release ntfs-3g ntfsprogs

```
