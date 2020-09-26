# Day 14

## 25-09-2020

### Preserving the systemd journal 

- Be able to configure systemd-journal to store journal entries on disk rather on memory.

Be default systemd journal is kept in _/run/log/journal_. If _/var/log/journal_ exists the journal will log to that directory instead.

Advantage that data available at reboot. Disadvantage is that _logrotate_ will delete 10% of the data to save storage. This value can be changed in _/etc/systemd/journal.conf_

Systemd journal can be made persistent by executing the below commands.

Create dir _journal_ in the location _/var/log/_

	mkdir /var/log/journal

Ensure that the directory is owned by user root and group systemd-journal and has permission 2755

	chmown root:systemd-journal /var/log/journal

	chmod 2755 /var/log/journal

Send special signal USR1 as user root to systemd-journal process OR Reboot

	killall -USR1 systemd-journald

Since the system journal is persistent across reboots, execute

	journalctl -b

This can reduce the output by only showing log messages since the last boot of the system.

When debugging a system crash with persistent journal, it is ussually required to limit the journal query to the reboot before the crash happened. This can be done by attaching a negative number.

	journalctl -b -1

This command limits the output to the previous reboot.


#### Maintain Accurate Time


NTP (Network Time Protocol) is used to synchronize time in the machine. 

To show current overview of time related system setting, execute 

	timedatectl

To change current time and date settings, execute

	timedatectl set-time HH:MM:SS

Another option is to first confirm the timezone that you need. Find out the correct time zone by executing

	timedatectl time-zones

You can then choose the desired timezone to set the time. 

Inorder to disbale/enable NTP, execute 

	timedatectl set-ntp true/false

#### Configuring and monitoring Chronyd

The chronyd service keeps the ususally inaccurate local hardware clock (RTC) on track by synchronizing it to the local NTP servers.

You have to point the chronyd service to the local servers by editing the file

	vim /etc/chronyd.conf

	#Use public servers from the pool.ntp.org project
	server classroom.example.com iburst

Once this is done, the service needs to be restarted

	systemctl restart chronyd.service

In order to verify correct sync the command _chronyc_ needs to used. 

	chronyc sources -v

End Of Day.





