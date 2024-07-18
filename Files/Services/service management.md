Here are the most important and commonly used `systemctl` commands:

### Service Management

- **Check the status of a service**:
  ```bash
  systemctl status <service-name>
  ```
  Example:
  ```bash
  systemctl status nginx
  ```

- **Start a service**:
  
  Example:
  ```bash
  systemctl start nginx
  ```

- **Stop a service**:
  
  Example:
  ```bash
  systemctl stop nginx
  ```

- **Restart a service**:

  Example:
  ```bash
  systemctl restart nginx
  ```

- **Reload a service’s configuration** (without stopping the service):

  Example:
  ```bash
  systemctl reload nginx
  ```

### Enable/Disable Services

- **Enable a service to start on boot**:
 
  Example:
  ```bash
  systemctl enable nginx
  ```

- **Disable a service from starting on boot**:

  Example:
  ```bash
  systemctl disable nginx
  ```

- **Check if a service is enabled**:

  Example:
  ```bash
  systemctl is-enabled nginx
  ```

### Mask/Unmask Services

- **Mask a service** (prevents the service from being started):
 
  Example:
  ```bash
  systemctl mask nginx
  ```

- **Unmask a service** (removes the mask):

  Example:
  ```bash
  systemctl unmask nginx
  ```

### Listing and Viewing Units

- **List all active units**:
  ```bash
  systemctl list-units
  ```

- **List all units, including inactive ones**:
  ```bash
  systemctl list-units --all
  ```

- **List failed units**:
  ```bash
  systemctl --failed
  ```

- **List unit files**:
  ```bash
  systemctl list-unit-files
  ```

- **List enabled unit files**:
  ```bash
  systemctl list-unit-files --state=enabled
  ```
  
