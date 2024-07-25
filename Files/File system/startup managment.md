Managing startup processes in Linux involves controlling which services and applications start automatically when the system boots. Different Linux distributions and versions use different initialization systems, such as System V init, Upstart, and systemd. The most common system in modern Linux distributions is systemd.

### Startup Management with systemd

**systemd** is a system and service manager for Linux, providing a standard process for controlling what programs run when a Linux system boots up. Here’s how to manage startup processes using systemd:

#### Checking the Status of Services

- **List all services and their status:**
  ```sh
  systemctl list-units --type=service
  ```

- **Check the status of a specific service:**
  ```sh
  systemctl status <service_name>
  ```

#### Enabling and Disabling Services

- **Enable a service to start at boot:**
  ```sh
  sudo systemctl enable <service_name>
  ```

- **Disable a service so it does not start at boot:**
  ```sh
  sudo systemctl disable <service_name>
  ```

#### Starting and Stopping Services

- **Start a service immediately:**
  ```sh
  sudo systemctl start <service_name>
  ```

- **Stop a service immediately:**
  ```sh
  sudo systemctl stop <service_name>
  ```

- **Restart a service:**
  ```sh
  sudo systemctl restart <service_name>
  ```

- **Reload the configuration of a service without restarting:**
  ```sh
  sudo systemctl reload <service_name>
  ```

#### Checking Enabled Services

- **List all enabled services:**
  ```sh
  systemctl list-unit-files --type=service | grep enabled
  ```

#### Viewing Logs

- **View logs for a specific service:**
  ```sh
  journalctl -u <service_name>
  ```

### Startup Management with SysVinit

**SysVinit** is an older init system still used in some Unix-like operating systems. It uses scripts stored in `/etc/init.d/` to manage services.

#### Managing Services

- **Start a service:**
  ```sh
  sudo service <service_name> start
  ```

- **Stop a service:**
  ```sh
  sudo service <service_name> stop
  ```

- **Restart a service:**
  ```sh
  sudo service <service_name> restart
  ```

- **Check the status of a service:**
  ```sh
  sudo service <service_name> status
  ```

#### Enabling and Disabling Services

- **Enable a service to start at boot:**
  ```sh
  sudo update-rc.d <service_name> defaults
  ```

- **Disable a service so it does not start at boot:**
  ```sh
  sudo update-rc.d <service_name> disable
  ```

### Startup Management with Upstart

**Upstart** is an event-based init system used in some older Linux distributions like Ubuntu 14.04 and earlier.

#### Managing Services

- **Start a service:**
  ```sh
  sudo start <service_name>
  ```

- **Stop a service:**
  ```sh
  sudo stop <service_name>
  ```

- **Restart a service:**
  ```sh
  sudo restart <service_name>
  ```

- **Check the status of a service:**
  ```sh
  sudo status <service_name>
  ```

#### Enabling and Disabling Services

To control whether a service starts at boot, you usually modify or create a `.conf` file in `/etc/init/`.

### Custom Startup Scripts

To run custom scripts at startup, you can place them in specific directories depending on your init system:

#### systemd

1. **Create a service unit file**:
   ```sh
   sudo nano /etc/systemd/system/myscript.service
   ```

   - Example content:
     ```ini
     [Unit]
     Description=My Custom Script

     [Service]
     ExecStart=/path/to/your/script.sh

     [Install]
     WantedBy=multi-user.target
     ```

2. **Enable the service**:
   ```sh
   sudo systemctl enable myscript.service
   ```

3. **Start the service**:
   ```sh
   sudo systemctl start myscript.service
   ```

#### SysVinit

1. **Place the script in `/etc/init.d/`**:
   ```sh
   sudo cp myscript.sh /etc/init.d/myscript
   ```

2. **Make the script executable**:
   ```sh
   sudo chmod +x /etc/init.d/myscript
   ```

3. **Add the script to the default runlevels**:
   ```sh
   sudo update-rc.d myscript defaults
   ```

