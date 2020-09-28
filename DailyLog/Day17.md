# Day 17
## 28-09-20
### 28 Days to go

Hostname configuration. Remaining excercises, sligh changes. 

Important note, to set hostname for ssh so that a name can be used instead of an IP Address.

Assign IP address and name in /etc/hosts

	vim /etc/hosts

Once this is done name of the machine can be used and not the IP Address.

#### Archiving and copying files between systems

The command that is used for archiving is 

	tar

To create an archive 

	tar cf test-archive.tar file1 file2 file3

	tar cf /root/test1-archive.tar /etc

The first command will archive the three files in the working directory where the command is executed.

The second command will archive the entire directory etc in the location /root/ with the name test1-archive.tar

Once archived to display the files in the archive

	tar ft test.archive.tar

To extract the archive

	tar xf test.archive.tar

_To preseve the permissions of an archived file option 'p' is used. 

	tar xpf test.archive.tar

Create a compressed tar archive 

z for gzip filename.tar.gz OR filename.tgz

j for bzip2 filename.tar.bz2

J for xz filename.tar.xz


Copying files between systems securely

The command scp is used for this purpose.

	scp -r /etc/yum.conf /etc/hosts user@host:/path/to/paste

The above command is used to transfer from local to remote. For remote to local execute

	scp -r user:host:/etc/yum.conf /etc/hosts /path/to/paste

Transfer files with SFTP. This command is used to transfer files securely between systems. 

	sftp user@host
	password
	sftp>
	sftp> mkdir test
	sftp> cd test
	sftp> put /etc/yum.conf
	exit

	sftp user@host
	password
	sftp>
	sftp> get /etc/hosts
	exit


Synchronizing files between systems 

	rsync

For a dry run which is advised 

	rsync -n

Command options for rsync are 

- -a archive mode 
- -v verbose mode
- -r recursively
- -l sync symbolic links
- -t sync timestamps
- -g preserve group ownership
- -H sync hard links
- -o preserve owner of files
- -A sync ACL
- -D synchronize device files

Sync two local folders 

	rsync -av /var/log /tmp

Sync folders between local and remote 

	rsync -av /var/log user@host:/tmp

Sync folder between remote and local 

	rsync -av user@host:/var/log /tmp

End Of Day 

