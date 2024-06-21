### Documentation 

 **``ls --help``**       - for quick help about the commands and will come in pager (user arrow keys for navigation).  
 **``man jouranlctl``**  - Manual pages for the commands 

### apropos 
The apropos command is particularly useful when you know what functionality you need but not the **exact command or function name**.
You can search for multiple keywords by providing them as space-separated values.  
For example, to search for entries related to both "network" and "configuration":

```bash
apropos network configuration
```

### auto completion
Auto completion of the word , file names, keywords
```bash
ls +tab
```
```bash
ls +tab +tab
```
this will show all the arguemnts.

### Hostname
- Display the current hostname
```bash
hostname
```
- Set a new hostname
```bash
sudo hostname newhostname
```
- Display the IP address(es)
```bash
hostname -i
```
**Output: 192.168.1.100**

### Permanent Hostname Change:
Changing the hostname with the hostname command is temporary and will revert after a reboot.  
To make it permanent, you need to modify the appropriate configuration files:

- On systems using systemd, you can use hostnamectl:
```bash
sudo hostnamectl set-hostname newhostname
```
You may also need to edit /etc/hostname and /etc/hosts files for the changes to be reflected properly.

- Editing /etc/hostname:
```bash
sudo nano /etc/hostname
```
Change the contents to the new hostname and save the file.

- Editing /etc/hosts:
```bash
sudo nano /etc/hosts
```
Update the line starting with 127.0.1.1 to match the new hostname.
