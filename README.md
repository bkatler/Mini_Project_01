# Mini_Project_01 by Brady Katler

## Basic Network Configuration Guide
This guide will demonstrate how to create a Local Area Network (LAN) and connect it to another LAN to make a Wide Area Network (WAN). The final WAN can be used for people to communicate across offices or for a business with branches in multiple regions. This guide will be created for macOS users (specifically on Sonoma 14.5).

### Setting up a LAN
1. Choose end devices and necessary hardware (such as computers, routers, switches, etc)
2. Plug in switch and connect it to end devices using ethernet cables
      * A switch allows for the connection of multiple devices in a LAN so they can communciate with each other
4. Set an IP address for end devices
   1. Open System Settings
   2. Click Network on the sidebar
   3. Click on the LAN connection (Mine was called USB 10/100/1000 LAN)
   4. Click TCP/IP on the sidebar
   5. Set "Configure IPv4" to "Manually"
      * IPv4 addresses were used instead of IPv6 because they are shorter and easier to manage for a small-scale LAN than IPv6
   7. Set "IP Address" to "10.96.8.194" and "Subnet Mask" to "255.255.255.192"
   8. Follow the same steps for other end devices on the network, but incrementing the IP address by 1 (10.96.8.195, 10.96.8.196, etc)
      * The lowest IP address (10.96.8.193 in this example) is usually saved for the router so it is easier to remember, as that address       is used a lot for setting default gateways
5. Test connection by pinging end devices using terminal/power shell
   1. In the top left corner of your mac, search for Terminal and open it
   2. Ping an IP address by typing ```ping #IP Address of different end device on LAN#```
   3. A successful reply will look like ```64 bytes from 17.253.144.10: icmp_seq=8 ttl=56 time=17.928 ms```
   
   Example of a successful ping:
  <img width="438" alt="Screenshot 2024-09-18 at 12 23 04 PM" src="https://github.com/user-attachments/assets/38ae1382-e5d3-49c5-990c-f422f582cb95">
.

  Example of an unsuccessful ping:
  
<img width="433" alt="Screenshot 2024-09-18 at 12 23 30 PM" src="https://github.com/user-attachments/assets/4df2c52b-c13f-4547-b8c5-4b93567d4d28">

   

