# Linux Documentation

by firebird641

## Nano

Nano is a simple Linux Console Text / Script Editor. Run it using the **nano** command.

## Cat

With cat you can show the content of files.

~~~bash
cat file.txt
~~~

## List Files

~~~bash
ls # show files in current directory
ls -l # list files in current directory
ls -la # list all files in current directory
~~~

## Copy, Move, Rename and Delete

~~~bash
# Copy
cp file1 file2
# Rename / Move
mv file1 file2
# Delete
rm file
rm -r directory # recursively remove
~~~

## Directory Structure Commands

~~~bash
/ # root directory
~ # current users home directory
./ # current directory
~~~

## Change Directory

~~~bash
cd /home/user/ # go to /home/user/
~~~

## Chroot

Chroot allowes you to change the root directory. This means you can set up a folder as a virtual environment for example (this is used when installing Arch Linux). To run commands inside the chroot directory you need to have all necessary files inside the jail. You can also run commands in a chroot:

~~~
chroot /home/user/directory command
~~~

## Fakeroot

Fakeroot creates a environment that simulates root privileges on a command. It fooles the command process that it runs as root.

## File Extensions

Linux does not know any file extensions. It determines the type of a file by the file header. Use whatever you want.

## Special Chaining Operators

~~~bash
apt update & apt dist-upgrade -y & # Backgrounds the Update commands
sleep 10 ; wall "Hello World" # send Message "Hello World" to all users after 10 Seconds
rm -rf !(*.html) # delete all files except *.html
~~~

## Autocomplete

When typing a command you can press the TAB-Key to let the system automatically complete your input if possible.

## Console Shortcuts

There are 6 tty Consoles on any Linux System. If it runs run a Desktop Manager, it is on the 7th Console. You can Access the Consoles with the Keyboard Shortcut:

~~~bash
Strg + Alt + F1-F7
~~~

## APT

APT (Advaned Packaging Tool) is a Linux Package Manager. It is used to Install / Remove / Update Software Packages for Debian-based Distributions like Ubuntu, Linux Mint and others.

~~~bash
apt update # Update Software List (check for updates)
apt dist-upgrade # Update Software based on Software List
apt install gimp # Install Package "GIMP"
apt search python # Search for Package "python"
apt remove firefox # Remove the Package "Firefox"
apt autoremove # Remove unnecessary Packages automatically
apt -f install # Install unmet dependencies
dpkg --configure -a # Complete Update/Upgrade Process if it has been interrupted
dpkg -i package.deb # Install the Debian Package "package.deb"
~~~

## Services

Services can be configured using the service command.

~~~bash
service --status-all # show status of all services
service networking restart # restart network service
service gdm start # start service gdm
service ssh stop # stop SSH service
~~~

## Networking

Here are some useful networking commands:

~~~bash
ifconfig -a # Show Status of all Interfaces
ip link # show all Network Interfaces
ip addr # Show interface IP/MAC-Addresses
netstat -tulpn # show Services listening on TCP/UDP Ports
nslookup google.com # resolve Google.com using the systems DNS Server
traceroute google.com # do a traceroute on google.com
~~~

The Network Interfaces can be configured in the **/etc/network/interfaces** file.

~~~bash
# DHCP Interface Example
auto eth0
iface eth0 inet dhcp
# Static Interface  Example
auto eth1
iface eth1 inet static
	address 192.168.0.1
	netmask 255.255.255.0
	gateway 192.168.0.1
	dns-nameservers 1.1.1.1
~~~

## Script Execution

When writing a script you want to execute with the console (./script), you need to specify the program that is being used to run the script. The following example is the first line of a python script.

~~~bash
#!/usr/bin/python
~~~

## mkpasswd

~~~bash
mkpasswd -l 16 # generates a passwort of length 16
~~~

## iptables

iptables is a low-Level IP-Filtering Firewall.

## arptables

arptables is a low-Level ARP-Filtering Firewall.

## dd

The disk dump command allowes you to create images from block devices or write images to block devices.

~~~bash
dd if=source of=target # clones from source to target
~~~

## sync

Sync writes any data buffered in memory to the disk. Useful if there is an unexpected halt of the system or before removing an external data stroage medium.

## I/O Redirection

### Stream Numbers
0: STDIN is the standard Input

1: STDOUT is the standard Output

