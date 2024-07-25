On-demand mounting is a technique where file systems are automatically mounted when they are accessed and unmounted when they are no longer in use. This can be particularly useful for network file systems like NFS or for less frequently accessed storage. One popular tool for implementing on-demand mounting in Linux is `autofs`.

### Setting Up `autofs` for On-Demand Mounting

#### 1. **Install `autofs`**

- **Debian/Ubuntu**:
  ```sh
  sudo apt-get install autofs
  ```

- **RHEL/CentOS**:
  ```sh
  sudo yum install autofs
  ```

#### 2. **Configure `autofs`**

The `autofs` service uses a master map file (`/etc/auto.master`) to manage mount points and corresponding map files.

1. **Edit `/etc/auto.master`**:
   ```sh
   sudo nano /etc/auto.master
   ```

   Add the following line to define a mount point and its map file:
   ```sh
   /nfs /etc/auto.nfs --timeout=600
   ```

   - `/nfs`: The directory under which the file systems will be mounted.
   - `/etc/auto.nfs`: The map file defining the details of the mounts.
   - `--timeout=600`: The time (in seconds) after which an unused file system will be automatically unmounted.

2. **Create the map file `/etc/auto.nfs`**:
   ```sh
   sudo nano /etc/auto.nfs
   ```

   Add entries for the file systems to be mounted on demand:
   ```sh
   shared -fstype=nfs,rw server_ip:/srv/nfs/shared
   ```

   - `shared`: The subdirectory under `/nfs` where the NFS share will be mounted.
   - `-fstype=nfs,rw`: The file system type and options.
   - `server_ip:/srv/nfs/shared`: The NFS server and exported directory.

#### 3. **Restart `autofs` Service**

- **Debian/Ubuntu**:
  ```sh
  sudo systemctl restart autofs
  ```

- **RHEL/CentOS**:
  ```sh
  sudo systemctl restart autofs
  ```

#### 4. **Accessing the On-Demand Mount**

Now, when you access the directory `/nfs/shared`, the NFS share will be automatically mounted.

- List the contents of the mounted directory:
  ```sh
  ls /nfs/shared
  ```

After the specified timeout period (600 seconds in this case), the file system will be automatically unmounted if it is no longer in use.

### Example Configuration

#### `/etc/auto.master`
```sh
/nfs /etc/auto.nfs --timeout=600
```

#### `/etc/auto.nfs`
```sh
shared -fstype=nfs,rw server_ip:/srv/nfs/shared
```

### Benefits of On-Demand Mounting

- **Resource Efficiency**: File systems are only mounted when needed, saving system resources.
- **Automation**: Reduces the need for manual mounting and unmounting.
- **Scalability**: Useful for environments with many file systems or network shares.

### Troubleshooting `autofs`

- **Check the status of `autofs` service**:
  ```sh
  sudo systemctl status autofs
  ```

- **View `autofs` logs**:
  ```sh
  sudo journalctl -u autofs
  ```

- **Manually trigger a mount**:
  ```sh
  sudo automount -fv
  ```

By configuring `autofs` for on-demand mounting, you can streamline the management of your file systems and ensure that resources are efficiently utilized.
