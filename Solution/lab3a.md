# Solution to Lab3a

## Q1

**Who is the developer that created this signature, and what is their key's fingerprint?**

### Answer: 

**Developer: Pierre Schmitz**

**Fingerprint: 3E80 CA1A 8B89 F69C BA57 D98A 76A5 EF90 5444 9A5C**

```
gpg: assuming signed data in 'archlinux-2024.02.01-x86_64.iso'
gpg: Signature made Thu Feb  1 12:10:46 2024 UTC
gpg:                using EDDSA key 3E80CA1A8B89F69CBA57D98A76A5EF9054449A5C
gpg:                issuer "pierre@archlinux.org"
gpg: /root/.gnupg/trustdb.gpg: trustdb created
gpg: key 76A5EF9054449A5C: public key "Pierre Schmitz <pierre@archlinux.org>" imported
gpg: key 7F2D434B9741E8AC: public key "Pierre Schmitz <pierre@archlinux.org>" imported
gpg: Total number processed: 2
gpg:               imported: 2
gpg: no ultimately trusted keys found
gpg: Good signature from "Pierre Schmitz <pierre@archlinux.org>" [unknown]
gpg: WARNING: This key is not certified with a trusted signature!
gpg:          There is no indication that the signature belongs to the owner.
Primary key fingerprint: 3E80 CA1A 8B89 F69C BA57  D98A 76A5 EF90 5444 9A5C
```

## Q2

**What is the current hostname? What is your IP address**

### Answer

**Hostname: arches**

**IP address: 192.168.122.29**

## Q3

**Give a brief and basic explanation of the purpose of having (1) the EFI system partition and (2) the swap partition.**

### Answer

#### EFI System Partition

The EFI System Partition is used by computers with UEFI firmware to store boot loaders, device drivers, and other files required to start the operating system. It's a dedicated partition that allows the UEFI firmware to access and launch the operating system and its utilities before the OS itself starts. This partition is essential for the boot process in modern computing environments that use UEFI instead of traditional BIOS.
#### Swap Partition 

The swap partition serves as overflow space for your computer's RAM. If your system runs out of physical memory (RAM), it can move inactive pages of memory to the swap partition to free up RAM for active processes. This can prevent the system from crashing due to memory exhaustion, especially in situations where RAM is limited. However, accessing data on the swap partition is slower than accessing RAM, so while it increases the system's capacity for handling memory, it can also lead to slower performance if relied upon too heavily.

## Q4

**Test your understanding: What would be the name of the device file corresponding to the fourth partition on the second discovered storage device?**

### Answer

**sdb4**

## Q5

**To see your final results, run `fdisk -l /dev/sda` and paste the output into Gradescope.**

### Answer

```
Disk /dev/sda: 5 GiB, 5368709120 bytes, 10485760 sectors
Disk model: QEMU HARDDISK
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B9D6D4CB-DCAA-4C71-B870-5EDF998A5D93

Device       Start      End Sectors  Size Type
/dev/sda1     2048  1050623 1048576  512M EFI System
/dev/sda2  1050624  9437183 8386560    4G Linux filesystem
/dev/sda3  9437184 10483711 1046528  511M Linux swap
```

## Q6

**Run `lsblk` to see the hierarchy of these partitions.**

### Answer

```
NAME          MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS
loop0           7:0    0 766.5M  1 loop  /run/archiso/airootfs
sda             8:0    0     5G  0 disk
├─sda1          8:1    0   512M  0 part
├─sda2          8:2    0     4G  0 part
│ └─cryptroot 254:0    0     4G  0 crypt
└─sda3          8:3    0   511M  0 part
sr0            11:0    1 932.3M  0 rom   /run/archiso/bootmnt
```

## Q7

**What previous command we ran is similar to this command, and what’s the difference? (Bonus: why?)**

### Answer

**the `mkfs.fat -F32 /dev/sda1` command.**

#### Difference

`mkfs.fat -F32` formats the partition with the FAT32 filesystem, while `mkfs.ext4` formats with the Ext4 filesystem. `/dev/sda1` is likely a primary partition, whereas `/dev/mapper/cryptroot` suggests an encrypted logical volume.

#### Why

The `mkfs.fat` command is used to format a boot partition, which doesn't require the advanced features of Ext4 and needs to be readable by the system's firmware (like UEFI) to boot the system. The `mkfs.ext4` command is used for the main system partition where the Linux operating system and its files will reside.

## Q8

**You can see every single filesystem that’s currently mounted by running the `mount` command. Run it, and look for the two filesystems we just mounted.**

