ASSIGNMENT 2

TASK 1 :- Make 5 partitions in your pendrive.
 STEPS  :-
```
                           # sudo mount ( check the mounted device)
                           # sudo fdisk -l (to identify my device)
                           # sudo fdisk /dev/sdb (to make partitions)
```
                           First partition –     n -> p -> 1 -> enter -> +10M (sdb1)
                           Second partition -  n -> p -> 2 -> enter -> +10M (sdb2)
                           Third partition -    n -> p -> 3 -> enter -> +10M (sdb3)
                           Extended part     - n -> e -> enter -> +7G            (sdb4)
                           Fourth partition -  n -> enter -> +50M                (sdb5)
                           Fifth partition -      n -> enter -> +50M                (sdb6)
                                                            w -> (saves the partition on disk) 
```                           
                           # partprobe (save to the kernel)
```












TASK 2 :- Mount those partition.
STEPS   :- 
```
                           # cd /
                           # sudo mkdir mnt1 mnt2 mnt3 mnt4 mnt5 (made the mount points)
                           # sudo mkfs.ext4 /dev/sdb1 (giving file system to 1st partition)
                           # sudo mkfs.ext4 /dev/sdb2 (giving file system to 2ndpartition)
                           # sudo mkfs.ext4 /dev/sdb3 (giving file system to 3rdpartition)
                           # sudo mkfs.ext4 /dev/sdb5 (giving file system to 4thpartition)
                           # sudo mkfs.ext4 /dev/sdb6 (giving file system to 5thpartition)
                           # sudo mount /dev/sdb1 /mnt1
                           # sudo mount /dev/sdb2 /mnt2
                           # sudo mount /dev/sdb3 /mnt3
                           # sudo mount /dev/sdb5 /mnt4
                           # sudo mount /dev/sdb6 /mnt5
```

TASK 3 :- Validate the same by making files in the above and unmount the same and check if you still see the contents.
Steps    :-               
```
                          # cd /mnt1
                          # sudo touch test1
                          # cd /mnt2
                          # sudo touch test2
                          # cd /mnt3
                          # touch test3
                          # cd /mnt4
                          # touch test5
                          # cd /mnt5
                          # touch test6   
                          # sudo umount /dev/sdb1
                          # sudo umount /dev/sdb2
                          # sudo umount /dev/sdb3
                          # sudo umount /dev/sdb5
                          # sudo umount /dev/sdb6
```

TASK 4 :- Delete all the partitions and make a single partition.
Steps    :-  First delete all partitions properly.
```
                 # sudo fdisk /dev/ 
```   
                          First partition ->  d -> 1
                          Second partition ->  d -> 2
                          Third partition ->  d -> 3
                          Extended partition ->  d -> 4
                          Fourth partition ->  d -> 5
                          Fifth partition ->  d -> 6
                          Save changes -> w
```      
                    # sudo parted -a opt /dev/sdb mkpart primary ext4 0% 100%
```   
                          (Created a single partition with whole disk space)
                          


TASK 5 :- Make it a lvm partition -> physical vol -> vol_grp - > logical_vol1.
Steps    :-  
```
                          # sudo lvmdiskscan (scans free disk for lvm partition)
                          # sudo pvcreate /dev/sdb (physical vol created)
                          # sudo pvscan (scans and shows the physical_vol)
```
output :-
  PV /dev/sdb                                               lvm2 [7.23 GiB]
  Total: 1 [7.23 GiB] / in use: 0 [0   ] / in no VG: 1 [7.23 GiB]
                          

```
                          # sudo vgcreate vol_grp /dev/sdb 
                             # sudo vgdisplay
```

output:-
--- Volume group ---
  VG Name               vol_grp
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               7.23 GiB
  PE Size               4.00 MiB
  Total PE              1850
  Alloc PE / Size       0 / 0   
  Free  PE / Size       1850 / 7.23 GiB
  VG UUID               KfqNo2-vlQ6-6bQ4-0UpP-72Pv-LjaY-UooGX2


