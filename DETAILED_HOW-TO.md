# Lenovo Win7 Slim Down Detailed How-To
----
## Requirements / Prerequisites / Assumptions

Hardware: Lenovo (Tested on a W530)
Host OS: Linux (Tested with Ubuntu 18.04, but any Linux OS should work)
Hypervisor: VirtualBox v5.2.18-dfsg-2~ubuntu18.04.3 (Installed via apt)
Guest OS: Lenovo Windows 7 Pro

-- Windows 7 Application and Drivers Recovery Disc 1/2
md5: a4209af89197e52a8c35bca5b4b4e7a6
sha512: 454b8f598e5c19cd85d3cf54537b2eb793576b45bc837f7d8316671f8cc99834e3ccbc9ef08284b9448f404c0751d325c0bea199ba22f954ee90f4bc8d78ca1f

-- Windows 7 Application and Drivers Recovery Disc 2/2
md5: 9fe5d2482b3895bfefe7518bb0af4e1f
sha512: 40957c1e395166e9a1fe398401f4e93982c4754b5fcaf55f5fc7f34032ed7abdab86744f4eabe9d4061c976327d4d15ee1b0f6749cdc052d022ef9210b5594e2

-- Windows 7 Professional SP 1 Operating System Recovery Disc 1
md5: 5d22c93dc1d2aaa9fac826fea385f4ee
sha512: 7c08e5de3b2b63addfac616e0f3137576d3db37353a3986690fc78b74532c85863172e41d59e95849e28537046f795b8eab063c9ca40005601b09c510ca59455

~/virtualbox
    └── win7
    └── slic

----
# Prepare

## Extract the SLIC

    $ sudo dd if=/sys/firmware/acpi/tables/SLIC of=/home/user/virtualbox/slic/win7_lenovo_slic.bin

## Build VM & add SLIC

1. Create a new VM
    -- Type: Microsoft Windows
    -- Version: Windows 7 (64-bit)
    -- Memory: 1024MB
    -- Processors: 1
    -- Disk: 64GB (35G after updates + 14G 'Q' Recovery drive that can get removed later)
    -- CD/DVD: Win7 Application and Driver Recovery Disc 1/2

    Do not start Win7 yet.

2. Add SLIC to virtual machine:
    
        $ VBoxManage setextradata "win7" "VBoxInternal/Devices/acpi/0/Config/CustomTable" "/home/user/virtualbox/slic/win7_lenovo_slic.bin"
 
3. Start the VM and continue through the install process as normal. After loading the files from the 3rd disc and when Win7 installer tells you that it needs to reboot to continue the install process, cick OK and when the virtual machine reboots close the VM window and select the option to 'Power Off the machine'
 
4. Create a snapshot (CTRL+SHIFT+T) so you will have the ability to return to this moment in time in the case that something with the patch fails or you want to fine tune what runs and what doesn't run.
 
## Mount VDI & patch

1. Load NBD module

        :~# lsmod | grep nbd
        :~# 
        :~# modprobe nbd max_part=16
        :~# lsmod | grep nbd
        nbd                    36864  0
        :~# 
        
