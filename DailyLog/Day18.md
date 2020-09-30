# Day 18 
## 29-09-20
### 27 Days to go 

#### Installing and Updating Software Packages

Yum is the package manager. Commands for yum 

- yum help
- yum list 
- yum list 'http*'
- yum search 
- yum search all 'httpd'
- yum info httpd
- yum provides /var/html/www
- yum install httpd
- yum remove httpd
- yum update
- yum update httpd
- yum update kernel (Will install new kernel)
- yum list kernel (list installed and available kernel)
- To view the current kernel _uname -r_ gives release and version. For detailed info _uname -a_
- yum group list
- yum group list hidden
- yum group info "Group Name"

##### Markers used inn Group Listing 

- = Package is installed , was installed as part of the group
- + Package is not installed, will be if group is
- - Package is not installed, will not be if group is installed/updated
-   No marker. Package is installed but was not installed through the group

	yum group install "Group Name"

- Transaction history is available in _/var/log/yum.log_

	tail -5 /var/log/yum.log

- yum history 
- yum history info Step#

	yum history info 7

- yum history undo Step#

	yum history undo 7

---

##### Enabling Yum Repository

- Create a .repo file in the directory _/etc/yum.repos.d/_

The file should contain 
- URL of the repository
- Name 
- Whether to use GPG check
- URL of GPG Key 

_SAMPLE_
[EPEL]
name=EPEL 7 beta
baseurl1=Path to url of repo
enabled=1
gpgkey=///path to gpg key/..

To enable repo

	yum --enablerepo=PATTERN

---

##### Examining packages with _RPM_

RPM is a low level tool that can get info about the content of package files and installed packages from the database or package itself.

Usage 

	rpm -q yum 

To view all 

	rpm -q -a 

To view packaage file 

	rpm -q -p packagefile.rpm

To view file name 

	rpm -q -f /path/to/file

---

### Accessing Linux File System 

The process of adding a new file system to the existing directory tree is called _mounting_

The directory where the new file system is mounted is known as _mounting point_

Storage devices are represented by a special file type called block devices. Block device is stored in /dev

- sd_a_ first storage device
- sd_b_ second storage device 
- sd_c_ third storage device 
- sd_d_ fourth ... and so on 

- sda_1_ first partition of first storage device
- sda_2_ second partition of first sotrage device 
- sda_3_ third partition and so on 

To display overview of existing partitions with a file system on them and UUID of the file system as well as the file system used to format the partition 

	blkid 

To view storage utilization 

	df /root 

To view storage utilization in human readable form 

	df -h OR df -H

A file system can be mounted on an existing directory. The /mnt directory exists by default and can be used to mount. First create a sub-directory in it and use that as a mounting point. 


Mounting a file system

	mount /dev/vdb1 /mnt/mydata

Using UUID 

	mount UUID="UUID" /mnt/mydata

Unmounting a file system

	umount 

Unmounting is not possible if the mount point is accessed by a process. To check this use 

	lsof /mnt/mydata

Lsof lists all files and processes accessing them in the provided directory

Default location for accessing removable storage is 

	/run/media/<user>/<label>

End Of Day 
