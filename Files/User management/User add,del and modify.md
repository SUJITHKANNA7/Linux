The `useradd`, `usermod`, and `userdel` commands are essential tools for managing user accounts in Linux.
### `useradd`

The `useradd` command is used to create a new user account.

**Basic Syntax:**
```bash
sudo useradd [options] username
```

**Common Options:**
- `-c "comment"`: Adds a comment, such as the user's full name.
- `-d home_directory`: Specifies the user's home directory.
- `-e expiration_date`: Sets the account expiration date.
- `-g initial_group`: Defines the user's initial login group.
- `-G additional_groups`: Lists additional groups the user belongs to.
- `-m`: Creates the user's home directory if it does not exist.
- `-s login_shell`: Specifies the user's login shell.
- `-u uid`: Sets the user's ID.

**Example:**
Create a new user with a specific home directory, shell, and add to additional groups:
```bash
sudo useradd -m -d /home/newuser -s /bin/bash -G sudo,users newuser
```

### `usermod`

The `usermod` command is used to modify an existing user account.

**Basic Syntax:**
```bash
sudo usermod [options] username
```

**Common Options:**
- `-c "comment"`: Changes the user's comment field.
- `-d home_directory`: Changes the user's home directory.
- `-e expiration_date`: Changes the account expiration date.
- `-g new_group`: Changes the user's primary group.
- `-G new_groups`: Changes the user's secondary groups.
- `-aG group`: Adds the user to additional groups without removing them from existing groups.
- `-l new_username`: Changes the username.
- `-s login_shell`: Changes the user's login shell.
- `-L`: Locks the user's account.
- `-U`: Unlocks the user's account.

**Example:**
Add an existing user to the `sudo` group and change their shell to `/bin/zsh`:
```bash
sudo usermod -aG sudo -s /bin/zsh username
```

### `userdel`

The `userdel` command is used to delete a user account.

**Basic Syntax:**
```bash
sudo userdel [options] username
```

**Common Options:**
- `-r`: Removes the user's home directory and mail spool.

**Example:**
Delete a user and their home directory:
```bash
sudo userdel -r username
```

### Practical Examples

1. **Create a new user with a home directory and specific shell:**
   ```bash
   sudo useradd -m -s /bin/bash newuser
   ```

2. **Modify a user to add them to additional groups:**
   ```bash
   sudo usermod -aG sudo,users newuser
   ```

3. **Change a user's home directory:**
   ```bash
   sudo usermod -d /new/home/dir newuser
   ```

4. **Lock a user account:**
   ```bash
   sudo usermod -L newuser
   ```

5. **Unlock a user account:**
   ```bash
   sudo usermod -U newuser
   ```

6. **Delete a user and their home directory:**
   ```bash
   sudo userdel -r newuser
   ```

By using these commands, you can effectively manage user accounts on a Linux system, ensuring proper access control and user administration.