2: STDERR is the standard Error
### Redirection
~~~bash
command 2> error.log # Redirects Error Output to error.log
command &> file.log # Redirects Output and Error to file.log
command > file.log 2>&1 # same as above
command 2>&1 # Redirects STDERR to STDOUT
command 2> errors.txt 1> output.txt # Redirects Error and Output to different files
command < file.txt # Redirects the default input STDIN to command
command << file.txt # Redirects the input from file to STDIN sequencially
command1 | command2 # Redirects output of command1 to command2
~~~
## Tee
This command allows you to write command output to a file and also redirect it to the STDOUT. Normally it is being used in a pipe.
~~~bash
command1 | tee output.txt | command2
~~~
## Grep

grep looks for Text.

~~~bash
cat text.txt | grep Hello # search for "Hello"
grep -v Hello ./text.txt # prints all lines that do not contain "Hello"
~~~

## Locate

Very fast method to find files by their name. It uses a Search Database called mlocate.

~~~bash
locate file.txt # prints out all paths to files calles "file.txt"
locate -c file.txt # prints the number of results
sudo updatedb # updates the search database (mlocate)
~~~

## Lists

~~~bash
command ./{element1,element2,element3}
~~~
## Less

The less command shows the content of a file from the beginning.

## Echo

Echo allowes you to print Strings to the STDOUT. You can combine it with Pipes and pass it to other files.

~~~bash
echo "Hello World."
~~~

## Wall

Wall sends a message to all users.

~~~bash
wall "Hello. System Shutdown in 30 seconds." ; shutdown -h -t 30
~~~

## Talk

Talk let's you chat with logged in users. Install using apt.

~~~bash
talk customuser
~~~

## User Input

~~~bash
read variable1 variable2 variable3
~~~
## Arguments
### Number of arguments
~~~bash
$#
~~~
### Arguments
~~~bash
$0, $1, $2
~~~
## If-Statements
### if then
~~~bash
if [ condition ]
then
  statement
fi
~~~
### if then else
~~~bash
if [ condition ]
then
  statement1
else
  statement2
fi
~~~
## Operators
### Integer Comparison
~~~bash
-eq # equals
-ne # not equals
-gt # greater than
-ge # greater equal
-lt # lower than
-le # lower equal
~~~
### String comparison
~~~bash
= # is euqal to
== # is equal to
!= # is not equal to
< # less than
> # greater than
-z # is null (length of zero)
~~~
### Logical Operators
~~~bash
! # NOT
&& # AND
|| # OR
~~~
Examples:
~~~bash
command1 && command2
~~~
Runs command2 only if command1 returns exit code 0.
~~~bash
command1 || command2
~~~
Run command1 successfully otherwise run command2.
## Echo
### Escape Code Flag
This enables the interpretation of \ escape codes.
Examples:
~~~bash
\b # backspace
\c # suppress newline
\n # newline
\r # carriage return
\t # tab (horizontal)
\v # tab (vertical)
\\ # backslash
~~~
## Arrays
### Definition
~~~bash
array=('element1' 'element2' 'element3')
~~~
### Outputting all elements
~~~bash
echo "${array[@]}"
~~~
### Outputting specific elements
~~~bash
echo "${array[0]}" # outputs 'element1'
~~~
### Outputting indices
~~~bash
echo "${!array[@]}"
~~~
### Appending item to array
~~~bash
array=('element1' 'element2')
array[2]='element3'
~~~
### Remove item from array
~~~bash
array=('element1' 'element2')
unset array[1] # removes 'element2' from array
~~~
## While-Loops
~~~bash
while [ condition ]
do
  statement
done
~~~
## Until-Loops
~~~bash
until [ condition ]
do
  statement
done
~~~
## For-Loops
~~~bash
# Elements from array
for element in array
do
  statement
done

# Outputs from command
for output in $(command)
do
  statement
done
~~~
## Functions

~~~bash
# declaring a function
print_something () {
	echo Hello I am a function
}
# calling a function
print_something
# declaring a function with arguments
print_something () {
	echo Hello $1
}
# calling a function with arguments
print_something Test
~~~

## File Permissions

### Users and Groups
Users have a name and a UID, unique ID.

Groups consist of multiple users and also have a name and a GID, group ID.
### Attribute String
~~~bash
d rwx r-x ---
1 2   3   4

# 1: Type
# 2: User
# 3: Group
# 4: Everyone
~~~
#### First Element (1 Character)
d = Directory

b = Block Device

c = Character Device

s = Socket

f = Pipeline

\- = File
#### Second to Fourth Element (3 Characters each)
r = Read Permission

w = Write Permission

x = Execution Permission

