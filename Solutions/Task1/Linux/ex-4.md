### Exercise 4: Network Configuration and Troubleshooting

1. Check the current IP address of your machine.

**	ifconfig or ip addr show	


2. Modify the DNS resolve settings to use ```1.1.1.1``` DNS server.

**	sudo nano /etc/resolv.conf #to open the configration file 
	#change the nameserver to be 1.1.1.1 instead of whatever 
	nameserver 1.1.1.1

3. Use ping and traceroute to verify the connection to www.google.com.


**	ping www.google.com
	sudo apt install traceroute #if you don't have it
	traceroute www.google.com
	#I found a problem with traceroute www.google.com so I used the command traceroute 8.8.8.8


4. Allow only incoming traffic to ```(http/https/ssh)``` services using firewall-cmd/UFW (depend on your machine).

**	sudo ufw enable
	sudo ufw allow http
	sudo ufw allow https
	sudo ufw allow ssh

