# Linux Command Cheat Sheet

This book provides a comprehensive guide to various Linux commands categorized by topics. It serves as a quick reference for users who need to perform specific tasks on a Linux system.

## Table of Contents

1. [User Information](#user-information)
2. [File and Directory Commands](#file-and-directory-commands)
3. [File Permissions](#file-permissions)
4. [Networking](#networking)
5. [Installing Packages](#installing-packages)
6. [Disk Usage](#disk-usage)
7. [System and Hardware Information](#system-and-hardware-information)
8. [Search Files](#search-files)
9. [SSH](#ssh)
10. [Vi/Vim Commands](#vi-vim-commands)
11. [Top/Task Manager Command](#toptask-manager-command)
12. [Kill Command](#kill-command)
13. [History Command](#history-command)
14. [Curl Command](#curl-command)

## User Information

### `who`
Displays information about currently logged in users.

- **Login name of the user**
- **User terminal**
- **Date & Time of login**
- **Remote host name of the user**

```bash
$ who
sudheer :0 2019-08-04 01:21 (:0)
```

### `whoami`
Displays the current system’s username.

```bash
$ whoami
sudheer
```

### `id`
Displays the user identification (the real and effective user and group IDs) information.

```bash
$ id
uid=1000(sj) gid=1000(sj) groups=1000(sj),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),120(lpadmin),131(lxd),132(sambashare)
```

### `groups`
Displays all the groups to which the user belongs.

```bash
$ groups
sj: sj, adm, cdrom, sudo, dip, plugdev, lpadmin, lxd, sambashare
```

### `finger`
Checks the information of any currently logged in users, such as login time, tty (name), idle time, home directory, shell name, etc.

```bash
$ finger
Login     Name       Tty      Idle  Login Time   Office     Office Phone
sj        sj        *:0             Aug 28 01:27 (:0)
```

### `users`
Displays usernames of all users currently logged on the system.

```bash
$ users
sj
```

### `grep`
A powerful pattern searching tool to find information about a specific user from the system accounts file: /etc/passwd.

```bash
$ grep -i sj /etc/passwd
sj:x:1000:1000:sj,,,:/home/sj:/bin/bash
```

### `w`
Displays information about currently logged in users and what each user is doing.

```bash
$ w
 18:45:04 up  2:09,  1 user,  load average: 0.09, 0.07, 0.02
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
sj       :0       :0               01:27   ?xdm?   1:14   0.01s /usr/lib/gdm3/g
```

### `last` or `lastb`
Displays a list of last logged in users on the system.

```bash
$ last
sj       :0           :0               Fri Aug 28 01:27    gone - no logout
reboot   system boot  5.4.0-29-generic Fri Aug 28 01:27   still running
```

### `lastlog`
Finds the details of a recent login of all users or of a given user.

```bash
$ lastlog
Username         Port     From             Latest
root                                       **Never logged in**
daemon                                     **Never logged in**
```

## File and Directory Commands

### `pwd`
Prints the name of the present/current working directory starting from the root.

```bash
$ pwd
/home/sj/Desktop/Linux
```

### `ls`
Lists files or directories. Accepts flags or options that change how files or directories are listed in your terminal.

```bash
$ ls
bin dev lib libx32 mnt  
$ ls -ltr
drwxr-xr-x 2 sj sj 4096 May 14  2020 Videos
$ ls ~
Desktop    Downloads  Pictures  Sudheer    test   test.txt
```

### `mkdir`
Creates directories or folders.

```bash
$ mkdir ubuntu
$ mkdir -p dir1/dir2/dir3
$ cd dir1/dir2/dir3
```

### `rmdir`
Removes empty directories.

```bash
$ rmdir FolderName
$ rmdir FolderName1 FolderName2 FolderName3
$ rmdir -p a/b/c
```

### `rm`
Removes objects such as files, directories, symbolic links, etc., from the file system.

```bash
$ rm file_name
$ rm -f filename
$ rm -r myDir
$ rm -rf myDir
```

### `touch`
Creates, changes, and modifies timestamps of a file without any content.

```bash
$ touch file_name
$ touch file1_name file2_name file3_name
$ touch -a file_name
$ touch -m file_name
$ touch -r file2 file1
$ touch -t 1911010000 file_name
```

### `cat`
Creates single or multiple files, views content of files, concatenates files, and redirects output in terminal or files.

```bash
$ cat > file_name1.txt
Hello, How are you?
$ cat file_name1 file_name2
$ cat file_name1.txt | more
$ cat file_name1.txt | less
```

## File Permissions

### Ownership
Each file or directory has three types of owners:
1. **User**: Owner of the file who created it.
2. **Group**: Group of users with the same access permissions to the file or directory.
3. **Other**: Applies to all other users on the system.

### Permissions
Each file or directory has the following permissions for the above three types of owners:
1. **Read**: Authority to open and read a file and list its content for a directory.
2. **Write**: Authority to modify the contents of a file and add, remove, and rename files stored in the directory.
3. **Execute**: Authority to run the program in Unix/Linux.

### `chmod`
Changes the access mode of a file.

```bash
$ chmod ugo-rwx test.txt
$ chmod 764 test.txt
```

### `chown`
Changes the ownership and group of a file/directory.

```bash
$ chown user filename
$ chown user:group filename
$ chown John test.txt
$ chown John:Admin test.txt
```

### `chgrp`
Changes the group owner only.

```bash
$ chgrp group_name filename
$ sudo chgrp Administrator test.txt
```

## Networking

### `ifconfig`
Displays all network information (IP address, ports, etc.).

```bash
$ ifconfig -a
```

### `ping`
Sends an echo request to test the connection of a remote machine.

```bash
$ ping 10.0.0.11
```

### `hostname`
Displays the IP address of the current machine.

```bash
$ hostname -I
```

### `ip`
Displays IP address.

```bash
$ ip addr show
```

### `netstat`
Shows active or listening ports.

```bash
$ netstat -pnltu
```

### `whois`
Finds information about a domain, such as the owner of the domain, the owner’s contact information, and the nameservers used by the domain.

```bash
$ whois google.com
```

## Installing Packages

### `yum`
Installs, removes, and provides information about packages.

```bash
$ yum install package_name
$ yum info package_name
$ yum remove package_name
```

### `rpm`
Installs packages from local files.

```bash
$ rpm -i package_name.rpm
```

### From Source Code
```bash
$ tar zxvf sourcecode.tar.gz
$ cd sourcecode
$ ./configure
$ make
$ make install
```

## Disk Usage

### `du`
Checks the information of disk usage of files and directories on a machine.

```bash
$ du /home/
$ du -h /home/
$ du -sh /home/
$ du -ah /home/
$ du -ah --max-depth 2 /home/
$ du -ah --exclude="*.txt" /home/
$ du --help
```

## System and Hardware Information

### `uname`
Prints system information.

```bash
$ uname -a
$ uname -s
$ uname -r
$ uname -m
$ uname -o
```

## Search Files

### `grep`
Searches patterns in files.

```bash
$ grep "^hello" test.txt
$ grep -i "hELLo" text.txt
```

### `find`
Finds or searches files and directories by file name, folder name, creation date, modification date, owner, and permissions, etc.

```bash
$ find ./test -name test.txt
$ find ./test -name *.txt
$ find ./test -name test.txt -exec rm -i {} \;
$ find ./test -empty
$ find ./test -perm 664
$ find ./ -type f -name "*.txt" -exec grep 'World'  {} \;
```

### `whereis`
Locates binary or source files for a command.

```bash
$ whereis netstat
```

### `locate`
Finds files by name.

```bash
$ locate "*.txt" -n 10
```

## SSH

### `ssh`
Connects to a remote machine using IP address or machine name.

```bash
$ ssh 192.111.66.100
$ ssh test.remoteserver.com
$ ssh john@192.0.0.22
$ ssh john@test.remoteserver.com
$ ssh test.remoteserver.com -p 3322
```

### `ssh-keygen`
Generates SSH keys.

```bash
$ ssh-keygen -t rsa
```

### `ssh-copy-id`
Copies SSH keys to servers.

```bash
$ ssh-copy-id hostname_or_IP
```

### `scp`
Securely copies files over the SSH protocol.

```bash
$ scp test.txt test@10.0.0.64:/home/john/Desktop
```

### `vim`
Edits SSH configuration file.

```bash
$ sudo vim /etc/ssh/sshd_config
```

### `ssh`
Runs commands on a remote server.

```bash
$ ssh test.remoteserver.com mkdir NewDirectoryName
```

### `ssh`
Restarts SSH service.

```bash
$ sudo ssh service restart
$ sudo sshd service restart
```

## Vi/Vim Commands

### `vi` and `vim`
Text editors used in CLI for text editing tasks in many configuration files.

```bash
$ vi first.txt
```

### Basic Vi/Vim Commands

1. **Start with Vi Editor**
   - Create a new file or open an existing file using `vi filename` command.
   - Example:
     ```bash
     $ vi first.txt
     ```
   - To save the text and exit:
     ```bash
     :wq!
     ```
2. **Cursor movement**
   - Move cursor:
     ```bash
     h        # Move left
     j        # Move down
     k        # Move up
     l        # Move right
     ```
   - Jump one word:
     ```bash
     w        # Jump forwards to the start of a word
     W        # Jump forwards to the start of a WORD
     e        # Jump forwards to the start of a word
     E        # Jump forwards to the start of a WORD
     b        # Jump backwords to the start of a word
     B        # Jump backwords to the start of a WORD
     ```
   - Jump to start or end of a line or next line:
     ```bash
     ^        # Jump to the start of a current line
     $        # Jump to the end of a current line
     return   # Jump to the start of a next line
     ```
   - Move sides:
     ```bash
     Backspace # Move cursor one character to the left
     Spacebar  # Move cursor one character to the right
     H(High)   # Move cursor to the top of the screen
     M(Middle) # Move cursor to the middle of the screen
     L(Low)    # Move cursor to the bottom of the screen
     ```
   - Paging and Scrolling:
     ```bash
     Ctrl + f     # move forward one full screen
     Ctrl + b     # move backward one full screen
     Ctrl + d     # move forward half a screen
     Ctrl + u     # move backward half a screen
     ```

3. **Inserting Text**
   - Insert:
     ```bash
     i    # Insert text to the left of the cursor
     I    # Insert text at the beginning of a line
     ESC  # Exit insert mode
     ```
   - Append:
     ```bash
     a    # Insert(or Append) text to the right of the cursor
     A    # Insert(or Append) text at the end of a line
     ```
   - Open a line:
     ```bash
     o    # Open a line below the current cursor position
     O    # open a line above the current cursor position
     ```

4. **Editing Text**
   - Change word:
     ```bash
     cw
     ```
   - Change line:
     ```bash
     cc
     ```
   - Change line from specific character:
     ```bash
     C
     ```

5. **Deleting Text**
   - Deleting One Character:
     ```bash
     x
     X       # To delete one character before the cursor
     ```
   - Deleting a Word:
     ```bash
     dw
     ```
   - Deleting a Line:
     ```bash
     dd
     ```

6. **Cut, Copy & Paste**
   - Copy:
     ```bash
     yy      # Copy an entire line
     3yy     # Copy three lines
     yaw     # Copy word with trailing whitespace
     yiw     # Copy word without trailing whitespace
     y$      # Copy right of the cursor
     y^      # Copy left of the cursor
     ytx     # Copy text between the cursor and character
     yfx     # Copy text between the cursor and character
     ```
   - Cut:
     ```bash
     dd      # Cut entire line
     3dd     # Cut three lines
     d$      # Cut right of the cursor
     d^      # Cut left of the cursor
     ```
   - Paste:
     ```bash
     p
     ```
   - Visual Mode:
     ```bash
     v       # To select individual characters
     V       # To select the entire line
     Ctrl+v  # To select by block
     ```

7. **Exiting**
   ```cmd
   :w     # Write (save) the file, but don't exit
   :wq    # Write (save) and quit
   :wq!   # Force write (save) and quit
   :q     # Quit, but it fails if anything has changed
   :q!    # Quit and throw away for any changes
   ```

## Top/Task Manager Command

### `top`
Provides dynamic real-time viewing of the running system.

```bash
$ top
```

## Kill Command

### `kill`
Sends a signal to a process.

```bash
$ kill -s SIGTERM <process_id>
$ kill -l
$ kill -n <process_group_id>
$ kill -TERM <process_id>
$ kill -p <process_id>
```

## History Command

### `history`
Shows a list of previously issued commands.

```bash
$ history -c
$ history -d <offset>
$ history -a
$ history -r
$ history -n
$ history -w
$ history -s "<command>"
$ history -p <offset>
$ history -f <file>
```

## Curl Command

### `curl`
Transfers data to or from a server. Supports dozens of protocols, including HTTP, HTTPS, FTP, SFTP, Telnet, DICT, LDAP, LDAPS, FILE, IMAP, SMTP, POP3, RTSP, and RTMP.

```bash
$ curl http://example.com
$ curl -X POST http://example.com
$ curl -H "Content-Type: application/json" http://example.com
$ curl -X POST --data "key1=value1&key2=value2" http://example.com
$ curl -o output.html http://example.com
$ curl -O http://example.com/file.zip
```
