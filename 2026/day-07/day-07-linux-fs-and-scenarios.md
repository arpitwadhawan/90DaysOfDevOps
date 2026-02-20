**NOT COMPLETED YET
**
/
Purpose: The root directory is the top-level directory in Linux. Everything in the system starts from here.
UseCase: When need to understand the overall system structure or navigate to major system directories.

/home
Purpose: Contains home directories for regular users.
Example (ls -l /home):
vanisha ubuntu
UseCase: When want to access user files, projects, or personal scripts.

/root
Purpose: Home directory for the root (superuser) account.
Example (ls -l /root):
.bashrc  scripts/
UseCase: When logged in as root and need to manage system-level configurations or scripts.

/etc
Purpose: Contains system-wide configuration files.
Example (ls -l /etc):
passwd  ssh/  systemd/
UseCase: When need to modify service configurations, SSH settings, or system parameters.

/var/log
Purpose: Stores system and application log files. Very important for debugging.
Example (ls -l /var/log):
syslog auth.log nginx/
UseCase: When troubleshooting server issues, checking authentication problems, or debugging services.

/tmp
Purpose: Stores temporary files created by applications and users.
Example (ls -l /tmp):
systemd-private-*  temporary files
UseCase: When we need to store short-lived files or test scripts that are not permanent.

/bin
Purpose: Contains essential command binaries required for basic system functionality.
Example (ls -l /bin):
ls   cp  mv
UseCase: When you want to understand where core system commands are stored.

/usr/bin
Purpose: Contains user-level command binaries and applications.
Example (ls -l /usr/bin):
python3  git  nano
UseCase: When want to check installed software or locate executable programs.

/opt
Purpose: Used for optional or third-party software installations.
Example (ls -l /opt): google/  custom-app/
UseCase: When you want to install third-party tools like custom applications or enterprise software.
