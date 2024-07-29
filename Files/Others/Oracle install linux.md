# Download InstantClient

```bash
mkdir -p /opt/oracle
cd /opt/oracle
wget https://download.oracle.com/otn_software/linux/instantclient/218000/instantclient-basic-linux.x64-21.8.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.8.0.0.0dbru.zip
```

# Download SQLPlus

```bash
wget https://download.oracle.com/otn_software/linux/instantclient/218000/instantclient-sqlplus-linux.x64-21.8.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.8.0.0.0dbru.zip
```

After you unzip sqlplus package, you will see both lib files and `sqlplus` command inside directory `instantclient_21_8`

```bash
ls -la /opt/oracle/instantclient_21_8
```

# Install Ubuntu dependency package

```bash
sudo apt install libaio1
```

# Autoload LD_LIBRARY_PATH

```bash
sudo sh -c "echo /opt/oracle/instantclient_21_8 > /etc/ld.so.conf.d/oracle-instantclient.conf"
sudo ldconfig
```

Add follow code to `~/.bashrc`

```bash
export LD_LIBRARY_PATH=/opt/oracle/instantclient_21_8:$LD_LIBRARY_PATH
export PATH=/opt/oracle/instantclient_21_8:$PATH
```

Then logout and login again or run `source ~/.bashrc` to reload `$PATH` environment

# install libaio libaray which is required by oracle instant client

```bash
sudo apt-get install libaio1  (Ubuntu,debian)
sudo yum install libaio (centos,fedora,RHEL)
```  

# Test connection

## Use SQLPlus

```bash
sqlplus username:password@host:port/service_name

# password promt (better)
sqlplus username@host:port/service_name
```
