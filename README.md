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
4. Add default gateway to all end devices and hosts
5. Test connection by pinging end devices on a different LAN

## Configuration FAQ

### Recommended Practices
1. Label all hardware (duct tape and a marker works fine)
2. Record all IP addresses
3. Give the first IP address in a given set to the router

### Troubleshooting Checklist
1. Ensure all hardware is plugged in and turned on
2. Ensure all cables are plugged in securely
3. Check firewall settings to ensure that it is not blocking connections
4. Check for typos in IP addresses
5. Restart the needed device(s)
6. Verify connection using ping

## Retrospective

  Building a network reminded me a lot of building a PC like I did in high school: although all the different parts seem daunting at first, connecting and configuring them is simple to do with clear instructions. 