```
                             # sudo lvcreate -l 256 -n logical_vol1 vol_grp 
```   
 (logical_vol1 created by giving the value in form of extent 256 extent=1gb)
```   
                             # sudo lvdisplay
```
output:-
--- Logical volume ---
  LV Path                /dev/vol_grp/logical_vol1
  LV Name                logical_vol1
  VG Name                vol_grp
  LV UUID                NCDTob-ssYC-0vo7-yOKv-ni9r-Aotf-a88oWg
  LV Write Access        read/write
  LV Creation host, time dell-Inspiron-3542, 2018-05-22 16:23:44 +0530
  LV Status              available
  # open                 0
  LV Size                1.00 GiB
  Current LE             256
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           253:0





TASK 6 :- Extend the size to 1.5G and then reduce it to 500M.
Steps    :-  # sudo lvextend -l384 /dev/vol_grp/logical_vol1
                            (we did it by giving 384 extent but we could also given +128 extent)
```   
                       # sudo lvdisplay
```
output:-
--- Logical volume ---
  LV Path                /dev/vol_grp/logical_vol1
  LV Name                logical_vol1
  VG Name                vol_grp
  LV UUID                NCDTob-ssYC-0vo7-yOKv-ni9r-Aotf-a88oWg
  LV Write Access        read/write
  LV Creation host, time dell-Inspiron-3542, 2018-05-22 16:23:44 +0530
  LV Status              available
  # open                 0
  LV Size                1.50 GiB
  Current LE             384
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           253:0
```
                         # sudo lvreduce -L 500M /dev/vol_grp/logical_vol1
                         # sudo lvdisplay
```


output:-
--- Logical volume ---
  LV Path                /dev/vol_grp/logical_vol1
  LV Name                logical_vol1
  VG Name                vol_grp
  LV UUID                NCDTob-ssYC-0vo7-yOKv-ni9r-Aotf-a88oWg
  LV Write Access        read/write
  LV Creation host, time dell-Inspiron-3542, 2018-05-22 16:23:44 +0530
  LV Status              available
  # open                 0
  LV Size                500.00 MiB
  Current LE             125
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     256
  Block device           253:0

```   
                       # sudo resize2fs
```


TASK 7 :- LVM.
Theory  :- 



















1. For adding a new PV we have to use fdisk to create the LVM partition.
=> To Create new partition Press n. 
1. Choose primary partition use p. 
2. Choose which number of partition to be selected to create the primary partition. 
3. Press 1 if any other disk available. 
4. Change the type using t. 
5. Type 8e to change the partition type to Linux LVM. 
6. Use p to print the create partition ( here we have not used the option). 
7. Press w to write the changes. 
Restart the system once completed.
2. Ways to create the logical volumes.
=>  We can create a logical volume either by giving the size directly or also with the help of extent. 1 extent = 4 MiB.
        256 extent = 1024 GiB              
3. What is LVM? Why we need it?
=> LVM is used for the following purposes:
Creating single logical volumes of multiple physical volumes or entire hard disks, allowing for dynamic volume resizing. 
Managing large hard disk farms by allowing disks to be added and replaced without downtime or service disruption. 
On small systems (like a desktop), instead of having to estimate at installation time how big a partition might need to be, LVM allows filesystems to be easily resized as needed. 
Performing consistent backups by taking snapshots of the logical volumes. 
Encrypting multiple physical partitions with one password. 
LVM can be considered as a thin software layer on top of the hard disks and partitions, which creates an abstraction of continuity and ease-of-use for managing hard drive replacement, repartitioning and backup.

TASK 7 :- Shell tasks given by RAJAT_VATS.
1. #!/bin/bash
    char=”2”
    #abc=echo -n $char|wc -c
    if [$char -gt “9” ] && [$char -it “100”]
    then
    echo “double digit”
    else
    if [ $char -it “10” ]
    then
    echo “its single digit”
    else
    echo “invalid code”
    fi
