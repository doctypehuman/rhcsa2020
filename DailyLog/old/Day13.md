# Day 13 
## 24-09-2020

### SSH continues

useful command to see who the users are that are logged in and what they are doing execute:

	w-f

Key Generation is an important part of the set up. It is done by executing 

	ssh-keygen

When executed, there are two keys that are generated. A public key and a private key. Both these keys are stored in ~/.ssh/

Before key based authentication can be used the public key needs to be copied to the destination. You can do this by executing

	ssh-copy-id user@hostname

Below are the steps that are required to set up authentication using the keys generated.

	ssh-keygen

	ssh-copy-id -i ~/.ssh/id_rsa.pub user@hostname

Another important part of using SSH is to prohibit root user from logging in. This step is taken as a precautionary step just in case someone guesses the password and gains access to the system. You can do this by editing the configuration file which is located at 

	/etc/ssh/sshd_config

In the configuration file you will need to change the setting to the below mentioned code

	PermitRootLogin no

To make this change effective you will need to restart the service. This can be done by executing

	systemctl restart sshd.service

Another step taken to increase the security is to only allow key based ssh login as root. This can be done by making the below change in the configuration file 

	PermitRootLogin without password

Yet another step to increase the security is to prohibit password authentication using SSH. This step is taken to pre-empt the possibility of a comprimised password. This can be done by making the below change in the configuration file. 

	PasswordAuthentication no 

### Analyzing and storing logs

Topics that will be covered in this section are as follows 
- System Log Architecture
- Review Syslog Files
- Review systemd journal entries
- Preserving systemd journal
- Maintaining accurate time

While these topics will be covered in this chapter, not all of them have been covered today. 

Logs are stored by default in 

	/var/log

The main commands that are used for analyzing and storing logs are 
- systemd
- journald
- rsyslog

A simple and effecient way of monitoring log files is by using the _tail_ command. The command can be used with _-f_ option . This option will continue to append any live logs /entries that are being made to the log file. 

		tail -f /path/to/file

To send a message to rsyslog that gets recorded in /var/log/boot.log execute

	logger -p local7.notice "log entry"

#### Finding Log Entries

Change rsyslog config to log all messages with severity debug to var/log/messages-debug by adding etc/rsyslog.d/debug.conf

	echo"*.debug/var/log/messages-debug" > /etc/rsyslog.d/debug.conf

Restart service

	systemctl restart rsyslog

Generate debug log message with logger

	logger -p user.debug"Test debug message"

#### Reviewing systemd Journal Entries
- Finding events with *journalctl*

__ systemd journal is stored in /run/log by default and its contents are cleared after a reboot __

journalctl shows full system journal starting with the oldest entry first.

To show 10 entries execute 

	journalctl -n 

To show 5 entries execute 

	journalctl -n 5

To show entries marked with certain priority 

	journalctl -p err

To show entries that are time specific 

	journalctl --since "YYYY-MM-DD" --until "YYYY-MM-DD"

Keywords such as _today , yesterday , tomorrow _ are also accepted.

	journalctl --since "yesterday" --unti "today"

Other options to search for lines relevant are 
- _comm ( Name of command )
- _EXE ( The path to the executable for the process )
- _PID ( Process ID )
- _UID ( The UID of the user running the process )
- _SYSTEMD_UNIT ( The systemd unit that started the process )

Ouput only systemd journal messages, execute 

	journalctl _PID=1

Display all systemd journal messages that originate from system.service started wit UID 81

	journalctl _UID=81

Output journal messages with priority *warning* and above

	journalctl -p warning

Query to show log events recorded in previous 30 minutes. Curent time 0900 hrs.

	journalctl --since 9:00:00 --until 9:30:00

Query to display the events originating from sshd service with system unit file sshd.service recorded since 9:00:00 this morning.

	journalctl --since 9:00:00 _SYSTEMD_UNIT="sshd.service"

End Of Day 
