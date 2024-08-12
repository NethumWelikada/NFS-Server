**NFS Server Configuration**

#Installing NFS client on CentOS
sudo yum install nfs-utils

#Create a directory to serve as the mount point for the remote NFS share:
sudo mkdir /var/backups

#Check NFS Service Status
systemctl status nfs-server

#Start NFS Service
systemctl start nfs-server   # For systemd-based systems (e.g., Ubuntu, CentOS 7+)
service nfs-server start 	 # For systemd-based systems (e.g., Ubuntu, CentOS 7+)

#Enable NFS Service
systemctl enable nfs-server

#Set up a mount point for the remote NFS share:
sudo mkdir /var/backups

#Open the /etc/fstab
cd /etc >>> vi fstab

#Edit fstab with this
/etc/fstab

# <file system>     <dir>       <type>   <options>   <dump>	<pass>
NFS Server IP:/backups /var/backups  nfs      defaults    0       0

#Alow Primary Server IP
sudo iptables -A INPUT -s Primary Server IP -j ACCEPT

#On the NFS server, Edit the the file /etc/exports
/backups Primary Server IP(rw,sync,no_subtree_check)

**Primary Server Configurations**

#Allow NFS Server IP
sudo iptables -A INPUT -s NFS Server IP -j ACCEPT

#Mount NFS Server
sudo mount -t nfs NFS Server IP:/backups /var/backups