### Adding DNS
* Adding a DNS server allows the user to enter a domain name rather than an IP address to access the web server
1. In the same network settings as above, select "DNS" on the left sidebar
2. Under "DNS Servers", select the "+" on the bottom left and add the IP address of the end device hosting the DNS server
3. Install and use NAMO (or other equivalent software) to host a local DNS server
4. Add a new host by pressing the "+" in the bottom left corner
5. Set "Host Name" to the website domain you want
6. Set "IP Address" to "Local IP address" (Assuming this is being configured on the end device hosting the DNS server. Otherwise, set it to "Individual IP address" and enter the IP Address of the host device.
7. Press Save to confirm
8. Repeat steps 4-7 using the DNS server's IP address for any end device you want to use to connect to the DNS server.


### Adding a Web Server
* While adding a Web Server isn't required, it remains another functional use case of the WAN
1. On the end device hosting the web server, install MAMP
3. Under "Web Server", select "Nginx" from the top bar
4. Click the "Start" icon in the top right hand corner
5. Create an index.html file in the main directory (accessed through /Applications/MAMP/htdocs)
6. Within the index.html file, put in the following html code: ```<DOCTYPE HTML><html><p>Website Text Here</p></html>```
7. To test that the Web Server and DNS server are active,have a different end device enter the domain name into their web browser and see if the webpage comes up.

<img width="660" alt="Screenshot 2024-09-18 at 12 39 54 PM" src="https://github.com/user-attachments/assets/4102e1b3-8d20-45c2-bb8b-bea9aafefe33">




### Communicating across LANs
* Adding a router allows two different LANs to communicate as it directs traffic.
1. Plug in router and connect to switch (make note of the port number you connect to) 
2. Turn router ports on by hitting the power switch on the back of the router
3. Add IP address to the router
    1. Plug router into an end device using the console port (install drivers as needed)
    2. Enter configuration mode in Terminal by typing `enable` and `conf t`
       * You're terminal should say Router(config)# on the bottom line as such:
         <img width="656" alt="Screenshot 2024-09-18 at 12 28 03 PM" src="https://github.com/user-attachments/assets/60463a19-c6e2-4792-9ab7-578ae6b89263">

    4. Enter the following commands to set the IP address:
        1. `int *Port number connected to switch*`
        2. `ip add 10.96.8.193 255.255.0.0`
        3. `description #To *Switch #*`
        4. `no shut`
        5. `write memory`
        6. To verify the settings saved, enter ```sh start```      
4. Add default gateway to all end devices and hosts (the IP of the router)
* Adding a default gateway allows for communciation across LANs because it directs incoming traffic through the router
6. Test connection by pinging end devices on a different LAN

## Configuration FAQ

### How do I remember all the IP addresses of each device?
   Two key strategies are to label all hardware (duct tape and a sharpie are a good simple method) and to store all IPs in a google sheet (EX: PC0 - Web Server - 10.96.8.195)

### Why can't I ping another end device on my LAN?
   Check all the basic issues: are all cables connected properly? Did you mistype the IP on the end device or in the ping command? Is a firewall on one of the end devices blocking pings? If none of those three are the issue, it is likely a hardware issue with one of the end devices

### Why can't I ping another device on a different LAN?
   First, I would recommend double checking that the device your pinging is connected to the router and has a default gateway. If the issue persists, try checking if you can ping the same device using another device on the same LAN and follow the steps above accordingly.

### Why can I ping the DNS server using the IP address but not the domain name?
   First, I would recommend double checking that the DNS settings saved on the DNS server. The other likely culprit is forgetting to add the DNS server as the default on the device you're using.

### Why am I struggling to connect to the router on my LAN?
   Double check that you are connecting the right port number connected to your switch. For example, on step 4.1 in "Communicating Across Lans", you should enter ```int g0/0``` if you're switch is connected to port 0/0, ```int g0/1``` if you're connected to port 0/1, and so on.
   

## Retrospective
   After having fully set up a LAN for the first time, I am very confident I could do it again much faster, especially now that I know the key obstacles that were blocking me.
   
   The biggest issue I faced was that my partners were using windows devices. Although I have used them before, I am inexperienced when it comes to troubleshooting nextwork issues on there, so it was difficult for me to contribute on some of the parts where they were struggling. Through a combination of trial and error along with google, we were able to resolve the issues, but it certainly added time onto the project. However, I now know how to solve these issues if they come up in the future.
   
   Another obstacle we faced was being careless about what port from the router we were connecting our switch to. This resulted in us being incapable of pinging across lans because on the first step, we configured to the wrong port. Professor Lontok found this issue for us when we were troubleshooting and we now know to be aware of it in the future.
   
   The final issue we faced was forgetting to save our progress on configuring the router. After entering the code on steps 4.1-4.4 of "Communicating across LANs", we neglected to add the ```write memory``` command which meant that none of the code we wrote the first time saved. We now know to always incldue this command and to double check by using ```sh start``` before exiting out.
   
   With the challenges for next time out of the way, I am confident I could set up a WAN quickly or troubleshoot a WAN someone else made. I feel confident that I understand the role specific networking devices play such as switches and routers, along with how to configure software such as a Web Server or DNS to provide functional use cases to my LAN. Most importantly, I feel like I have developed a general understanding of the basics of networking. This is extremely practical in settings such as my house, connecting end devices on a work environment, or even if I had to troubleshoot AWS at my work.
   
   I feel that struggling during troubleshooting could be the most impactful takeaway from this unit. I do not intend to enter a career that involves network engineering from the ground up, but having an understanding of how to troubleshooting networking problems is important for any career in the information technology field. Using strategies such as ping, checking default gateways, checking that integral cables are plugged in properly, and understanding DNS settings will certainly help my career in the future as I could potentially solve issues thay I or others are facing without needing to wait on IT or outside consulting.
   
   In the future, I believe I could improve this project by constantly checking my work as I went and incorporating new concepts I have learned from class. For instance, I would go very long stretches without checking my work while configuring our WAN. This was often as a mistake, as periodically pinging would have made troubleshooting far easier than checking at the very end of all my work. Rather than spending 20 minutes checking through DNS settings, I would have been better served doing occasional pings where I would have realized much faster that the issue was one of the cables being unplugged. This is why I chose to include verification steps at the end of each section of the step-by-step configuration guide, although an argument could be made that more checks should be put in place. I also feel confident that including DHCP onto this WAN would make it far easier to use - for myself and also new users. At the time we were closing out this project, we had not yet learned it which explains the omission. Having to check our google sheet for IP addresses and make sure that we entered them correctly was a blocker that ate up a surprising amount of time, so spending a short amount of time configuring this using DHCP woudld've resolved this issue permanently.
  
