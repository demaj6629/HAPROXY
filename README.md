# HAproxy as Load Balancer

# I will be simulating a system with one Load Balancer and to web-servers

# CentOS 7 servers in the virtualbox for remote connection to the servers

# SYSTEM SET UP

# I install a CENTOS 7 server and called it LoadBalancer
# Create two clones of the server and called them WEBSERVER1 nad WEBSERVER2
# Boot up the Three Servers (Loadbalancer, Webserver1 and Webserver2)
# Login to the three servers to check their IP using the IFCONFIG command
# Connect remotely to each servers ssh root@192.168.43.114, 192.168.43.29, 192.168.43.30
# Enter the root passoword for each

# Now let's cange the hostname of the servers
# Run the command nmtui, go to set hostname and press enter to validate

# Now I need to stop firewall and disable selinux
# Run the command systemctl status firewalld, I stopped it using the systemctl stop firewalld command
# I disabled the Selinux too using vi /etc/selinux/config command and rebooted the system

# Now mu webservers set up

# Firstly i made sure i installed apache on both servers
# yum install httpd -y
# systemctl start httpd
# systemctl enable httpd

# Next i modified the web content on my webservers
# cd /var/www/html
# vi index.html
# Enter some html code: <h1> Server 1 </h1>

# Next is my Loadbalancer set-up
# I installed HAPROXY
# yum install haproxy -y
# Check the daemon status: systemctl status haproxy
# Start the daemon: systemctl start haproxy
# Make it permanent: # system enable haproxy

# I then opened the configuration file

# cd /etc/haproxy/ 
# vi config
# At the frontend, i set the port to 8000
# i deactivated the static backend line by commenting it out

# I then used the ROUND-ROBIN scheduling algorithm

# I modified the server app lines to correspond with my webservers

# I restarted my Haproxy daemon using systemctl restart haproxy command

# I proceeded to my browser and entered the ip of my loadbalancer with the assigned port 192.168.43.114:8000

# As i kept on refreshing it kept on redirecting traffic to either webserver1 or webserver2 because of the round robin scheduling algorithm