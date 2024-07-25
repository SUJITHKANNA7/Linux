The `firewall-cmd` command is used with the `firewalld` service in Linux to manage firewall rules. When you use the `--info-service` option, you can obtain information about a specific service's firewall configuration.

For example, to get information about the `nginx` service, you would use the following command:

```sh
sudo firewall-cmd --info-service=nginx
```

### **Explanation of the Command**

- **`firewall-cmd`**: This is the command-line tool used to interact with `firewalld`, a firewall management tool.
- **`--info-service=nginx`**: This option asks `firewall-cmd` to provide information about the firewall rules associated with the `nginx` service.

### **Example Output**

The command will typically return information similar to this:

```sh
nginx
  ports:
    80/tcp
    443/tcp
  protocols:
    tcp
  services:
    http
    https
```

### **Breakdown of the Output**

- **`nginx`**: The name of the service.
- **`ports:`**: Lists the ports associated with the service.
  - **`80/tcp`**: HTTP port.
  - **`443/tcp`**: HTTPS port.
- **`protocols:`**: Lists the protocols used by the service.
  - **`tcp`**: Transmission Control Protocol.
- **`services:`**: Lists additional services or protocols associated with the service.
  - **`http`**: Refers to HTTP service.
  - **`https`**: Refers to HTTPS service.

### **Common Commands with `firewall-cmd`**

Here are some additional `firewall-cmd` commands you might find useful:

- **List all available services**:
  ```sh
  sudo firewall-cmd --list-services
  ```

- **Add a service to the firewall**:
  ```sh
  sudo firewall-cmd --add-service=nginx
  ```

- **Remove a service from the firewall**:
  ```sh
  sudo firewall-cmd --remove-service=nginx
  ```

- **List all open ports**:
  ```sh
  sudo firewall-cmd --list-ports
  ```

- **Add a port to the firewall**:
  ```sh
  sudo firewall-cmd --add-port=8080/tcp
  ```

- **Remove a port from the firewall**:
  ```sh
  sudo firewall-cmd --remove-port=8080/tcp
  ```

- **Make changes permanent**:
  ```sh
  sudo firewall-cmd --runtime-to-permanent
  ```

Using `firewall-cmd` allows you to manage and configure your firewall rules effectively on a Linux system using `firewalld`.
