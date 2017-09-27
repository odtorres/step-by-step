NFS Configuration 

## Server install
sudo apt-get update
sudo apt-get install nfs-kernel-server

/---
sudo mkdir /var/nfs/general -p
ls -la /var/nfs/general
sudo chown nobody:nogroup /var/nfs/general
ls -la /var/nfs/general
/----
sudo nano /etc/exports
/----
/var/nfs/general    203.0.113.256(rw,sync,no_subtree_check)
/---

sudo systemctl restart nfs-kernel-server


## Client
sudo apt-get update
sudo apt-get install nfs-common

sudo mkdir -p resources

sudo mount -t nfs4 18.220.30.33:/var/nfs/general resources/

df -h