### Answer

```
/dev/mapper/cryptroot on /mnt type ext4 (rw,relatime)
/dev/sda1 on /mnt/boot type vfat (rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=ascii,shortname=mixed,utf8,errors=remount-ro)
```

## Q9

**Hypothetically, if we had made a separate `/home` partition and filesystem in the previous steps, what command(s) would we need to run to mount it? Assume the `/home` partition is `/dev/sda3`.**

### Answer

## Q10

**To show off your newly installed Arch system, run the following commands and paste the output into Gradescope**

### Answer

**`hostname -f`: arch**

**`ip addr`:**

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: ens2: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 52:54:00:19:b5:ce brd ff:ff:ff:ff:ff:ff
    altname enp0s2
    inet 192.168.122.172/24 brd 192.168.122.255 scope global dynamic noprefixroute ens2
       valid_lft 3518sec preferred_lft 3068sec
    inet6 fe80::a59:6c7d:ff7d:16eb/64 scope link
       valid_lft forever preferred_lft forever
```

**`mount`:**

```
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
sys on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
dev on /dev type devtmpfs (rw,nosuid,relatime,size=481452k,nr_inodes=120363,mode=755,inode64)
run on /run type tmpfs (rw,nosuid,nodev,relatime,mode=755,inode64)
efivarfs on /sys/firmware/efi/efivars type efivarfs (rw,nosuid,nodev,noexec,relatime)
/dev/mapper/cryptroot on / type ext4 (rw,relatime)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
cgroup2 on /sys/fs/cgroup type cgroup2 (rw,nosuid,nodev,noexec,relatime,nsdelegate,memory_recursiveprot)
pstore on /sys/fs/pstore type pstore (rw,nosuid,nodev,noexec,relatime)
bpf on /sys/fs/bpf type bpf (rw,nosuid,nodev,noexec,relatime,mode=700)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=37,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=1804)
hugetlbfs on /dev/hugepages type hugetlbfs (rw,nosuid,nodev,relatime,pagesize=2M)
mqueue on /dev/mqueue type mqueue (rw,nosuid,nodev,noexec,relatime)
debugfs on /sys/kernel/debug type debugfs (rw,nosuid,nodev,noexec,relatime)
tracefs on /sys/kernel/tracing type tracefs (rw,nosuid,nodev,noexec,relatime)
fusectl on /sys/fs/fuse/connections type fusectl (rw,nosuid,nodev,noexec,relatime)
configfs on /sys/kernel/config type configfs (rw,nosuid,nodev,noexec,relatime)
systemd-1 on /boot type autofs (rw,relatime,fd=52,pgrp=1,timeout=120,minproto=5,maxproto=5,direct,pipe_ino=2904)
tmpfs on /tmp type tmpfs (rw,nosuid,nodev,nr_inodes=1048576,inode64)
/dev/sda1 on /boot type vfat (rw,nosuid,nodev,noexec,relatime,nosymfollow,fmask=0077,dmask=0077,codepage=437,iocharset=ascii,shortname=mixed,utf8,errors=remount-ro)
tmpfs on /run/user/0 type tmpfs (rw,nosuid,nodev,relatime,size=98444k,nr_inodes=24611,mode=700,inode64)
```

**`lsblk`:**

```
NAME          MAJ:MIN RM  SIZE RO TYPE  MOUNTPOINTS
sda             8:0    0    5G  0 disk
├─sda1          8:1    0  512M  0 part
├─sda2          8:2    0    4G  0 part
│ └─cryptroot 254:0    0    4G  0 crypt /
└─sda3          8:3    0  511M  0 part  [SWAP]
sr0            11:0    1 1024M  0 rom
```

**`uname -a`:**

```
Linux arch 6.7.6-arch1-1 #1 SMP PREEMPT_DYNAMIC Fri, 23 Feb 2024 16:31:48 +0000 x86_64 GNU/Linux
```



## Some Tips

### Tip One

The command used to create the VM provided by the lab is:

```
sudo virt-install --name archvm --memory 575 --cpu host --vcpus 1 --disk size=5 --network network=default --boot uefi --graphics none --cdrom archlinux-2021.09.01-x86_64.iso
```

But the creation will run into error since current available versions of arch linux is much larger, which results in larger memory cost. So I recommend you to allocate at least 1 GB memory for the vm.

### Tip Two

You'd better do network configuration and management during the installation, which may become little tricky after you reboot your system. In my case, I need to install `dhcpcd` during installation, so that I can install `inetutils` to use `hostname` command after boot.

