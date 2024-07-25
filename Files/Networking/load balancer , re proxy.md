Nginx is a powerful tool that can serve as both a reverse proxy and a load balancer. Here's how you can configure Nginx to perform these roles.

### **1. Nginx as a Reverse Proxy**

A reverse proxy forwards client requests to backend servers. This can help with load balancing, SSL termination, and caching.

#### **a. Basic Reverse Proxy Configuration**

**1. Install Nginx**

**On Debian-based systems:**
```sh
sudo apt-get update
sudo apt-get install nginx
```

**On Red Hat-based systems:**
```sh
sudo yum install nginx
```

**2. Configure Nginx**

Edit the Nginx configuration file or create a new configuration file in `/etc/nginx/sites-available/`.

**Example Configuration (`/etc/nginx/sites-available/reverse-proxy.conf`):**
```nginx
server {
    listen 80;

    # Define the server name
    server_name example.com;

    # Define the location block for the reverse proxy
    location / {
        # Pass requests to the backend server
        proxy_pass http://backend_server;

        # Set headers to pass original client information
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

**3. Create a Symbolic Link to Enable the Configuration**

```sh
sudo ln -s /etc/nginx/sites-available/reverse-proxy.conf /etc/nginx/sites-enabled/
```

**4. Test and Restart Nginx**

Test the configuration for syntax errors:
```sh
sudo nginx -t
```

Restart Nginx to apply the changes:
```sh
sudo systemctl restart nginx
```

### **2. Nginx as a Load Balancer**

A load balancer distributes incoming traffic across multiple backend servers to balance the load and increase availability.

#### **a. Basic Load Balancer Configuration**

**1. Edit Nginx Configuration**

Edit the Nginx configuration file or create a new configuration file in `/etc/nginx/sites-available/`.

**Example Configuration (`/etc/nginx/sites-available/load-balancer.conf`):**
```nginx
http {
    # Define the upstream servers
    upstream backend {
        # List of backend servers
        server backend1.example.com;
        server backend2.example.com;
        server backend3.example.com;
    }

    server {
        listen 80;

        # Define the server name
        server_name example.com;

        # Define the location block for load balancing
        location / {
            # Pass requests to the upstream servers
            proxy_pass http://backend;

            # Set headers to pass original client information
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
}
```

**2. Create a Symbolic Link to Enable the Configuration**

```sh
sudo ln -s /etc/nginx/sites-available/load-balancer.conf /etc/nginx/sites-enabled/
```

**3. Test and Restart Nginx**

Test the configuration for syntax errors:
```sh
sudo nginx -t
```

Restart Nginx to apply the changes:
```sh
sudo systemctl restart nginx
```

### **3. Advanced Load Balancer Configuration**

**a. Load Balancing Algorithms**

Nginx supports several load balancing algorithms. You can specify them in the `upstream` block.

- **Round Robin (default)**:
  ```nginx
  upstream backend {
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

- **Least Connections**:
  ```nginx
  upstream backend {
      least_conn;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

- **IP Hash**:
  ```nginx
  upstream backend {
      ip_hash;
      server backend1.example.com;
      server backend2.example.com;
  }
  ```

**b. Health Checks**

Nginx can also check the health of backend servers. However, this requires the `nginx-plus` version or a third-party module like `nginx_upstream_check_module`.

**c. SSL Termination**

You can also configure Nginx to handle SSL termination. Here’s a brief example:

**SSL Configuration Example**:
```nginx
server {
    listen 443 ssl;

    # Define SSL certificates
    ssl_certificate /etc/nginx/ssl/nginx.crt;
    ssl_certificate_key /etc/nginx/ssl/nginx.key;

    # Define the server name
    server_name example.com;

    # Define the location block for reverse proxy
    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### **Summary**

- **Reverse Proxy**: Forwards client requests to backend servers. Useful for SSL termination and caching.
  - **Nginx**: Configure `proxy_pass` in the `location` block.

- **Load Balancer**: Distributes traffic across multiple backend servers. Enhances performance and redundancy.
  - **Nginx**: Use the `upstream` block with load balancing algorithms.

Nginx's versatility makes it an excellent choice for both reverse proxy and load balancing. With these configurations, you can efficiently manage and distribute traffic to ensure high availability and performance.
