In Linux, the `groupmod`, `groupadd`, and `groupdel` commands are used for managing groups. These commands allow you to modify existing groups, create new groups, and delete groups, respectively. Here’s a detailed guide on how to use these commands:

### `groupadd`

The `groupadd` command is used to create a new group

**Example:**
Create a new group named `developers` with a specific GID:
```bash
sudo groupadd -g 1001 developers
```

### `groupmod`

The `groupmod` command is used to modify an existing group.

**Common Options:**
- `-g GID`: Changes the GID of the group.
- `-n new_groupname`: Changes the name of the group.

**Examples:**

1. **Change the GID of a Group:**
   ```bash
   sudo groupmod -g 2000 developers
   ```

2. **Rename a Group:**
   ```bash
   sudo groupmod -n newdevelopers developers
   ```

### `groupdel`

The `groupdel` command is used to delete a group.

**Example:**
Delete a group named `developers`:
```bash
sudo groupdel developers
```

### Managing Group Membership

In addition to creating, modifying, and deleting groups, you often need to manage the membership of these groups. Here are some useful commands for managing group memberships:

**Add a User to a Group:**

Example:
```bash
sudo usermod -aG developers john
```

**Remove a User from a Group:**

Example:
```bash
sudo gpasswd -d john developers
```

### Viewing Group Information

**View All Groups:**
```bash
cat /etc/group
```

**View the Groups a User Belongs To:**
Example:
```bash
groups john
```

**View Detailed Group Information:**
```bash
getent group groupname
```
Example:
```bash
getent group developers
```