\- = No Right
### Octal Numbers
~~~bash
4 = Read
2 = Write
1 = Execute
0 = No Rights
~~~
All numbers added together define the permission for a file or folder.
### Examples
~~~bash
# No Rights: 0 / ---
# Executable: 1 / --x
# Writeable: 2 / -w-
# Readable: 4 / r--
# Executable + Writeable: 3 / -wx
# Executable + Readable: 5 / r-x
# Readable + Writeable: 6 / rw-
# Readable + Writeable + Executable: 7 rwx
~~~
### Special Rights
setUID: Run executable with the rights of the owner, not the one who is executing it (Octal 4).

setGID: Run executable with rights of the group, not the one of the executing group (Octal 2).

stickyBit: Only owner of the file can remove or rename the file (Octal 1).

## chmod

Sets the file permissions for a file or directory.

~~~bash
chmod +x file.sh # make file.sh executable
~~~

## chown

Sets the owner of a file or directory.

~~~bash
chown -R user:user ./directory/ # sets user "user" and group "user" as the owner of the directory
~~~

## Find
### Permissions
~~~bash
find . -type -f -perm 0660 # Output all files that are readable and writeable for user and group
find . -type -f ! -perm 0777 # Output all file except those with 0777-Permissions
find . -type -perm 4777 # Output all files with setUID set
~~~
### Particular Users
~~~bash
find . -user alice
~~~
## Which, Whereis and Whatis
~~~bash
which command # outputs the pathnames where binaries are stored
whereis command # outputs the pathnames of files which whould be executed in current environment
whatis command # outputs description of command from manpages
~~~
## Creating users
~~~bash
useradd alice -m -s /bin/bash -g users

-m # automatically create home directory
-s <shell> # set default shell
-g <group> # default user group
-c "<comment>" # define comment
~~~
## Remove users
~~~bash
userdel -r alice

-r # delete home directory as well
~~~
## Group Management
~~~bash
groups # returns all groups connected to current user
cat /etc/group # returns all groups on system
groupadd mygroup # add a group named mygroup
gpasswd -a username groupname # adds user username to group groupname
gpasswd -d username groupname # deletes user username from group groupname
~~~
## Bashrc
.bashrc is being executed when a new shell or terminal session is opened. You can find it as a hidden file in every user directory.
## Alias
Alias defined shortcuts ('aliases') for commands.
~~~bash
alias shortname='command' # defines new alias
alias shortname # shows existing alias
unalias shortname # remove shortname alias
unalias -a # remove all aliases
~~~
## Watch
Recalls a command in regular time intervals.
~~~bash
watch -n 1 command
# executes command every second
~~~
## Head and Tail
Head returns first part of a file, while the tail command returns the last part
~~~bash
head -n 10 file.txt # shows first 10 lines of file.txt
tail -n 10 file.txt # shows last 10 lines of file.txt
tail -f file.txt # output appended data as the file grows
~~~
## wc
wc (Word Count) prints newline, word, and byte counts for each file.
~~~bash
wc file.txt
1  6  42 file.txt
# 1: lines
# 6: words
# 42: characters
~~~
## tar Archive Management
Packing Archives:
~~~bash
tar -cvf archive.tar.gz archive
~~~
Unpacking Archives:
~~~bash
tar -xvf archive.tar.gz
~~~
## fstab
fstab contains information for automatically mounting partitions. Contents of this file are split into columns for each line:
~~~bash
<file system>   # /dev/sda
<mount point>   # /mnt
<type>          # ntfs
<option>        # defaults
<dump>          # 0
<pass>          # 0
~~~
## Cronjobs
~~~bash
crontab -e # run cron as current user
sudo crontab -e # run cron as root
~~~
Then configure the cronjob in the text editor.
## tmux Terminal Multiplexer
Basics
~~~bash
tmux new # new tmux Session
ctrl+B : # open tmux Prompt
ctrl+B d # detach tmux Session
tmux ls # show active tmux Sessions
tmux attach-session -t 0 # attach tmux Session 0
tmux a # attach latest tmux session
tmux kill-session -t 1 # kill Session 1
~~~
Naming Sessions
~~~bash
tmux new -s mysession # create a tmux Session named 'mysession'
tmux a -t mysession # attach the tmux Session 'mysession'
## a == attach-session
~~~
Panes
~~~bash
ctrl+B " # split Pane horizontally
ctrl+B % # split Pane vertically
ctrl+B ARROW_KEY # Switch between Panes
ctrl+B : # go to the tmux Console
ctrl+B resize-pane -D 2 # Resize Pane down by 2 lines
# U: up
# D: down
# L: left
# R: right
~~~
## Symbolic Links
Symbolic Links are Files that point to other files.

