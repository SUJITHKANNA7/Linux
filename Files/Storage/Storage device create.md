Creating storage from scratch on a Linux system involves several steps, including configuring the disk, partitioning, creating a file system, and mounting it. Here’s a step-by-step guide to help you through the process:

### 1. Identify the Disk

First, identify the disk you want to use for creating storage. You can use tools like `lsblk` or `fdisk` to list available disks.

```sh
lsblk
```

This will show you all the block devices and their partitions. Assume you want to work with `/dev/sdX`, where `X` represents the disk identifier.

### 2. Partition the Disk

Use a partitioning tool like `fdisk` or `parted` to create partitions on the disk.

#### Using `fdisk`

1. **Start `fdisk`**:
   ```sh
   sudo fdisk /dev/sdX
   ```

2. **Create a new partition**:
   - Type `n` to create a new partition.
   - Choose `p` for a primary partition or `e` for an extended partition.
   - Specify the partition number, first sector, and last sector (or size).
   - Type `w` to write the partition table to disk and exit.

#### Using `parted`

1. **Start `parted`**:
   ```sh
   sudo parted /dev/sdX
   ```

2. **Create a new partition table**:
   ```sh
   (parted) mklabel gpt
   ```

3. **Create a new partition**:
   ```sh
   (parted) mkpart primary ext4 0% 100%
   ```

4. **Quit parted**:
   ```sh
   (parted) quit
   ```

### 3. Create a File System

Once you have created the partition, you need to create a file system on it.

#### For ext4 File System

```sh
sudo mkfs.ext4 /dev/sdX1
```

#### For xfs File System

```sh
sudo mkfs.xfs /dev/sdX1
```

#### For vfat (FAT32) File System

```sh
sudo mkfs.vfat /dev/sdX1
```

### 4. Create a Mount Point

A mount point is a directory where the file system will be attached.

```sh
sudo mkdir /mnt/my_storage
```

### 5. Mount the File System

Mount the new file system to the mount point you created.

```sh
sudo mount /dev/sdX1 /mnt/my_storage
```

### 6. Verify the Mount

Check that the file system is mounted correctly.

```sh
df -h
```

You should see `/dev/sdX1` mounted on `/mnt/my_storage`.

### 7. Make the Mount Permanent

To ensure the file system mounts automatically on boot, add an entry to `/etc/fstab`.

1. **Edit `/etc/fstab`**:
   ```sh
   sudo nano /etc/fstab
   ```

2. **Add an entry**:
   ```sh
   /dev/sdX1  /mnt/my_storage  ext4  defaults  0  2
   ```

   Adjust the file system type (`ext4`, `xfs`, etc.) as needed.

3. **Test the fstab entry**:
   ```sh
   sudo mount -a
   ```

### 8. (Optional) Check and Repair the File System

Periodically check the file system for errors.

- **For ext4**:
  ```sh
  sudo fsck.ext4 /dev/sdX1
  ```

- **For xfs**:
  ```sh
  sudo xfs_repair /dev/sdX1
  ```

### Summary

1. **Identify the disk**: Use `lsblk` or `fdisk`.
2. **Partition the disk**: Use `fdisk` or `parted`.
3. **Create a file system**: Use `mkfs` (e.g., `mkfs.ext4`).
4. **Create a mount point**: Use `mkdir`.
5. **Mount the file system**: Use `mount`.
6. **Make it permanent**: Edit `/etc/fstab`.
7. **Verify and check**: Use `df -h`, `fsck`, or `xfs_repair`.

Following these steps will allow you to set up storage on a Linux system from scratch.
