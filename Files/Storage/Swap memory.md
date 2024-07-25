Swap memory is a type of virtual memory used to extend the physical RAM available on a system. When the RAM is full, inactive pages are moved to the swap space to free up RAM for active processes. This helps in preventing out-of-memory errors and can improve system stability, though accessing swap space is slower than accessing physical RAM.

### Key Concepts

- **Swap Space**: A portion of the hard drive or SSD reserved for use as virtual memory.
- **Swap File**: A file on a filesystem used as swap space.
- **Swap Partition**: A dedicated partition on the disk used exclusively for swap.

### Managing Swap Space

#### 1. **Check Current Swap Usage**

You can check the current swap space usage with:

```sh
swapon --show
```

Or:

```sh
free -h
```

#### 2. **Add Swap Space**

You can add swap space either by creating a swap file or a swap partition.

##### **Creating a Swap File**

1. **Create a Swap File**

   ```sh
   sudo fallocate -l 1G /swapfile
   ```

   Or if `fallocate` is not available:

   ```sh
   sudo dd if=/dev/zero of=/swapfile bs=1M count=1024
   ```

   - `1G` or `1024`: Size of the swap file.

2. **Set the Correct Permissions**

   ```sh
   sudo chmod 600 /swapfile
   ```

3. **Set Up the Swap Area**

   ```sh
   sudo mkswap /swapfile
   ```

4. **Enable the Swap File**

   ```sh
   sudo swapon /swapfile
   ```

5. **Verify the Swap Space**

   ```sh
   swapon --show
   ```

6. **Make Swap File Permanent**

   Add the following line to `/etc/fstab`:

   ```sh
   /swapfile none swap sw 0 0
   ```

##### **Creating a Swap Partition**

1. **Create a Swap Partition** (using a tool like `fdisk`, `parted`, or `gparted`).

2. **Set Up the Swap Area**

   ```sh
   sudo mkswap /dev/sdXn
   ```

   Replace `/dev/sdXn` with your partition identifier.

3. **Enable the Swap Partition**

   ```sh
   sudo swapon /dev/sdXn
   ```

4. **Verify the Swap Space**

   ```sh
   swapon --show
   ```

5. **Make Swap Partition Permanent**

   Add the following line to `/etc/fstab`:

   ```sh
   /dev/sdXn none swap sw 0 0
   ```

#### 3. **Adjusting Swappiness**

Swappiness is a parameter that controls how often the system swaps data out of RAM to the swap space. It can be set to a value between 0 and 100. A lower value means the system will use swap space less often.

1. **Check Current Swappiness Value**

   ```sh
   cat /proc/sys/vm/swappiness
   ```

2. **Set Swappiness Temporarily**

   ```sh
   sudo sysctl vm.swappiness=10
   ```

3. **Set Swappiness Permanently**

   Edit `/etc/sysctl.conf`:

   ```sh
   sudo nano /etc/sysctl.conf
   ```

   Add or modify the following line:

   ```sh
   vm.swappiness=10
   ```

   Apply the changes:

   ```sh
   sudo sysctl -p
   ```

#### 4. **Turn Off Swap**

If you need to disable swap temporarily:

```sh
sudo swapoff /swapfile
```

Or for a swap partition:

```sh
sudo swapoff /dev/sdXn
```

To remove swap space, first turn it off, then remove the swap file or partition configuration from `/etc/fstab`.

### Summary

Swap space is an important component of virtual memory management in Linux, allowing systems to handle more processes than physical RAM alone would permit. By understanding how to manage and configure swap space, you can optimize system performance and stability.