~~~bash
ln -s target link_name
~~~

## Formatting block devices

~~~bash
mkfs.ext4 /dev/sda1 # format /dev/sda1 with ext4
~~~

## Boot Process

### Simplified Boot Process 

- BIOS runs the Bootloader
- Bootloader loads Kernel into Memory and starts it
- Kernel initializes services and drivers
- Kernel mounts / (root filesystem)
- Kernel starts **init** Program (PID 1)
- **init** starts Rest of System Processes

### Kernel Initialization

- CPU Inspection
- Memory Inspection
- Device Bus and Device Discovery
- Auxiliary Kernel Subsystem Setup
- Mount Root FS
- Start Userspace

## GRUB Bootloader

GRUB = Grand Unified Bootloader

Press "e" to view the Bootloader Config for the current Boot Option.

### GRUB Command Line

Startup: Press C inside the Boot Menu.

~~~bash
ls # list Devices
ls -l # more detailed device list
echo $root # determine GRUB root
ls ($root)/boot # go to /boot directory
set # view all current GRUB variables
~~~

### GRUB Configuration

File Path: /boot/grub/grub.cfg

**Do not edit grub.cfg directly! Use grub-mkconfig.**

/etc/grub.d provides shell scripts for grub-mkconfig.

~~~bash
grub-mkconfig # prints the configuration to the stdout
grub-mkconfig -o /boot/grub/grub.cfg # same as above but writes it to grub.cfg
~~~

### GRUB Installation

~~~bash
grub-install /dev/sda # install to /boot/grub
grub-install --boot-directory=/mnt/boot/ /dev/sdc # install to /mnt/boot
~~~

## Userspace Basics

### Intro to init

init is the first process of a linux system to start, with PID = 1. It executes all other processes.

Init Implementations:

- System V init: Traditional old version
- systemd: Standard for most distros
- Upstart: Ubuntu init (prior v15.04)

### Runlevels

Runlevels control the execution of Processes and Daemons.

~~~bash
0: Shutdown. Dismount Partitions. Close Network Connections.
1: Single-User Runlevel. Only Hard Drives and Filesystems are active.
2: Single-User Mode. No Network. Only local Resources.
3: Local Multi-User Mode. Network Init (Debian). Local Resources.
4: Not defined.
5: Graphical User Interface is starting.
6: Reboot. Close Network Connections. Dismount Partitions.
~~~

### Changing Runlevels

~~~bash
init <runlevel> # = 1-6
~~~

### systemd

Systemd Startup:

- systemd loads config
- systemd determines boot goal (default.target)
- systemd loads boot goal dependencies
- systemd activates dependencies and default.target

### Units and Unit Types

A unit type is a systemd capability, like for example mounting Filesystems, Monitor Network Sockets, Run Timers. There are different Unit Types:

- Service Units (control daemons)
- Mount Units (control filesystem attachments)
- Target Units (control other Units)

## sudo

sudo allows you to run commands as root.

~~~bash
sudo passwd -d root # disable root login
~~~

Examples for /etc/sudoers:

~~~bash
root ALL = (ALL) ALL # Root may execute all commands with sudo
%administrator ALL = (ALL) ALL #  Group administrator my execute all commands with sudo
admin ALL = NOPASSWD: ALL # user admin may execute all programs without password input
user ALL = NOPASSWD: /usr/bin/python # user may execute /usr/bin/python without password input
~~~

## cmp

Compares two files and outputs all differences.

## curl

Allows you to transfer files from or to a server. It supports a wide range of network protocols: HTTP, FTP, HTTPS, LDAP, TELNET and others.

Example usage:

~~~bash
curl https://debian.org # get the main Debian webpage
curl http://10.10.0.123:8080 # get Ip 10.10.0.123 Port 8080
curl -o thatpage.html http://www.netscape.com # Store the web page to thatpage.html
curl -O www.haxx.se/index.html -O curl.haxx.se/download.html # fetch two files and store them with their remote name
curl -u name:passwd ftp://machine.domain:port/full/path/to/file # Download File from FTP Server with username and password
~~~

## Environment Variables

Environment Variables are Variables accessible by any shell and can for example define paths to executables or proxy configurations. They are different from Shell Variables.

Important commands:

