## Login methods 

- Local text mode console
- Local Graphical mode 
- Remote Text mode (SSH, Telnet)
- Remote Graphical mode (Remote Desktop Connection, VNC)

### Authentication

Autentication invloves in two ways,
- Password based
- Key based auth

### SSH Login 

SSH, or Secure Shell, **``protocol used to securly logon to remote systems.``**
SSH works by connecting client program to an ssh server called sshd. 

### Components

- **SSH Client**: A program that establishes the connection to the SSH server. Examples include `ssh` command-line tool in Linux and PuTTY for Windows.
- **SSH Server**: The service that runs on the remote machine and listens for incoming SSH connections. In Linux, the most common SSH server is `sshd` (SSH Daemon).

### Basic SSH Commands

1. **Connecting to a remote server**:
    ```bash
    ssh username@hostname
    ```
   This command connects to a remote server with the specified username.

2. **Specifying a port**:
    ```bash
    ssh -p port_number username@hostname
    ```
   By default, SSH uses port 22, but this command lets you specify a different port.

3. **Copying files over SSH**:
    - **scp (Secure Copy)**:
      ```bash
      scp local_file username@hostname:/remote/directory/
      scp username@hostname:/remote/directory/ local_file
      scp -r dir username@hostname:/remote/directory/  (copy entire dir & contents)
      ```
      This command copies a file from the local machine to the remote server.

    - **rsync**:
      ```bash
      rsync -avz local_directory username@hostname:/remote/directory/
      ```
      `rsync` is more efficient for transferring large files and directories, especially when only a few files have changed.
       - **a** for archive
       - **v** for verbose
       - **z** for compress
       - **h** for human readble
       - **--progress**  Show progress during transfer.
       - **--delete** Delete files in the destination directory that are not in the source directory.

4. **Method 1 - for key auth**
**Generating SSH keys**:
    ```bash
    ssh-keygen 
    ```
    ```bash
    ssh-keygen -t rsa
    ```
    This command generates a pair of SSH keys (public and private). By default, they are saved in the `~/.ssh` directory.

5. **Copying the public key to a remote server**:
    ```bash
    ssh-copy-id username@hostname
    ```
    This command copies the public key to the remote server, enabling passwordless login.

     (or)
 
    copy publickey from client to remote
    **``~/.ssh/id_rsa_pub ``**  to  **``~/.ssh/authorized_keys``**

### Configuration Files

1. **Client Configuration (`~/.ssh/config`)**:
   You can create a configuration file to simplify SSH commands. For example:
   specific server config
    ```
    Host myserver
        HostName hostname
        User username
        Port port_number
        IdentifyFile ~/.ssh/..
        Compress yes
        ControlMaster auto
    ```
   This allows you to connect with just `ssh myserver`.

   Common server config
    ```
    Host *
        ForwardAgent yes (frwd connection)
        ServerAliveInterval 60 ( keeps connection alive 60 sec)
        ServerAliveCountMax 3 
    ```

3. **Server Configuration (`/etc/ssh/sshd_config`)**:
   The SSH server configuration file. Common settings include changing the default port, disabling root login, and setting up authentication methods.

    # The default configuration file for OpenSSH server
    /etc/ssh/sshd_config
   
    ```
    Port 22      - Port number to listen on for SSH connection
    Protocol 2   - Protocol version (deprecated, OpenSSH 7.6+ only supports protocol 2)
    HostKey /etc/ssh/ssh_host_rsa_key  - (Host keys for protocol version 2)
    MaxAuthTries 6  - (Maximum number of authentication attempts per connection)
    LoginGraceTime 2m - (Time before a new login attempt is allowed after the previous one failed)
    PermitRootLogin prohibit-password  - (Permit root login with/without password or prohibit entirely)
    PasswordAuthentication yes  - ( Allow or disallow password-based authentication)
    PubkeyAuthentication yes - (Allow or disallow public key-based authentication)
    UsePAM yes  - (Use PAM (Pluggable Authentication Modules))
    Include /etc/ssh/sshd_config.d/*.conf - (Specify a file containing user-specific configuration)
    AllowUsers user1 user2 - (Allow user user1 user2)
    DenyUsers user3  - (AllowGroups group1 group2)
    DenyGroups group3
    Banner /etc/issue.net  - (Set banner message)
    AuthenticationMethods publickey,password - (Define the authentication methods allowed)
    PermitEmptyPasswords no - (Disable empty passwords)
    LoginGraceTime 2m  - (Disconnect clients that haven't authenticated after a specified time period)
    AllowUsers user@192.168.1.0/24  - (Allow/deny specific IP addresses or CIDR ranges)
    ```
   
### Security Tips

- **Disable root login**: Set `PermitRootLogin no` in `sshd_config`.
- **Use strong passwords or keys**: Ensure that passwords are strong and consider using key-based authentication.
- **Change the default port**: Use a non-standard port to reduce the likelihood of automated attacks.
- **Firewall rules**: Ensure that only trusted IPs can access the SSH port.

### Example Workflow

1. **Generate an SSH key pair**:
    ```bash
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```
    Follow the prompts to save the key in the default location and optionally add a passphrase.

2. **Copy the public key to the remote server**:
    ```bash
    ssh-copy-id username@hostname
    ```

3. **Connect to the remote server**:
    ```bash
    ssh username@hostname
    ```

4. **Transfer files**:
    ```bash
    scp local_file username@hostname:/remote/directory/
    ```

### Troubleshooting

- **Permission issues**: Ensure correct permissions on `.ssh` directory and key files (`chmod 700 ~/.ssh` and `chmod 600 ~/.ssh/id_rsa`).
- **Firewall and SELinux**: Make sure the firewall and SELinux settings allow SSH traffic.
- **Verbose mode**: Use `ssh -v username@hostname` to get detailed logs for troubleshooting connection issues.

