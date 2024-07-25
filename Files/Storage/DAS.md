Direct Attached Storage (DAS) refers to a storage system that is directly connected to a server or workstation without a network intermediary. This type of storage architecture is commonly used in individual computers and servers due to its simplicity and high performance. Here's an overview of DAS and its management in Linux:

### 1. **Overview of DAS**

**Characteristics of DAS:**
- Directly attached to a host computer (e.g., via SATA, SAS, USB).
- Typically used for local storage.
- High-speed access compared to networked storage solutions.
- Simple to set up and manage.
- Examples: Internal hard drives, SSDs, and external USB drives.

### 2. **Identifying DAS Devices in Linux**

To identify and list DAS devices connected to your system, you can use the following commands:

- **`lsblk`**: Lists all block devices.
  ```sh
  lsblk
  ```

- **`fdisk -l`**: Lists all disk partitions.
  ```sh
  sudo fdisk -l
  ```

- **`blkid`**: Lists block devices with detailed information.
  ```sh
  blkid
  ```

- **`lsscsi`**: Lists SCSI devices.
  ```sh
  lsscsi
  ```

### 3. **Partitioning DAS Devices**

#### Using `fdisk` for MBR Partitioning:

```sh
sudo fdisk /dev/sdX
```

- Press `n` to create a new partition.
- Select partition type (primary or extended).
- Specify the partition size.
- Press `w` to write the changes.

#### Using `parted` for GPT Partitioning:

```sh
sudo parted /dev/sdX
```

- Create a new partition table:
  ```sh
  (parted) mklabel gpt
  ```
- Create a new partition:
  ```sh
  (parted) mkpart primary ext4 1MiB 100%
  ```

### 4. **Creating File Systems on DAS Devices**

Once partitions are created, you need to format them with a file system:

- **ext4**:
  ```sh
  sudo mkfs.ext4 /dev/sdX1
  ```

- **xfs**:
  ```sh
  sudo mkfs.xfs /dev/sdX1
  ```

- **vfat (FAT32)**:
  ```sh
  sudo mkfs.vfat /dev/sdX1
  ```

### 5. **Mounting DAS Devices**

To use the storage, you need to mount the file systems:

1. **Create a mount point**:
   ```sh
   sudo mkdir /mnt/my_storage
   ```

2. **Mount the file system**:
   ```sh
   sudo mount /dev/sdX1 /mnt/my_storage
   ```

3. **Verify the mount**:
   ```sh
   df -h
   ```

### 6. **Making Mounts Persistent**

To ensure the file system is mounted at boot, add an entry to `/etc/fstab`:

1. **Edit `/etc/fstab`**:
   ```sh
   sudo nano /etc/fstab
   ```

2. **Add the entry**:
   ```sh
   /dev/sdX1  /mnt/my_storage  ext4  defaults  0  2
   ```

3. **Test the configuration**:
   ```sh
   sudo mount -a
   ```

### 7. **Managing DAS Devices**

#### Checking Disk Usage

- **`df`**: Reports file system disk space usage.
  ```sh
  df -h
  ```

- **`du`**: Estimates file space usage.
  ```sh
  du -sh /path/to/directory
  ```

#### Monitoring Disk Health

- **`smartctl`**: Monitors S.M.A.R.T. attributes.
  ```sh
  sudo smartctl -a /dev/sdX
  ```

### 8. **Expanding DAS Storage**

#### Extending a Partition

- Use `parted` or `gparted` to resize the partition.
- Extend the file system:

  - **ext4**:
    ```sh
    sudo resize2fs /dev/sdX1
    ```

  - **xfs**:
    ```sh
    sudo xfs_growfs /mnt/my_storage
    ```

#### Adding New Storage

1. **Identify the new device** using `lsblk` or `fdisk -l`.
2. **Partition and format** the new device.
3. **Mount the new file system** and update `/etc/fstab` if needed.

### Summary

- **Identification**: Use commands like `lsblk`, `fdisk -l`, and `blkid` to identify DAS devices.
- **Partitioning**: Use `fdisk` for MBR and `parted` for GPT partitioning.
- **Creating File Systems**: Format partitions with file systems like `ext4`, `xfs`, or `vfat`.
- **Mounting**: Mount partitions manually or configure them in `/etc/fstab` for automatic mounting at boot.
- **Management**: Use tools like `df`, `du`, and `smartctl` to manage and monitor disk usage and health.
- **Expansion**: Resize partitions and file systems as needed to accommodate growing storage requirements.

Managing DAS in Linux involves a series of steps from identifying and partitioning the storage devices to creating file systems, mounting, and maintaining them. Proper management ensures reliable and efficient use of directly attached storage resources.
