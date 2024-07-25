### **1. `dig`**

`dig` (Domain Information Groper) is a powerful tool for querying DNS records. It provides detailed information about domain names and DNS servers.

#### **Basic Commands**

- **Query a Domain Name**:
  ```sh
  dig example.com
  ```
  Retrieves DNS records for `example.com`.

- **Query a Specific DNS Server**:
  ```sh
  dig @8.8.8.8 example.com
  ```
  Queries `example.com` using Google's public DNS server at `8.8.8.8`.

- **Reverse DNS Lookup**:
  ```sh
  dig -x 93.184.216.34
  ```
  Finds the domain name associated with the IP address `93.184.216.34`.

- **Short Output**:
  ```sh
  dig +short example.com
  ```
  Provides a concise output with only the essential information.

- **Full Trace Output**:
  ```sh
  dig +trace example.com
  ```
  Shows the complete path of DNS resolution, including all steps from root servers to authoritative servers.

#### **Example Output**

```sh
$ dig example.com
; <<>> DiG 9.16.1-Ubuntu <<>> example.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 1

;; QUESTION SECTION:
;example.com.           IN  A

;; ANSWER SECTION:
example.com.    3600    IN  A   93.184.216.34

;; AUTHORITY SECTION:
example.com.    3600    IN  NS  ns1.example.com.

;; ADDITIONAL SECTION:
ns1.example.com. 3600 IN  A   93.184.216.35

;; Query time: 50 msec
;; SERVER: 8.8.8.8#53(8.8.8.8)
;; WHEN: Tue Jul 25 12:34:56 UTC 2024
;; MSG SIZE  rcvd: 89
```

### **2. `ping`**

`ping` is a network utility used to test the reachability of a host on a network and measure round-trip time for messages sent from the originating host to a destination computer.

#### **Basic Commands**

- **Ping a Domain or IP Address**:
  ```sh
  ping example.com
  ping 93.184.216.34
  ```
  Sends ICMP Echo Request packets to `example.com` or `93.184.216.34` and measures the response time.

- **Ping with a Specific Number of Packets**:
  ```sh
  ping -c 4 example.com
  ```
  Sends 4 ICMP Echo Request packets to `example.com`.

- **Ping with a Specific Packet Size**:
  ```sh
  ping -s 100 example.com
  ```
  Sends ICMP Echo Request packets with a payload size of 100 bytes.

#### **Example Output**

```sh
$ ping example.com
PING example.com (93.184.216.34) 56(84) bytes of data.
64 bytes from example.com (93.184.216.34): icmp_seq=1 ttl=56 time=30.1 ms
64 bytes from example.com (93.184.216.34): icmp_seq=2 ttl=56 time=29.8 ms

--- example.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 29.813/29.940/30.130/0.157 ms
```

### **3. `nslookup`**

`nslookup` (Name Server Lookup) is a command-line tool for querying DNS to obtain domain name or IP address mapping.

#### **Basic Commands**

- **Query a Domain Name**:
  ```sh
  nslookup example.com
  ```
  Retrieves DNS records for `example.com`.

- **Query a Specific DNS Server**:
  ```sh
  nslookup example.com 8.8.8.8
  ```
  Queries `example.com` using Google's public DNS server at `8.8.8.8`.

- **Reverse DNS Lookup**:
  ```sh
  nslookup 93.184.216.34
  ```
  Finds the domain name associated with the IP address `93.184.216.34`.

- **Interactive Mode**:
  ```sh
  nslookup
  ```
  Enters interactive mode, where you can issue multiple queries.

#### **Example Output**

```sh
$ nslookup example.com
Server:  8.8.8.8
Address:  8.8.8.8#53

Non-authoritative answer:
Name:    example.com
Address: 93.184.216.34
```

### **Summary**

- **`dig`**: Provides detailed and flexible DNS information. Useful for in-depth DNS troubleshooting and analysis.
- **`ping`**: Tests network connectivity and measures response time between hosts.
- **`nslookup`**: Offers a simpler interface for DNS queries and is useful for basic lookups and interactive querying.

Each tool has its own strengths and is used for different purposes in network diagnostics and DNS troubleshooting.
