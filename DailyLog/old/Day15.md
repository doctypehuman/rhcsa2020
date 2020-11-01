# Day 15

## 26-09-2020 

### 30 days to go

Before the next chapter was done, one last excercise regarding logs/journals.

Configure rsyslog by adding a rule to the newly configured file /etc/rsyslog.d/auth-errors.conf to log all security messages with priority level alert and higher to /var/log/auth-errors. Test the newly added log directive with logger.

- Add the directive to log authpriv.alert to syslog messages to /var/log/auth-errors file in /etc/rsyslog.d/auth-errors.conf. 

	echo"authpriv.alert /var/log/auth-errors" > /etc/rsyslog.d/auth-errors.conf

Restart syslog

	systemctl restart rsyslog

Monitor newly created file 

	tail -f /var/log/auth-errors

User logger to send message to the newly created file

	logger -p authpriv.alert "Test Message"

Check output in the terminal window where tail command is running.

### Managing RHEL Networking 

Show IP address 

	ip addr show

To see network performance 

	ip -s link show eth0

Ping to check connectivity

	ping google.com

To end the process 

	Ctrl+C

Simpler way to check ping is to specify the count with -c option. This has to be followed by a number.

	ping -c4 google.com

To trace the path to a remote host use tracepath OR traceroute

	traceroute (UDP default)

	traceroute -I (ICMP)

	traceroute -T (TCP)

The command _ss_ is used to display socket statistics similar to _netstat_

The various options for ss are mentioned below 

- -n Show numbers instead of names of interfaces and ports.
- -t Show TCP sockets
- -u Show UDP sockets
- -l Show only listening sockets
- -a Show all 
- -p Show the process using the sockets


Display current IP address and netmask for all interfaces 

	ip addr

Display the statistics for the interface eth0

	ip -s link show eth0

Display routing information

	ip route

Verify if the router is available 

	ping -c3 google.com

Show all the hops between local system and classroom.example.com

	tracepath classroom.example.com

Display the listening sockets for TCP 

	ss -lt


End Of Day 