~~~bash
KEY=value1:value2:value3 # Three values in one variable
KEY="value with spaces" # One String (with spaces) in a variable
env # print all set environment variables
echo $TEST_VAR # output value of TEST_VAR
export TEST_VAR # Convert Shell Variable into Environment Variable
export NEW_VAR="Testing export" # Set NEW_VAR as Environment Variable
export -n TEST_VAR # Convert Environment Variable to Shell Variable
unset TEST_VAR # Remove Shell Variable
~~~

## Killing Processes

You can either kill a process by it's UID (Unique Identifier) or by it's name:

~~~bash
kill 1234 # kill Process with ID 1234
kill -SIGTERM 3139 # kill Process 3139 with SIGNTERM
killall python # kill python
~~~

## man

Shows the manpages for a package installed on the system.

## Mounting devices

~~~bash
mount -l # list mounted devices
mount /dev/sda1 /mnt/mountpoint # mount /dev/sda1 to /mnt/mountpoint
umount /dev/sda1 # dismount device /dev/sda1
umount /mnt # dismount mountpoint /mnt
mount -a # mount all from fstab
umount -a # dismount all
~~~

## ping

Send ICMP Ping to a Machine by IP or Hostname.

## Poweroff and Reboot

~~~bash
poweroff # poweroff the machine
reboot # reboot the machine
~~~

## ssh

~~~bash
ssh user@host[:port] # connect to server
ssh -D user@host[:port] # connect to server and create SOCKS Proxy
ssh -N user@host[:port] # connect but do not open a shell
~~~

## uname

Shows System Information like:

- Kernel name
- Hostname
- Processor Type
- Platform
- Kernel Version

## wget

Downloads files from HTTP/HTTPS/FTP Servers.

~~~bash
wget https://cdimage.parrotsec.org/parrot/iso/4.5.1/Parrot-security-4.5.1_amd64.iso # Download ISO
~~~

## whoami

~~~bash
whoami # returns the current user name
~~~

## File System Structure

- / (root directory)
- /bin (Essential user command binaries)
  - Binary Executables
  - Linux Commands
  - ping, grep, ...
- /boot (Boot Loader)
  - initrd
  - grub config files
  - vmlinuz
- /dev (Device Files)
  - sdX
  - ttyX
  - usbX
- /etc (System Configuration Files)
  - Configfiles
  - startup and shutdown shell scripts
- /home (User Home Directories)
  - user files
  - bashrc
  - local configuration files
- /lib (Shared Libraries)
  - libraries for /bin
  - libraries for /sbin
  - Shared Object Files
- /media (Removable Media)
  - cdrom
  - floppy
  - HDDs
  - USB Sticks
- /mnt (Mounted Filesystems)
  - temporarily mounted devices
  - manually mounted devices
- /opt (Application Software Packages)
- /sbin (System Binaries)
  - init, route, fsck
  - iptables, reboot, fdisk, ifconfig, swapon
- /srv (Data for System Services)
- /tmp (Temporary Files)
- /usr (User Utilities and Applications)
  - libraries
  - documentation
  - source-code
- /proc (Process Information)
  - System Processes
  - System Resources (like uptime)

## Kernel Modules

Kernel Modules extend or are part of the Linux Kernel. Examples:

- WiFi Driver
- Sound Card Driver
- USB Device Driver

### Displaying loaded Modules

~~~bash
# two ways to display kernel modules
kmod list
lsmod
~~~

### modinfo - Showing Module Information

~~~bash
modinfo snd # show info for snd module

~~~

### modprobe - Loading and Unloading Modules

With modprobe you can load or unload kernel modules at runtime.

~~~bash
modprobe -n MODULENAME # simulate loading a module
modprobe -a MODULENAME # load a module
modprobe -r MODULENAME # unload module
modprobe --show-depends MODULENAME # show dependencies  of a module
~~~

### depmod - Module Dependencies

depmod can be used to recreate the file **/lib/modules/KERNELVERSION/modules.dep** when adding custom modules to the kernel.

### Loading modules automatically

To load a module automatically, just add it's name to **/etc/modules**

### Blacklisting

You can disallow a module to be loaded automatically by using a blacklist. You can find the blacklist under **/etc/modprobe.d**, normally inside the file **blacklist.conf**.

## Regular Expressions

~~~bash
. # matches a single character
\ # escape character
.* # matches any string
$ # end of a line
[] # range
| # logical OR
[^] # logical NOT
~~~

## Wildcards

~~~bash
? # single character
* # any number of characters
[a-c] # range of characters
{} # list of items
~~~

## sed

sed is the Linux Stream Editor. It is a non-interactive Text Editor for the Console. You can call sed like this:

~~~bash
sed SED_SCRIPT FILE # general sed command
~~~
