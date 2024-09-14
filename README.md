# Mini_Project_01 by Brady Katler

## Basic Network Configuration Guide

### Setting up a LAN
1. Choose end devices and necessary hardware (such as computers, routers, switches, etc)
2. Plug in switch and connect it to end devices using ethernet cables
3. Set an IP address for end devices
4. Test connection by pinging end devices using terminal/power shell

### Adding DNS
1. Set an IP address for the DNS server to the same IP as the end device hosting the server
2. Install and use NAMO (or other equivalent software) to host a local DNS server
3. Add on a domain name

### Communicating across LANs

1. Plug in router and connect to switch (make note of the port number you connect to)
2. Turn router ports on
3. Add IP address to the router
    1. Plug router into an end device (install drivers as needed)
    2. Enter configuration mode in command line by typing `enable` and `conf t`
    3. Enter the following commands to set the IP address:
        1. `int *Port number connected to switch*`
        2. `ip add (ip address and subnet mask)`
        3. `description #To *Switch #*`
        4. `no shut`
        5. `write memory`      
4. Test connection by pinging end devices on a different LAN


