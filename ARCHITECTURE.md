# hOtSwap Architecture (Draft 1)

This is basically my plan for the "brain transplant." I have no idea if this is the best way to do it, but here's how I think we can swap Windows for Linux without a USB stick.

### Stage 1: The Windows "Scout"
First, we need a .exe that runs while the user is still in Windows. 
* It needs to look at C:\Users\ and figure out how much data we're moving so we don't run out of space mid-swap.
* It downloads a small "Bridge" (a tiny Linux kernel) and the actual Linux ISO the user wants.
* The big trick: It uses 'bcdedit' to mess with the boot order. It tells the PC to boot into our Bridge kernel just once. 
* Tools: bcdedit (Windows)

### Stage 2: The Bridge (The Magic Part)
The PC reboots and instead of Windows, it loads a tiny Linux OS into the RAM.
* Since it's running in RAM, we can actually "unlock" the physical SSD. 
* We use 'ntfsresize' to shrink the Windows partition and make a hole. 
* Then we create a new partition for Linux in that hole.
* Tools: ntfsresize, fdisk/parted

### Stage 3: Moving the Goods
This is where we move the files.
* We mount the Windows partition (read-only so we don't break it) and the new Linux partition.
* We copy the photos/docs over. 
* I need to figure out how to map "Windows User" permissions to "Linux User" permissions so the files aren't locked when we're done.
* Networking: If we're moving files to a NAS because the local disk is tiny, we have to use "host" networking. I learned from my Portainer setup that virtual bridges just break everything here.

### Stage 4: The Hand-off
* We use 'efibootmgr' to tell the BIOS that Linux is the new boss.
* We delete the old Windows boot entry.
* Reboot, and hopefully, it just works.
* Tools: efibootmgr

### Stuff that will probably break
1. BitLocker: If this is on, the Bridge can't see the files. We need to check 'manage-bde -status' before we start.
2. Secure Boot: The BIOS might hate our Bridge kernel because it's not signed by Microsoft. 
3. Filesystem units: One tool uses MB, another uses MiB. If I mess this up, the partition gets cut in half and everything dies.
