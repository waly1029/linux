# Linux 分区
## 1. 只有一个根目录
## 2. 采用一种载入的处理方法

```
[root@192 home]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sr0          11:0    1 1024M  0 rom  
nvme0n1     259:0    0   20G  0 disk 
├─nvme0n1p1 259:1    0  600M  0 part /boot/efi
├─nvme0n1p2 259:2    0    1G  0 part /boot
├─nvme0n1p3 259:3    0 16.4G  0 part /
└─nvme0n1p4 259:4    0    2G  0 part [SWAP]

[root@192 home]# lsblk -f
NAME        FSTYPE FSVER LABEL UUID                                 FSAVAIL FSUSE% MOUNTPOINTS
sr0                                                                                
nvme0n1                                                                            
├─nvme0n1p1 vfat   FAT32       24E8-6E1B                             591.9M     1% /boot/efi
├─nvme0n1p2 ext4   1.0         0e7cb920-aa94-4b4f-9e60-804806a86dad  688.3M    22% /boot
├─nvme0n1p3 ext4   1.0         e93d8b23-556b-46c6-b9cf-61252365ef31    9.1G    38% /
└─nvme0n1p4 swap   1           d23f674e-5aad-4f26-ab30-c1eb6d1f0533                [SWAP]
```
sr0:            光驱
nvme0n1:        分区情况
UUID:           每个分区的唯一标识符40i位
MOUNTPOINTS:    挂载点


## 挂载案例
增加一块硬盘
1. 虚拟机增加
```
[root@192 桌面]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sr0          11:0    1  7.6G  0 rom  /run/media/root/CentOS-Stream-9-BaseOS-aarch64
nvme0n1     259:0    0   20G  0 disk 
├─nvme0n1p1 259:1    0  600M  0 part /boot/efi
├─nvme0n1p2 259:2    0    1G  0 part /boot
├─nvme0n1p3 259:3    0 16.4G  0 part /
└─nvme0n1p4 259:4    0    2G  0 part [SWAP]
nvme0n2     259:5    0   20G  0 disk 
nvme0n3     259:6    0    1G  0 disk
```
2. 分区命令
```
[root@192 桌面]# fdisk /dev/nvme0n3 

欢迎使用 fdisk (util-linux 2.37.4)。
更改将停留在内存中，直到您决定将更改写入磁盘。
使用写入命令前请三思。

设备不包含可识别的分区表。
创建了一个磁盘标识符为 0x8327dc08 的新 DOS 磁盘标签。

命令(输入 m 获取帮助)：n
分区类型
   p   主分区 (0 primary, 0 extended, 4 free)
   e   扩展分区 (逻辑分区容器)
选择 (默认 p)：p
分区号 (1-4, 默认  1): 4
第一个扇区 (2048-2097151, 默认 2048): 
最后一个扇区，+/-sectors 或 +size{K,M,G,T,P} (2048-2097151, 默认 2097151): 

创建了一个新分区 4，类型为“Linux”，大小为 1023 MiB。

命令(输入 m 获取帮助)：w
分区表已调整。
将调用 ioctl() 来重新读分区表。
正在同步磁盘。

[root@192 桌面]# lsblk
NAME        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sr0          11:0    1  7.6G  0 rom  /run/media/root/CentOS-Stream-9-BaseOS-aarch64
nvme0n1     259:0    0   20G  0 disk 
├─nvme0n1p1 259:1    0  600M  0 part /boot/efi
├─nvme0n1p2 259:2    0    1G  0 part /boot
├─nvme0n1p3 259:3    0 16.4G  0 part /
└─nvme0n1p4 259:4    0    2G  0 part [SWAP]
nvme0n2     259:5    0   20G  0 disk 
nvme0n3     259:6    0    1G  0 disk 
└─nvme0n3p4 259:8    0 1023M  0 part
```

3. 格式化已经分区编号的新硬盘
   UUID
```
[root@192 桌面]# mkfs -t ext4 /dev/nvme0n3p4
```

4. 挂载mount
```
[root@192 桌面]# mount /dev/nvme0n3p4 /newdisk/
[root@192 桌面]# lsblk -f
```

5. 卸载umount
```
[root@192 /]# umount /dev/nvme0n3p4 
[root@192 /]# lsblk -f
```
## 用命令行挂在的方式重启以后会失效

6. 永久挂载，自动挂载
```
[root@192 桌面]# vim /etc/fstab
UUID=1be1501c-0ccc-48af-b54e-dc21a41e176a /newdisk                ext4    defaults        0 0
```































