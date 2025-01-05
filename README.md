# what is NFS
The Network File System (NFS) is a mechanism for storing files on a network. It is a distributed file system that allows users to access files and directories located on remote computers and treat those files and directories as if they were local


1.NFS server installation and configuration

[for sever]

1.Update the System:

 Update the System && sudo apt upgrade -y

2.Install NFS Server

 sudo apt install nfs-kernel-server -y

3.create diretory whih you want to share with others 

 sudo mkdir -p /mnt/nfs_share

4.Set appropriate permissions (modify as needed)

 sudo chown nobody:nogroup /mnt/nfs_share
 sudo chmod 777 /mnt/nfs_share

5.Configure the Exported Directory

 sudo vim  /etc/exports

6.Add the following line to export the directory

 /mnt/nfs_share *(rw,sync,no_subtree_check)

 rw: Stands for Read/Write.
 sync: Requires changes to be written to the disk before they are applied.
 No_subtree_check: Eliminates subtree checking

7.Apply the Configuration

 sudo exportfs -a

8.Restart the NFS serve

 sudo systemctl restart nfs-kernel-server

[for clint]

9.Install NFS Client (on Client Machine)

 sudo apt install nfs-common -y

10.Mount the NFS Share (on Client Machine)

 sudo mkdir -p /mnt/nfs_client

11.Mount the NFS share

 sudo mount <server-ip>:/mnt/nfs_share /mnt/nfs_client

13.Check mounted shares on the client
 
 df -h

sudo showmount -e serverip

14.How to know if the port is running

  sudo netstat -tuln | grep 2049
  suod netstat -tuln | grep 111



