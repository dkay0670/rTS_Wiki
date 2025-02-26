---
layout: default
title: Wiping Disks
nav_exclude: false
has_children: false
parent: Disks
search_exclude: false
last_modified_date: 2022-08-05
redirect_from: /books/troubleshooting-with-a-linux-live-session/page/wiping-disks
---

# Wiping Disks
This guide uses the [Linux live session](/docs/live-sessions/linux-live-session).

## Encrypted disks
All modern OS are capable of encrypting disks, on Windows this is called Bitlocker, MacOS has FileVault and Linux/BSD typically use LUKS. If you already use encryption to secure your data at rest then you are a step ahead with wiping the disk as well. You can format the disk by doing a full and proper reinstall of the OS ([Windows guide here](/windows)) to cycle your encryption keys. Once these keys are destroyed recovery of the old data is not possible.

## Wiping with software
### HDD
`nwipe` is a fork of `dwipe` which is the utility used in the popular [DBAN](https://dban.org/) solution.

1. Open "terminal emulator" from the application menu
2. Run `sudo nwipe` in the terminal to launch our nwipe session
3. Navigate up and down the list with the arrow keys, select disks by size with the space bar. 
	* Removing extra disks from the machine may make this selection easier. **Choosing the wrong disk will cause data loss**
	* You can change the wipe method by pressing `m`. DoD short is the default and recomended method. It makes 3 passes over the disk.
    * You can change the number of rounds by pressing `r`. This multiplies the method. Leaving DoD short and setting 2 rounds would make 6 passes (1 is recommended).
4. Press capital `S` to start the process

### SSD
[Secure erase article on kernel.org](https://ata.wiki.kernel.org/index.php/ATA_Secure_Erase)

#### NVMe SSD
This relies on the application `nvme-cli`. It might not be included on all Linux distros, you might have to install it. It is included in the r/Techsupport rescue media.
1. Open "terminal emulator" from the application menu.
2. Run `sudo nvme list` to see the list of valid nvme drives.
	* Some SSDs will not be listed here. If your drive isn't listed, put your computer to sleep and then wake it up. This is mainly an issue with Samsung drives.
3. Run `sudo nvme format -s2 /dev/nvmeX` where X is the location of your drive.
	* Example: `sudo nvme format -s2 /dev/nvme0n1` **Choosing the wrong disk will cause data loss**
    * Some manufacturers lock their drives. If you get an invalid field error, you will have to use a tool from your SSDs manufacturer. When doing this, make sure you do a secure erase.

## Physical destruction
Physical destruction is a perfectly acceptable method to ensure data cannot be read from a disk. This can be accomplished by either smashing the disk with a hammer or opening it and placing it in salt water to rust.

> DO NOT SMASH AN OPEN DISK.
> Disk platters may be made out of glass that can splinter into painfully small shards. These will go through your skin to cause intense irritation.

