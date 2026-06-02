# SOC-Analyst-Homelab
Homelab project to simulate an standard enterprise network being monitored by an SIEM tool/server and attacked by a Kali Linux machine

# 1) Setup

## 1.1 Download all of the necessary ISO files + Setup Virtualbox instances

In my homelab setup I will have a total of 5 machines. This includes a Windows Server 2022 Evaluation machine, 2 normal Windows "employee" machines (one on Windows 10 the other Windows 11), an attacker Kali Linux machine, and a Wazuh SIEM server. Before setting each of these up I gathered each of their ISO image files.

<img width="726" height="338" alt="image" src="https://github.com/user-attachments/assets/edbfeb8f-a883-4e99-91c8-a5ca4ee0b99d" />

After downloading each of the ISOs I configured each of the virtual machine instances with a default configuration for now that can be changed later depending on the resources needed. I also needed to re-enable virtualization in my BIOS because I previously disabled it.

<img width="951" height="722" alt="image" src="https://github.com/user-attachments/assets/72b0ad9d-367d-47c6-851a-fb631e42b510" />

## 1.2 Setup Windows Server 2022 Evaluation Machine

First I setup the Windows Server that is going to act as the administrative device using active directory and domain services. After downloading the OS and setting up the admin account for the Windows Server I was able to get to the Server Manager.

<img width="1026" height="772" alt="image" src="https://github.com/user-attachments/assets/f1267b05-c7c6-4992-92ba-1df9ddb2c97a" />

The first thing I did was rename the server to DC01 to make it identifiable as the Domain Controller within the lab. To apply these changes I had to restart.

<img width="402" height="467" alt="image" src="https://github.com/user-attachments/assets/20e46227-9294-420b-9aeb-4e21e4248fed" />

Next I wanted to configure the static IP of the internal facing NIC so I used the control panel to give it a static IP. I also configured the DNS server address to point back at that static IP as we are later going to use this server machine as a DNS server for the theoretical organization. Since I have 2 virtual network adapters in case I need to install something later, I needed to use the command prompt to cross reference the MAC addresses of each virtual network adapter with the VirtualBox manager using the "ipconfig /all" command. This allowed me to only set the static IP address for the internal network adapter.

<img width="400" height="454" alt="image" src="https://github.com/user-attachments/assets/255bc9cf-d140-4fae-97f4-6b80bdde2d05" />

The last step before setting up active directory was to check for Windows updates. Windows did find some updates so I went ahead and downloaded them then restarted the machine to install and apply them

Finally, I used the server manager to install the active directory and domain services using the "Add roles and features" option under the manage tab.




