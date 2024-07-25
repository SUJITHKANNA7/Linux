Network troubleshooting on Linux involves diagnosing and fixing issues related to network connectivity, performance, and configuration. Below is a detailed guide on how to troubleshoot network issues on Linux using various tools and techniques.

### **1. Check Network Interfaces**

Use `ip` or `ifconfig` to check the status of network interfaces.

#### **Using `ip` Command**
```sh
# Display all network interfaces and their statuses
ip addr show

# Display brief interface status
ip link show
```

#### **Using `ifconfig` Command**
```sh
# Display all network interfaces and their statuses
ifconfig -a
```

### **2. Test Network Connectivity**

#### **Ping**

Use `ping` to test connectivity to another host or IP address.

```sh
# Ping an IP address
ping 8.8.8.8

# Ping a domain name
ping example.com
```

#### **Traceroute**

Use `traceroute` to trace the route packets take to a destination.

```sh
# Trace route to a domain
traceroute example.com

# Trace route to an IP address
traceroute 8.8.8.8
```

#### **MTR**

`mtr` combines the functionality of `ping` and `traceroute` for real-time network diagnostics.

```sh
# Run MTR to a domain or IP address
mtr example.com
```

### **3. Check Routing Tables**

Use `ip` to check the routing table and ensure correct routing configuration.

```sh
# Display the routing table
ip route show
```

### **4. Check DNS Configuration**

Verify DNS settings in `/etc/resolv.conf`.

```sh
# View DNS configuration
cat /etc/resolv.conf
```

Use `dig` or `nslookup` to test DNS resolution.

```sh
# Use dig to query a domain
dig example.com

# Use nslookup to query a domain
nslookup example.com
```

### **5. Check Network Interfaces and Configuration**

Verify that network interfaces are configured correctly and up.

```sh
# Show interface configuration
nmcli device status

# Check the status of NetworkManager
systemctl status NetworkManager
```

### **6. Monitor Network Traffic**

#### **Using `netstat`**

View network connections, routing tables, and interface statistics.

```sh
# Display network connections
netstat -tuln

# Display routing table
netstat -r
```

#### **Using `ss`**

`ss` provides more detailed information on network sockets.

```sh
# Display network sockets
ss -tuln
```

#### **Using `iftop`**

Monitor bandwidth usage on an interface.

```sh
# Run iftop to monitor network traffic
sudo iftop -ni eth0
```

### **7. Analyze Network Traffic**

#### **Using `tcpdump`**

Capture and analyze network packets.

```sh
# Capture packets on a specific interface
sudo tcpdump -i eth0

# Capture packets for a specific port
sudo tcpdump -i eth0 port 80
```

#### **Using `wireshark`**

`wireshark` provides a graphical interface for network packet analysis.

```sh
# Start wireshark (requires X11)
sudo wireshark
```

### **8. Check Firewall Rules**

Ensure that firewall rules are not blocking traffic.

#### **Using `iptables`**

```sh
# List current iptables rules
sudo iptables -L -v -n
```

#### **Using `firewalld`**

If `firewalld` is used:

```sh
# List active firewall rules
sudo firewall-cmd --list-all
```

### **9. Review System Logs**

Check system logs for network-related errors.

```sh
# View kernel messages related to networking
dmesg | grep -i network

# Check syslog for network-related entries
sudo tail -f /var/log/syslog
```

### **10. Common Issues and Fixes**

- **No Network Connectivity**: Ensure the network interface is up (`ip link set dev eth0 up`), check cables and connections, and verify IP configuration.
- **DNS Issues**: Ensure `/etc/resolv.conf` has the correct DNS servers and test with `dig` or `nslookup`.
- **Firewall Blocking**: Check firewall rules and ensure required ports are open.
- **Routing Problems**: Verify the routing table with `ip route` and check for correct routes.

### **Summary**

- **Interface Status**: Use `ip` or `ifconfig`.
- **Connectivity**: Use `ping`, `traceroute`, `mtr`.
- **Routing**: Check with `ip route`.
- **DNS**: Verify with `cat /etc/resolv.conf`, `dig`, and `nslookup`.
- **Traffic Monitoring**: Use `netstat`, `ss`, `iftop`.
- **Traffic Analysis**: Use `tcpdump`, `wireshark`.
- **Firewall**: Check rules with `iptables` or `firewalld`.
- **Logs**: Review with `dmesg`, `syslog`.

By following these steps, you can systematically identify and resolve network issues on a Linux system.