2. Mount the file system

    Example of GPT:

        :~# qemu-nbd -c /dev/nbd0 /home/user/virtualbox/win7/win7.vdi
        :~# ls -l /dev/nbd0*
        brw-rw---- 1 root disk 43, 0 Mar 11 21:49 /dev/nbd0
        brw-rw---- 1 root disk 43, 1 Mar 11 21:49 /dev/nbd0p1
        brw-rw---- 1 root disk 43, 2 Mar 11 21:49 /dev/nbd0p2
        brw-rw---- 1 root disk 43, 3 Mar 11 21:49 /dev/nbd0p3
        brw-rw---- 1 root disk 43, 4 Mar 11 21:49 /dev/nbd0p4
        :~# fdisk -l /dev/nbd0
        Disk /dev/nbd0: 64 GiB, 68719476736 bytes, 134217728 sectors
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: gpt
        Disk identifier: 729CD692-2DD3-4384-A8DE-381E7224A4B0
        
        Device          Start       End   Sectors  Size Type
        /dev/nbd0p1      2048    206847    204800  100M EFI System
        /dev/nbd0p2    206848    468991    262144  128M Microsoft reserved
        /dev/nbd0p3    468992 105543679 105074688 50.1G Microsoft basic data
        /dev/nbd0p4 105543680 134215679  28672000 13.7G Microsoft basic data
        :~# mount /dev/nbd0p3 /mnt/win7
        :~# ls -l /mnt/win7
        total 488
        drwxrwxrwx 1 root root   4096 Mar 11 21:36  Boot
        -rwxrwxrwx 1 root root 383786 Nov 20  2010  bootmgr
        -rwxrwxrwx 1 root root   8192 Feb 24  2011  BOOTSECT.BAK
        lrwxrwxrwx 2 root root     15 Jul 13  2009 'Documents and Settings' -> /mnt/win7/Users
        drwxrwxrwx 1 root root      0 Jul 13  2009  PerfLogs
        drwxrwxrwx 1 root root   4096 Mar 11 21:39  ProgramData
        drwxrwxrwx 1 root root   4096 Dec  8  2011 'Program Files'
        drwxrwxrwx 1 root root   4096 Dec  9  2011 'Program Files (x86)'
        drwxrwxrwx 1 root root      0 Dec  9  2011 '$Recycle.Bin'
        drwxrwxrwx 1 root root   4096 Mar 11 21:39  SWTOOLS
        drwxrwxrwx 1 root root  65536 Mar 11 21:40  SWWORK
        drwxrwxrwx 1 root root   4096 Nov 20  2010  Users
        drwxrwxrwx 1 root root  16384 Mar 11 21:36  Windows
        :~# 

    Example of MBR:

        :~# qemu-nbd -c /dev/nbd0 /home/user/virtualbox/win7/win7.vdi
        :~# ls -l /dev/nbd0*
        brw-rw---- 1 root disk 43, 0 Mar 11 21:53 /dev/nbd0
        brw-rw---- 1 root disk 43, 1 Mar 11 21:53 /dev/nbd0p1
        brw-rw---- 1 root disk 43, 2 Mar 11 21:53 /dev/nbd0p2
        brw-rw---- 1 root disk 43, 3 Mar 11 21:53 /dev/nbd0p3
        :~# fdisk -l /dev/nbd0
        Disk /dev/nbd0: 64 GiB, 68719476736 bytes, 134217728 sectors
        Units: sectors of 1 * 512 = 512 bytes
        Sector size (logical/physical): 512 bytes / 512 bytes
        I/O size (minimum/optimal): 512 bytes / 512 bytes
        Disklabel type: dos
        Disk identifier: 0xf2805a0d

        Device      Boot     Start       End   Sectors  Size Id Type
        /dev/nbd0p1 *         2048   3074047   3072000  1.5G  7 HPFS/NTFS/exFAT
        /dev/nbd0p2        3074048 105543679 102469632 48.9G  7 HPFS/NTFS/exFAT
        /dev/nbd0p3      105543680 134215679  28672000 13.7G  7 HPFS/NTFS/exFAT
        :~# mount /dev/nbd0p2 /mnt/win7
        :~# ls -l /mnt/win7/
        total 488
        drwxrwxrwx 1 root root   4096 Feb 24  2011  Boot
        -rwxrwxrwx 1 root root 383786 Nov 20  2010  bootmgr
        -rwxrwxrwx 1 root root   8192 Feb 24  2011  BOOTSECT.BAK
        lrwxrwxrwx 2 root root     15 Jul 13  2009 'Documents and Settings' -> /mnt/win7/Users
        drwxrwxrwx 1 root root      0 Jul 13  2009  PerfLogs
        drwxrwxrwx 1 root root   4096 Mar 11 18:16  ProgramData
        drwxrwxrwx 1 root root   4096 Dec  8  2011 'Program Files'
        drwxrwxrwx 1 root root   4096 Dec  9  2011 'Program Files (x86)'
        drwxrwxrwx 1 root root      0 Dec  9  2011 '$Recycle.Bin'
        drwxrwxrwx 1 root root   4096 Mar 11 18:16  SWTOOLS
        drwxrwxrwx 1 root root  65536 Mar 11 18:17  SWWORK
        drwxrwxrwx 1 root root   4096 Nov 20  2010  Users
        drwxrwxrwx 1 root root  16384 Mar 11 18:14  Windows
        :~#

3. Fetch the patch and patch.

        :/mnt# wget .......
        :~# cd /mnt/win7
        :/mnt/win7# patch -p1 < ../win7-slim-virt.patch
        patching file SWTOOLS/antivirus/NORTONIS/ALL/MODULECUST/SETUP.CMD
        patching file SWTOOLS/Apps/Adobe/AdobeReader/MODULECUST/InstallAdbeRdrX.cmd
        patching file SWTOOLS/Apps/Adobe/AdobeReader/MODULECUST/SetupMUI.cmd
        <..snip..>
        patching file SWWORK/ZDOWORK2/CHECKSKU.CMD
        patching file SWWORK/ZDOWORK2/OA2CLN.CMD
        patching file SWWORK/ZDOWORK6/SETCLEAN.CMD
        :/mnt/win7# 

4. Unmount the file system and disconnect the NBD

        :/mnt/win7# cd ..
        :/mnt# umount /mnt/win7
        :/mnt# qemu-nbd -d /dev/nbd0
        /dev/nbd0 disconnected
        :/mnt# 

5. Boot your system and let the rest of the install process continue.
