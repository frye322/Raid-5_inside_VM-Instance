# Raid-5_inside_VM-Instance
Adding RAID-5 in a VMware Instance of Windows Server 2016


#Adding RAID-5 in a VMware Instance of Windows Server 2016

#Hardware Overview

Installed:
- 4 × 3.5" SATA HDD @ 1TB each (Brand New)

## VMware ESXi Setup

1. Physically installed the 4 HDDs on the ESXi host.
2. Logged into the **VMware ESXi web interface**.
3. Added each HDD as a **new datastore**:
   - Named: `HDD1`, `HDD2`, `HDD3`, `HDD4`

## Assigning the Drives to the VM

1. Navigated to my **Windows Server 2016** virtual machine.
2. Clicked **Edit Settings**.
3. Manually added the 4 HDDs to the VM as **virtual disks**.

## Reboot and Disk Management

1. Restarted the Windows Server 2016 instance.
2. Opened **Disk Management** inside Windows.

You should now see the 4 new disks listed as **unallocated space**.

## Creating the RAID-5 Volume

1. Right-click one of the new disks → **Convert to Dynamic Disk** (if prompted).
2. Right-click the same disk again → Select **New RAID-5 Volume**.
3. Add the remaining 3 disks to the array.

> Windows will ask whether to perform a **Quick Format** or **Full Format** (Slow Format).

# Format Choice Tip

- If you are using **old or reused drives**, it's **advisable to use Full Format** to:
  - Wipe previous data
  - Detect and isolate bad sectors
  - It will take a while to finish formating.

- Since I used **brand new drives**, I chose **Quick Format**, and it completed in a few minutes.

## Creating a Shared Backup Folder

1. After format, the new **RAID-5 volume** was ready.
2. Created a shared folder inside the new volume.
3. Configured permissions to **allow all users** to use it as:
   - Backup location
   - Shared storage for important files

---

## Final Notes

- **RAID-5** offers fault tolerance — one drive can fail without data loss.
- It’s a good balance between performance, storage efficiency, and redundancy.


