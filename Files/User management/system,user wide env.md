To manage environment profiles both system-wide and user-wide in Linux, you'll need to work with different sets of configuration files. Here are the distinctions and steps for each:

## System-wide Environment Profiles

### 1. `/etc/profile`
This file sets environment variables for all users at login.

1. Open `/etc/profile` with a text editor:
   ```bash
   sudo nano /etc/profile
   ```
2. Add the desired environment variables:
   ```bash
   export PATH=$PATH:/opt/myapp/bin
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
   ```
3. Save and close the file.

### 2. `/etc/profile.d/`
This directory contains scripts that set environment variables. These scripts are executed by `/etc/profile`.

1. Create a new script in `/etc/profile.d/`:
   ```bash
   sudo nano /etc/profile.d/myapp.sh
   ```
2. Add the environment variables:
   ```bash
   #!/bin/bash
   export PATH=$PATH:/opt/myapp/bin
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
   ```
3. Save the file and make it executable:
   ```bash
   sudo chmod +x /etc/profile.d/myapp.sh
   ```

### 3. `/etc/environment`
This file is specifically for setting environment variables that affect the entire system.

1. Open `/etc/environment`:
   ```bash
   sudo nano /etc/environment
   ```
2. Add the environment variables:
   ```bash
   PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/myapp/bin"
   JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
   ```
3. Save and close the file.

## User-wide Environment Profiles

### 1. `~/.profile`
This file sets environment variables for the individual user.

1. Open `~/.profile`:
   ```bash
   nano ~/.profile
   ```
2. Add the environment variables:
   ```bash
   export PATH=$PATH:/opt/myapp/bin
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
   ```
3. Save and close the file.

### 2. `~/.bashrc`
This file sets environment variables for the user when a new shell is opened (non-login shells).

1. Open `~/.bashrc`:
   ```bash
   nano ~/.bashrc
   ```
2. Add the environment variables:
   ```bash
   export PATH=$PATH:/opt/myapp/bin
   export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
   ```
3. Save and close the file.

## Applying Changes

### System-wide Changes
To apply changes made to `/etc/profile` or scripts in `/etc/profile.d/`, source the profile:
```bash
source /etc/profile
```
For changes in `/etc/environment`, a re-login or system restart is required.

### User-wide Changes
To apply changes made to `~/.profile` or `~/.bashrc`, source the respective file:
```bash
source ~/.profile
```
or
```bash
source ~/.bashrc
```
Alternatively, you can open a new terminal or re-login to see the changes.

Environment history in Linux typically refers to the recording and management of environment variables that have been set or modified over time. Linux does not inherently keep a history of environment variable changes, but you can implement mechanisms to track changes if needed.


### Viewing Command History

For viewing command history, including those that might modify environment variables, you can use the `history` command. This includes commands executed in the current shell.

1. **View History**
   - Run `history` to see a list of executed commands.
   - Search the history with `grep`:
     ```bash
     history | grep export
     ```

2. **Persistent History Across Sessions**
   - Ensure that your shell is configured to save history between sessions by setting appropriate options in your shell configuration files (`~/.bashrc`, `~/.bash_profile`, etc.):
     ```bash
     # Add to ~/.bashrc
     export HISTSIZE=1000
     export HISTFILESIZE=2000
     shopt -s histappend
     export PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
     ```
3. **print environment variables**
   ```bash
    env
   ```
By implementing these methods, you can effectively track and manage changes to environment variables over time, allowing for better monitoring and troubleshooting.
