# Homelab Project: Fixing a VM Boot Failure (Missing initramfs on ESXi)

This project documents how I troubleshooted and resolved a VM boot issue in my **homelab** on **VMware ESXi** caused by a missing **initramfs file**.

---

## 🔎 Problem
When the VM was powered on, it dropped into **initramfs emergency mode** and could not boot the OS.  

**What is initramfs?**  
Initramfs (Initial RAM File System) is a temporary root filesystem loaded into memory during boot. It contains essential drivers, kernel modules, and tools needed to mount the actual root filesystem. If it’s missing or corrupted, the system cannot boot.

---

### 🛠 Troubleshooting Steps

1. **Accessed the VM via ESXi Console**
   - Rebooted the VM, interrupted GRUB, and selected the **Rescue Kernel**.
   - Pressed **Enter** to boot into rescue mode.

2. **Checked Logs for Errors**
   ```bash
   tail -20 /var/log/messages

3. **Investigated, Rebuilt, and Rebooted

Inside the /boot directory, I discovered that the main initramfs file was missing, but a backup existed.
I then rebuilt the initramfs using dracut and rebooted the VM.

cd /boot
ls -l
dracut initramfs-<kernel_version>.img <kernel_version>
reboot

## 📌 Lessons Learned

Understanding the Linux boot process (GRUB, kernel, initramfs) is crucial for system administrators.
dracut is a powerful tool for rebuilding initramfs and recovering from boot issues.
Practicing in a homelab environment helps sharpen real-world troubleshooting skills.

### 🌟 Skills Highlighted

Linux System Recovery & Boot Troubleshooting
VMware ESXi VM Management
Red Hat Enterprise Linux (RHEL) Administration
