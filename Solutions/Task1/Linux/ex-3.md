### Exercise 3: Managing Services and Automating Tasks

1. Install Nginx on your server and ensure the service is running.

**	sudo apt install nginx 
	sudo systemctl status nginx

2. Configure Nginx to start automatically on boot.

**	sudo systemctl enable nginx

3. Edit unit file for Nginx to print the current machine time whenever the service started

**	sudo systemctl edit nginx
	#add this line 
	ExecStartPre=/bin/sh -c 'echo "Nginx started at: $(date)" | systemd-cat -t nginx-start'
	
	#Explanation
	#The ExecStartPre directive allows you to specify commands that run before the main service command (ExecStart).
	#The command echo "Nginx started at: $(date)" generates a timestamp when the service starts.
	#systemd-cat is used to log this output to the systemd journal, making it easier to find in the logs.


4. Search for patterns in Nginx logs to extract lines that only contain '200' . (hint: use *cat* - *grep* commands)

**	cat /var/log/nginx/access.log | grep ' 200 '
