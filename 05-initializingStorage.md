# Initializing storage

Find storage name either from the server with `lsblk`; 
~~~
ubuntu@3d-build:~$ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda       8:0    0   10G  0 disk 
|-sda1    8:1    0  9.9G  0 part /
|-sda14   8:14   0    4M  0 part 
`-sda15   8:15   0  106M  0 part /boot/efi
sdb       8:16   0   10G  0 disk 
~~~

Or via `openstack volume list`.

For `lsblk` the last line is the important one. 
Lets make a file system on that storage (important - do this ONLY ONCE!). 

~~~
ubuntu@3d-build:~$ sudo mkfs.ext4 /dev/sdb
mke2fs 1.43.5 (04-Aug-2017)
Discarding device blocks: done                            
Creating filesystem with 2621440 4k blocks and 655360 inodes
Filesystem UUID: b95fd2ba-6922-41bd-b149-20babb64191b
Superblock backups stored on blocks: 
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632

Allocating group tables: done                            
Writing inode tables: done                            
Creating journal (16384 blocks): done
Writing superblocks and filesystem accounting information: done 
~~~

Now we have a file system, but we cannot see it (try e.g. `df`). We must mount it:

~~~
ubuntu@3d-build:~$ sudo mkdir -p /testVolum
ubuntu@3d-build:~$ sudo mount /dev/sdb /testVolum
ubuntu@3d-build:~$ df
Filesystem     1K-blocks    Used Available Use% Mounted on
udev             1012480       0   1012480   0% /dev
tmpfs             204164   21052    183112  11% /run
/dev/sda1        9983232 1340704   8626144  14% /
tmpfs            1020808       0   1020808   0% /dev/shm
tmpfs               5120       0      5120   0% /run/lock
tmpfs            1020808       0   1020808   0% /sys/fs/cgroup
/dev/sda15        106858    3405    103454   4% /boot/efi
tmpfs             204160       0    204160   0% /run/user/1000
/dev/sdb        10255636   36888   9678076   1% /testVolum
ubuntu@3d-build:~$ df -h /testVolum
Filesystem      Size  Used Avail Use% Mounted on
/dev/sdb        9.8G   37M  9.3G   1% /testVolum
~~~

Your file area is ready for use. 

After unmounting, the file area can later be detached:

	umount /testVolum

	openstack server remove volume 3d-build mittTestVolum
