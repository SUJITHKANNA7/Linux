
## Debian-based Distributions (Debian, Ubuntu)

### APT (Advanced Package Tool)
APT is the most commonly used package management tool for Debian-based systems.

- **Update Package List:**
  ```sh
  sudo apt update
  ```
  This command updates the package lists from the repositories to get information on the newest versions of packages and their dependencies.

- **Upgrade Packages:**
  ```sh
  sudo apt upgrade
  ```
  This command installs the newest versions of all installed packages.

- **Install a Package:**
  ```sh
  sudo apt install package_name
  ```
  Replace `package_name` with the name of the package you want to install.

- **Remove a Package:**
  ```sh
  sudo apt remove package_name
  ```
  This command removes a package but leaves its configuration files.

- **Remove a Package and Its Configuration Files:**
  ```sh
  sudo apt purge package_name
  ```
  This command removes a package along with its configuration files.

- **Search for a Package:**
  ```sh
  apt search package_name
  ```
  This command searches for packages in the repositories that match the provided name.

- **Show Package Information:**
  ```sh
  apt show package_name
  ```
  This command displays detailed information about a specific package.

### DPKG (Debian Package)
DPKG is the low-level package manager for Debian-based systems.

- **Install a .deb File:**
  ```sh
  sudo dpkg -i package_file.deb
  ```
  Replace `package_file.deb` with the path to your .deb file.


## Red Hat-based Distributions (Fedora, CentOS, RHEL)

### YUM (Yellowdog Updater, Modified)
YUM is the traditional package management tool for older Red Hat-based systems.

- **Update Package List:**
  ```sh
  sudo yum check-update
  ```
  This command updates the package lists from the repositories.

- **Install a Package:**
  ```sh
  sudo yum install package_name
  ```
  Replace `package_name` with the name of the package you want to install.

- **Remove a Package:**
  ```sh
  sudo yum remove package_name
  ```
  This command removes a package by name.

- **List Available Packages:**
  ```sh
  yum list available
  ```
  This command lists all available packages in the repositories.

### DNF (Dandified YUM)
DNF is the next-generation package manager for Red Hat-based systems, replacing YUM.

- **Update Package List:**
  ```sh
  sudo dnf check-update
  ```
  This command updates the package lists from the repositories.

- **Install a Package:**
  ```sh
  sudo dnf install package_name
  ```
  Replace `package_name` with the name of the package you want to install.

- **Remove a Package:**
  ```sh
  sudo dnf remove package_name
  ```
  This command removes a package by name.

- **List Available Packages:**
  ```sh
  dnf list available
  ```
  This command lists all available packages in the repositories.

### RPM (Red Hat Package Manager)
RPM is the low-level package manager for Red Hat-based systems.

- **Install an .rpm File:**
  ```sh
  sudo rpm -i package_file.rpm
  ```
  Replace `package_file.rpm` with the path to your .rpm file.



