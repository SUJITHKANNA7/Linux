Network File System (NFS) is a distributed file system protocol that allows a user on a client computer to access files over a network in a manner similar to how local storage is accessed. It is commonly used in Linux and UNIX environments for sharing directories and files across a network. Here’s an overview of NFS and its management in Linux:

### 1. **Installing NFS**

#### On the Server

- **Debian/Ubuntu**:
  ```sh
  sudo apt-get install nfs-kernel-server
  ```

- **RHEL/CentOS**:
  ```sh
  sudo yum install nfs-utils
  ```

#### On the Client

- **Debian/Ubuntu**:
  ```sh
  sudo apt-get install nfs-common
  ```

- **RHEL/CentOS**:
  ```sh
  sudo yum install nfs-utils
  ```

### 2. **Configuring NFS Server**

1. **Create a shared directory**:
   ```sh
   sudo mkdir -p /srv/nfs/shared
   ```

2. **Set permissions**:
   ```sh
   sudo chown nobody:nogroup /srv/nfs/shared
   sudo chmod 777 /srv/nfs/shared
   ```

3. **Edit `/etc/exports` to define the shared directories**:
   ```sh
   sudo nano /etc/exports
   ```

   Add the following line to share the directory:
   ```sh
   /srv/nfs/shared    192.168.1.0/24(rw,sync,no_subtree_check)
   ```

   - `192.168.1.0/24`: The client network that can access the share.
   - `rw`: Read and write permissions.
   - `sync`: Writes changes to disk before responding.
   - `no_subtree_check`: Prevents subtree checking.

4. **Export the shared directories**:
   ```sh
   sudo exportfs -a
   ```

5. **Start and enable the NFS service**:

   - **Debian/Ubuntu**:
     ```sh
     sudo systemctl start nfs-kernel-server
     sudo systemctl enable nfs-kernel-server
     ```

   - **RHEL/CentOS**:
     ```sh
     sudo systemctl start nfs
     sudo systemctl enable nfs
     ```

### 3. **Configuring NFS Client**

1. **Create a mount point**:
   ```sh
   sudo mkdir -p /mnt/nfs/shared
   ```

2. **Mount the NFS share**:
   ```sh
   sudo mount -t nfs server_ip:/srv/nfs/shared /mnt/nfs/shared
   ```

   Replace `server_ip` with the IP address of the NFS server.

3. **Verify the mount**:
   ```sh
   df -h
   ```

### 4. **Making NFS Mount Persistent**

1. **Edit `/etc/fstab`**:
   ```sh
   sudo nano /etc/fstab
   ```

2. **Add the entry**:
   ```sh
   server_ip:/srv/nfs/shared /mnt/nfs/shared nfs defaults 0 0
   ```

3. **Test the configuration**:
   ```sh
   sudo mount -a
   ```

### 5. **Managing NFS Shares**

#### Checking Mounted NFS Shares

- **`df`**: Reports file system disk space usage.
  ```sh
  df -h
  ```

- **`mount`**: Lists all mounted file systems.
  ```sh
  mount
  ```

#### Unmounting NFS Shares

- **Unmount an NFS share**:
  ```sh
  sudo umount /mnt/nfs/shared
  ```

#### Exporting and Unexporting NFS Directories

- **Export all shared directories**:
  ```sh
  sudo exportfs -a
  ```

- **Unexport a specific directory**:
  ```sh
  sudo exportfs -u server_ip:/srv/nfs/shared
  ```

- **View currently exported file systems**:
  ```sh
  sudo exportfs -v
  ```

### 6. **Advanced NFS Configuration**

#### Setting Permissions

- **Edit `/etc/exports`** to fine-tune permissions for each share.

  Example:
  ```sh
  /srv/nfs/shared 192.168.1.0/24(rw,sync,no_subtree_check)
  ```

- Reload the NFS configuration:
  ```sh
  sudo exportfs -ra
  ```

#### Using `autofs` for Automounting

1. **Install `autofs`**:

   - **Debian/Ubuntu**:
     ```sh
     sudo apt-get install autofs
     ```

   - **RHEL/CentOS**:
     ```sh
     sudo yum install autofs
     ```

2. **Edit `/etc/auto.master`** to define the automount point:
   ```sh
   sudo nano /etc/auto.master
   ```

   Add the following line:
   ```sh
   /nfs /etc/auto.nfs
   ```

3. **Create `/etc/auto.nfs`**:
   ```sh
   sudo nano /etc/auto.nfs
   ```

   Add the following line:
   ```sh
   shared -fstype=nfs,rw server_ip:/srv/nfs/shared
   ```

4. **Restart `autofs` service**:
   ```sh
   sudo systemctl restart autofs
   ```

5. **Access the NFS share**:
   ```sh
   ls /nfs/shared
   ```

### Summary

NFS provides a robust solution for sharing directories and files across a network, especially in UNIX/Linux environments. Proper configuration and management of NFS include setting up the server, defining shared directories, and configuring clients to access these shares. Additionally, advanced configurations like automounting with `autofs` can help streamline access to NFS shares in dynamic environments.
