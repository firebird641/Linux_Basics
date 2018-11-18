# Linux Bash and Scripting Commands
## I/O Redirection
### Stream Numbers
0: STDIN is the standard Input

1: STDOUT is the standard Output

2: STDERR is the standard Error
### Redirection
~~~
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
~~~
command1 | tee output.txt | command2
~~~
## Lists
~~~
command ./{element1,element2,element3}
~~~
## Less Command
The less command shows the content of a file from the beginning.
## User Input
~~~
read variable1 variable2 variable3
~~~
## Arguments
### Number of arguments
~~~
$#
~~~
### Arguments
~~~
$0, $1, $2
~~~
## If-Statements
### if then
~~~
if [ condition ]
then
  statement
fi
~~~
### if then else
~~~
if [ condition ]
then
  statement1
else
  statement2
fi
~~~
## Operators
### Integer Comparison
~~~
-eq # equals
-ne # not equals
-gt # greater than
-ge # greater equal
-lt # lower than
-le # lower equal
~~~
### String comparison
~~~
= # is euqal to
== # is equal to
!= # is not equal to
< # less than
> # greater than
-z # is null (length of zero)
~~~
### Logical Operators
~~~
! # NOT
&& # AND
|| # OR
~~~
Examples:
~~~
command1 && command2
~~~
Runs command2 only if command1 returns exit code 0.
~~~
command1 || command2
~~~
Run command1 successfully otherwise run command2.
## Echo
### -e Flag
This enables the interpretation of \ codes.
Examples:
~~~
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
~~~
array=('element1' 'element2' 'element3')
~~~
### Outputting all elements
~~~
echo "${array[@]}"
~~~
### Outputting specific elements
~~~
echo "${array[0]}" # outputs 'element'
~~~
### Outputting indices
~~~
echo "${!array[@]}"
~~~
### Appending item to array
~~~
array=('element1' 'element2')
array[2]='element3'
~~~
### Remove item from array
~~~
array=('element1' 'element2')
unset array[1] # removes 'element2' from array
~~~
## While-Loops
~~~
while [ condition ]
do
  statement
done
~~~
## Until-Loops
~~~
until [ condition ]
do
  statement
done
~~~
## For-Loops
~~~
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
## File Permissions
### Users and Groups
Users have a name and a UID, unique ID.

Groups consist of multiple users and also have a name and a GID, group ID.
### Attribute String
~~~
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
~~~
4 = Read
2 = Write
1 = Execute
0 = No Rights
~~~
All numbers added together define the permission for a file or folder.
### Examples
~~~
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
## Find Command
### Permissions
~~~
find . -type -f -perm 0660 # Output all files that are readable and writeable for user and group
find . -type -f ! -perm 0777 # Output all file except those with 0777-Permissions
find . -type -perm 4777 # Output all files with setUID set
~~~
### Particular Users
~~~
find . -user alice
~~~
## Which, Whereis and Whatis
~~~
which command # outputs the pathnames where binaries are stored
whereis command # outputs the pathnames of files which whould be executed in current environment
whatis command # outputs description of command from manpages
~~~
## Creating users
~~~
useradd alice -m -s /bin/bash -g users

-m # automatically create home directory
-s <shell> # set default shell
-g <group> # default user group
-c "<comment>" # define comment
~~~
## Remove users
~~~
userdel -r alice

-r # delete home directory as well
~~~
## Group Management
~~~
groups # returns all groups connected to current user
cat /etc/group # returns all groups on system
groupadd mygroup # add a group named mygroup
gpasswd -a username groupname # adds user username to group groupname
gpasswd -d username groupname # deletes user username from group groupname
~~~
## .bashrc
Bashrc is being executed when a new shell or terminal session is opened.
## Alias
Alias defined shortcuts ('aliases') for commands.
~~~
alias shortname='command' # defines new alias
alias shortname # shows existing alias
unalias shortname # remove shortname alias
unalias -a # remove all aliases
~~~
## Watch
Recalls a command in regular time intervals.
~~~
watch -n 1 command
# executes command every second
~~~
## Head and Tail
Head returns first part of a file, while the tail command returns the last part
~~~
head -n 10 file.txt # shows first 10 lines of file.txt
tail -n 10 file.txt # shows last 10 lines of file.txt
tail -f file.txt # output appended data as the file grows
~~~
## wc
wc (Word Count) prints newline, word, and byte counts for each file.
~~~
wc file.txt
1  6  42 file.txt
# 1: lines
# 6: words
# 42: characters
~~~
## tar Archive Management
Packing Archives:
~~~
tar -cvf archive.tar.gz archive
~~~
Unpacking Archives:
~~~
tar -xvf archive.tar.gz
~~~
## Mounting Devices
### Mounting
~~~
mount /dev/sdX /mnt
mount -a # from fstab
~~~
### Unmounting
~~~
umount /mnt
umount -a # all
~~~
## fstab
fstab contains information for automatically mounting partitions. Contents of this file are split into columns for each line:
~~~
<file system>   # /dev/sda
<mount point>   # /mnt
<type>          # ntfs
<option>        # defaults
<dump>          # 0
<pass>          # 0
~~~
## Cronjobs
~~~
crontab -e # run cron as current user
sudo crontab -e # run cron as root
~~~
Then configure the cronjob in the text editor.
## tmux Terminal Multiplexer
Basics
~~~
tmux new # new tmux Session
ctrl+B : # open tmux Prompt
ctrl+B d # detach tmux Session
tmux ls # show active tmux Sessions
tmux attach-session -t 0 # attach tmux Session 0
tmux a # attach latest tmux session
tmux kill-session -t 1 # kill Session 1
~~~
Naming Sessions
~~~
tmux new -s mysession # create a tmux Session named 'mysession'
tmux a -t mysession # attach the tmux Session 'mysession'
## a == attach-session
~~~
Panes
~~~
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
## Links
### Hardlinks
### Symbolic Links
## Burning CDs/DVDs
## unmask-Bits
## Access Control Lists
## Linux Directory Structure
