# Day 16 
## 27-09-2020
### 29 Days to go 

From the 16 chapters in RH124 I am in Chapter 11. Networking. The chapter is  spread over 40 pages and I think i will have to read this again. I am 80 % done with the chapter. 

I have no clue how RHEL completes both the courses RH124 and RH134 in 5 days ! 

#### Configuring networking with nmcli

Configuartion file for network managing are located in 

	/etc/sysconfig/network-scripts/

Display list of all connections 

	nmcli con show 

Display list of only active connections 

	nmcli con show --acitve

Specify connection name to show details 

	namcli con show "enp0s3"

Show device status

	nmcli dev status

#### Creating network connections with nmcli

When creating a new connection with nmcli, the order of arguments is important

1. Common arguments appear first, these include type and interface.
2. Specify any type specific arguments.
3. Specify IP Addresses, Prefix info, Gateway info. 

Multiple IP addresses can be specified for one device. Additional settings like DNS server are set as modifications once the connection is created. 

Create a new connection called default which will autoconnect as an ethernet connection on the eth0 device using DHCP.

	nmcli con add con-name "default" type ethernet ifname eth0 

Create a new connection called static and specify the IP Address and the Gateway. Does not autoconnect.

	nmcli con add con-name "static" type ethernet ifname eth0 autoconnect no ip4 172.25.9.10/24 gw4 172.25.9.254

The system will autoconnect with the DHCP connection at boot. Change to the static connection. 

	nmcli con up "static"

Change back to the DHCP connection 

	nmcli con up "default"

To disable device 

nmcli dev disconnect Devicename

To view type options 

	nmcli con add help

#### Modify network interfaces with nmcli

Existing connections can be modified with 

	nmcli con mod 

Examples of modification 

1. Turn off autoconnect

	nmcli con mod "static" autoconnect no

2. Specify a DNS server

	nmcli con mod "static" ipv4.dns 172.25.9.254

3. Some configurations can have a "+" "-" sign to add or remove values. Ex add another DNS server

	nmcli con mod "static" +ipv4.dns 8.8.8.8

4. Add a secondary IP address without a gateway

	nmcli con mod "static" +ipv4.address 10.10.10.10

5. Replace the static IP address and gateway

	nmcli con mod "static" ipv4.addresses "172.25.8.10/24 172.25.8.254"

Note: nmcli con mod will save the changes. To activate the change, the connection needs to be activated/re-activated.

Some commands for nmcli 

Device Status

	nmcli dev status

List all connections 

	nmcli con show 

List active connections 

	nmcli con show --active

Activate a connection 

	nmcli con up "ID/name"

Deactivate a connection. Connection will restart if autoconnect is yes. 

	nmcli con down "ID/name"

Bring down an interface and temp disable autoconnect

	nmcli dev dis <Device>

Disable all managed interfaces 

	nmcli net off

Add a connection 

	nmcli con add con-name "Name"

Modify a connection 

	nmcli con mod "Name/ID"

Delete a connection 

	nmcli con del "NAME/ID"

Example: Conver a system from DHCP to static configuration

1. View network settings 

	nmcli con show 

2. Display all configuration settings for active connection 

	nmcli con show enp0s3

3. Show device status

	nmcli dev status

4. Create a static connection with the same ipv4 address, network prefix and default gateway. Name the new connection static

	nmcli cond add con-name "static" ifname enp0s3 type ethernet ip4 172.25.9.11/24 gw4 172.25.9.254

5. Modify the connection to add DNS

	nmcli con mod "static" ipv4.dns 8.8.8.8

6. Display and activate the new connection 

	nmcli con show 

	nmcli con up static

7. Test the connectivity using the network address. Verify the address 

	ip addr show

8. Verify the gateway

	ip route

9. Ping the gateway

	ping -c4 172.25.9.254

10. Configure the original connection so that it does not start on reboot and the new connection starts on reboot. Verify the same. 

	nmcli con mod "enp0s3" autoconnect no 

	reboot

	nmcli con show --active

End Of Day 


