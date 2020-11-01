# Day 19
## 30-09-2020
### 26 Days to go 

#### Hard Links and Soft Links

User root can make these links.

Hard Link : Basically a new name for the file. A hard link either needs to have  different name or needs to be in another directory. Hard links pointing to the same file content needs to be on the same file system. If the orginial file from which the hard link was created is deleted, the link still functions. Create a hard link by executing 

	ln /path/to/original/file /path/to/link/file

Command expects the first argument to be the original file followed by one or more additional links.
Please see man ln for all forms of usage. 

All hard links referencing the same file have the same persmission.

	cd /tmp; mkdir links; cd links; echo "example" > link.text; ln /tmp/links/link.txt /tmp/links/example-hard-link.txt; ls -ll

---
Soft Link : Treat this as a shortcut icon that is generally used in Desktops. It is a specified file type that points to an existing file or directory. Soft links unlike hard links can point to files in different file systems. Create a soft link by executing 

	ln -s /path/to/original/file /path/to/link/file

When the original file is deleted, the soft link file ceases to function and is called a dangling link.

Soft linking a directory

	ln -s /etc /home/user/etc-soft-link

---

### Locate and Find files on the system

Extremely helpful and important functions for users and sysadmins. 

The two commands that are used for this are 

	locate
and 

	find

Locate: This command searches a predefined database and returns the resuslts instantly. 

Find: This command crawls the entire sustem or target directory in real time and then displays the results.


Locate Usage 

locate -i : makes the search case insensitive

locate -n5 : limits the search result to 5 results 

updatedb : the user has to update the database once before executing the command. It is updated automatically daily by the system but it is advised that the user updates the db before using the command.


Search Usage

The first argument is the directory that needs to be searched followed by various options to further finetune the search parameters such as type, size, last modified etc..

	find /home/user

	find /

To search for a file with a specific name 

	find / -name sshd_config

Using wild cards for name search 

	find / -name '*.txt'

	find / -name '*pass'

The first command will find all text files, the second command will find all files with the letters pass in the name. 

To perform case insensitive searches 

	find / -iname "*messages"

Finding files based on ownership

	find / -user student

	find / -group wheel

	find / -uid 1000

	find /- gid 30000

Finding files based on permission 

	find / -perm 764

Finding files based on size 

	find / -size 50M

This command will search and display files that are exactly 50 M in size. Use the markers "+" and "-" to find files greater or less than a particular size

	find / -size -10GB

	find / -size +5GB


Finding files that had their content changed/modified at a particular time 

	find / -mmin 10 

The unit used here is minutes. Use the markers "+" "-" to signal less than or more than 

	find / -mmin -10

	find / -mmin +30

Finding files by type 

Regular file 

	find / -type f

Directory 

	find / -type d

Soft Link 

	find / -type l

Block Devices 

	fidn / -type b

Finding Hard Links. Use the option -links followed by a number. It will then find files that have a certain hard link count. Use markers "+" "-" to look for links higher or lower than the number specfied in the command.
 

	find / -links 1

	find / -links +1

	find / -links -1

End Of Day 

