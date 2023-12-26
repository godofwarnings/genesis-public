---
{"dg-publish":true,"permalink":"/linux/mounting-drives/"}
---

# Can’t mount secondary HDD
This is the procedure I followed to mount my **WDC 1 TB** hard disk
Checkout [[linux/Manjaro/Can’t mount secondary HDD\|Can’t mount secondary HDD]] for similar issue

## Some useful commands
- To check disk details like manufacturers and such, I used `lsblk` command in the following way
```bash
lsblk -o NAME,FSTYPE,LABEL,MOUNTPOINT,SIZE,MODEL
```
More information on this [Stackexchange answer](https://unix.stackexchange.com/questions/5085/how-to-see-disk-details-like-manufacturer-in-linux)

## Resources used
- Arch Wiki
- [Linux Fstab options](https://linuxopsys.com/topics/linux-fstab-options)
- [Auto mount drives in linux](https://www.techhut.tv/auto-mount-drives-in-linux-fstab/)

## Procedure
### Step 1 - Getting the Name, UUID and File System Type of the partition
1. run `blkid` command
```bash
sudo blkid
```
this was the output
![Pasted image 20231226191826.png](/img/user/linux/attachments/Pasted%20image%2020231226191826.png)
2. My drive of interest is `/dev/nvme1n1p2`. So I noted down the UUID and its filetype (ntfs)
### Step 2: Making an entry point/mount point for the partition
Since I use primarily use this partition in windows to install windows software, I made the following entry point in `/mnt`
```bash
sudo mkdir /mnt/ntfs_1
```
it was easier to remember this name instead of `/mnt/nvme1n1p2`
### Step 3: Editing the fstab file
1. Create a backup of the fstab file
```bash
cp /etc/fstab ~/Documents/linux/backups/
```
2. Open the original file
```bash
sudo nvim /etc/fstab
```
3. At the end of file, add the information corresponding to your drive
![Pasted image 20231226192653.png](/img/user/linux/attachments/Pasted%20image%2020231226192653.png)
line 11 in my case. For more details about the fstab file, check the **Resources Used** section
4. In the end, run
```bash
sudo mount -a
```

