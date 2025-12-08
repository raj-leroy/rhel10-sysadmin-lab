# 06 – Storage and LVM

This section demonstrates adding a new disk to a RHEL system and configuring Logical Volume Management (LVM).

## Identifying the New Disk

Available block devices were reviewed:

lsblk  

The new disk appeared as a secondary device with no partitions (example: /dev/sdb).

## Creating the Physical Volume

The new disk was initialized as a physical volume:

sudo pvcreate /dev/sdb  

Verification:

sudo pvs  

## Creating a Volume Group

A new volume group was created:

sudo vgcreate vg_data /dev/sdb  

Verification:

sudo vgs  

## Creating a Logical Volume

A 5G logical volume was created:

sudo lvcreate -L 5G -n lv_data vg_data  

Verification:

sudo lvs  

## Formatting and Mounting the Logical Volume

The logical volume was formatted with XFS:

sudo mkfs.xfs /dev/vg_data/lv_data  

A mount point was created and the volume mounted:

sudo mkdir -p /data  
sudo mount /dev/vg_data/lv_data /data  

Verification:

df -h | grep /data  

## Persisting the Mount Across Reboots

The UUID of the logical volume was retrieved:

sudo blkid /dev/vg_data/lv_data  

The following entry was added to /etc/fstab:

UUID=<REPLACE_WITH_YOUR_UUID> /data xfs defaults 0 0  

Verification:

sudo mount -a  
df -h | grep /data  

This confirms the LVM volume will mount automatically on system boot.

