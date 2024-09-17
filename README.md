# Mini_Project_01 by Brady Katler

## Basic Network Configuration Guide
This guide will demonstrate how to create a Local Area Network (LAN) and connect it to another LAN to make a Wide Area Network (WAN). The final WAN can be used for people to communicate across offices or for a business with branches in multiple regions. This guide will be created for macOS users (specifically on Sonoma 14.5).

### Setting up a LAN
1. Choose end devices and necessary hardware (such as computers, routers, switches, etc)
2. Plug in switch and connect it to end devices using ethernet cables
3. Set an IP address for end devices
   1. Open System Settings
   2. Click Network on the sidebar
   3. Click on the LAN connection (Mine was called USB 10/100/1000 LAN)
   4. Click TCP/IP on the sidebar
   5. Set "Configure IPv4" to "Manually"
   6. Set "IP Address" to "10.96.8.194" and "Subnet Mask" to "255.255.255.192"
   7. Follow the same steps for other end devices on the network, but incrementing the IP address by 1 (10.96.8.195, 10.96.8.196, etc)
5. Test connection by pinging end devices using terminal/power shell
   1. In the top left corner of your mac, search for Terminal and open it
   2. Ping an IP address by typing ```ping #IP Address of different end device on LAN#```
   3. A successful reply will look like ```64 bytes from 17.253.144.10: icmp_seq=8 ttl=56 time=17.928 ms```

### Adding DNS
1. In the same network settings as above, select "DNS" on the left sidebar
2. Under "DNS Servers", select the "+" on the bottom left and add the IP address of the end device hosting the DNS server
3. Install and use NAMO (or other equivalent software) to host a local DNS server
4. Add a new host by pressing the "+" in the bottom left corner
5. Set "Host Name" to the website domain you want
6. Set "IP Address" to "Local IP address" (Assuming this is being configured on the end device hosting the DNS server. Otherwise, set it to "Individual IP address" and enter the IP Address of the host device.
7. Press Save to confirm


### Adding a Web Server
1. On the end device hosting the web server, install MAMP
3. Under "Web Server", select "Nginx" from the top bar
4. Click the "Start" icon in the top right hand corner
5. Create an index.html file in the main directory (accessed through /Applications/MAMP/htdocs)
6. Within the index.html file, put in the following html code: ```<DOCTYPE HTML><html><p>Website Text Here</p></html>```
7. To test that the Web Server and DNS server are active,have a different end device enter the domain name into their web browser and see if the webpage comes up.


### Communicating across LANs

1. Plug in router and connect to switch (make note of the port number you connect to)
2. Turn router ports on
3. Add IP address to the router
    1. Plug router into an end device using the console port (install drivers as needed)
    2. Enter configuration mode in Terminal by typing `enable` and `conf t`
    3. Enter the following commands to set the IP address:
        1. `int *Port number connected to switch*`
        2. `ip add (ip address and subnet mask)`
        3. `description #To *Switch #*`
        4. `no shut`
        5. `write memory`
        6. To verify the settings saved, enter ```sh start```      
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
    
  
