In systemd, "targets" are used to group units and manage the system state.   
They are similar to runlevels in traditional Unix-like systems. Here are the most important commands related to target management using `systemctl`:

### Viewing and Changing Targets

- **List all available targets**:
  ```bash
  systemctl list-units --type=target
  ```

- **Check the current default target**:
  ```bash
  systemctl get-default
  ```
  Example output:
  ```bash
  graphical.target
  ```

- **Set the default target**:
 
  Example:
  ```bash
  systemctl set-default multi-user.target
  ```

- **Change the current target** (similar to changing runlevels):

  Example:
  ```bash
  systemctl isolate multi-user.target
  ```

### Common Targets

- `graphical.target`: Sets up a graphical environment (equivalent to runlevel 5 in SysVinit).
- `multi-user.target`: Sets up a non-graphical multi-user environment (equivalent to runlevel 3 in SysVinit).
- `rescue.target`: Sets up a basic system with only essential services running, useful for rescue operations (similar to single-user mode).
- `emergency.target`: Starts the system in the most minimal environment, with only the system console available.
- `reboot.target`: Reboots the system.
- `poweroff.target`: Shuts down the system.

### Example Usage

- **Change to the graphical target**:
  ```bash
  systemctl isolate graphical.target
  ```

- **Change to the multi-user target**:
  ```bash
  systemctl isolate multi-user.target
  ```

- **Set the default target to multi-user**:
  ```bash
  systemctl set-default multi-user.target
  ```

- **Reboot the system**:
  ```bash
  systemctl isolate reboot.target
  ```

- **Power off the system**:
  ```bash
  systemctl isolate poweroff.target
  ```

### Checking Dependencies

- **Show the dependencies of a target**:
  ```bash
  systemctl list-dependencies <target>
  ```
  Example:
  ```bash
  systemctl list-dependencies graphical.target
  ```

### Creating Custom Targets

You can create custom targets by defining new unit files. For example:

1. **Create a custom target file**:
   ```bash
   sudo nano /etc/systemd/system/mycustom.target
   ```

2. **Define the target in the file**:
   ```ini
   [Unit]
   Description=My Custom Target
   Requires=multi-user.target
   AllowIsolate=yes
   ```

3. **Reload the systemd manager configuration**:
   ```bash
   sudo systemctl daemon-reload
   ```

4. **Set your custom target as the default**:
   ```bash
   sudo systemctl set-default mycustom.target
   ```
