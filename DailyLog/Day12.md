# Day 12 
## 23-09-20

Things are moving on. Some of the topics that I covered were :
- Controlling services and daemons
- SSH setup and use

### Controlling services and daemons

The main commands that were studied were systemctl and systemd

Basically check if the services are running /active /disabled /enabled on boot or otherwise. 

Also list all services / sockets / paths etc that are in the system and available. 

Listing unit files with systemctl 

	systemctl list-units --type=service --all

List all sockets active & inactive 
	systemctl list-units --type=sockets --all

Display status 
	systemctl status sshd.service

Confirm listed daemons are running
	ps -p PID

Determine if service is enabled 
	systemctl is-enabled sshd

Determine if service is active without displaying all info
	systemctl is-active sshd

List enabled/disabled states of all service units
	systemctl list-unit-files --type=service 

Verify process running 
	ps-up PID 

Stop service 
	systemctl stop sshd.service

Restart service 
	systemctl restart sshd.service

Reload service 
	systemctl reload sshd.service

_When using reload, the PID does not change, when using restart the PID changes_


### SSH Setup and Use

Since I am using Virtual machines, using SSH between the two was a little tricky. 
In system settings in one needs to use BRIDGE as the network inorder for the two machines to be able to speak with each other. 

Once that is done you need to find the IP address by 
	ip a
After this the command for ssh is 
	ssh user@ipaddress

In the home directory there will be a new .ssh directory that will be formed. Within that directory there will be a folder called _known_hosts_
In that folder the host key will be saved. 

I was not able to change the hostname yet, that is something that I plan on doing today and also key generation needs to be done. 

End Of Day. 





































