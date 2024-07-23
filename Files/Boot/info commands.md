
### Hardware Information Commands

1. **`lspci`**
   Lists all PCI devices.
   ```sh
   lspci
   ```

2. **`lsusb`**
   Lists all USB devices.
   ```sh
   lsusb
   ```

3. **`lscpu`**
   Displays detailed information about the CPU architecture.
   ```sh
   lscpu
   ```

4. **`lsblk`**
   Lists information about all available or the specified block devices.
   ```sh
   lsblk
   ```

5. **`lshw`**
   Lists detailed information about all hardware.
   ```sh
   sudo lshw
   ```

6. **`lsdev`**
   Displays information about system devices.
   ```sh
   lsdev
   ```

7. **`lsmod`**
   Shows the status of modules in the Linux kernel.
   ```sh
   lsmod
   ```

8. **`dmidecode`**
   Displays hardware information from the system's DMI (SMBIOS) table.
   ```sh
   sudo dmidecode
   ```

### System Information Commands

1. **`uname -a`**
   Displays all system information.
   ```sh
   uname -a
   ```

2. **`hostnamectl`**
   Displays information about the system's hostname and related settings.
   ```sh
   hostnamectl
   ```

3. **`df -h`**
   Displays disk space usage in a human-readable format.
   ```sh
   df -h
   ```

4. **`free -h`**
   Shows memory usage in a human-readable format.
   ```sh
   free -h
   ```

### Network Information Commands

1. **`ifconfig`**
   Displays information about network interfaces.
   ```sh
   ifconfig
   ```

2. **`ip a`**
   Shows detailed information about all network interfaces.
   ```sh
   ip a
   ```

3. **`ethtool`**
   Displays or changes Ethernet device settings.
   ```sh
   sudo ethtool eth0
   ```

4. **`iwconfig`**
   Displays or changes wireless network device settings.
   ```sh
   iwconfig
   ```

### Storage Information Commands

1. **`fdisk -l`**
   Lists information about all partitions.
   ```sh
   sudo fdisk -l
   ```

2. **`blkid`**
   Displays or changes block device attributes.
   ```sh
   sudo blkid
   ```

3. **`mount`**
   Displays all currently mounted filesystems.
   ```sh
   mount
   ```

### Additional Tools

1. **`inxi`**
   Displays comprehensive system information in a user-friendly format.
   ```sh
   inxi -F
   ```

2. **`hwinfo`**
   Provides detailed information about hardware components.
   ```sh
   sudo hwinfo
   ```

These commands help you gather comprehensive information about your system's hardware and configuration, making it easier to manage and troubleshoot.
