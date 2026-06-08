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

Finally, I used the server manager to install the active directory and domain services using the "Add roles and features" option under the manage tab. Adding the AD DS server role also requires a DNS server. I learned that this is because DNS essentially works as a organization or domain-wide map for where certain services are located. AD DS keeps SRV or service records which tell computers within a domain which server within a domain provides services such as authentication. For my VirtualBox setup this DC01 domain controller server will handle authentication for the other Windows machines that will be joined to the domain. So when someone attempts to login on one of those Windows clients, the client will ask DNS "Who/What server is the domain controller for *domain name that I am joined to*" and DNS will respond with the record that shows the name and IP of the DC01 machine. Then the client will send the login attempt/request to the domain controller, check company records for the user credentials that were entered, and allow them in if they match. 

<img width="1023" height="773" alt="image" src="https://github.com/user-attachments/assets/97300c64-a09a-4fda-a0c0-45eae781516e" />

After this installation I needed to finally promote the server to be the domain controller for the ADDS. To do this we simply use another setup wizard to promote the server to the main Domain Controller and restart the machine to apply the changes.

<img width="1019" height="733" alt="image" src="https://github.com/user-attachments/assets/daf7631d-9660-4c87-bba1-3c8fb0485508" />
The server manager now shows the new domain that I created and I have access to tools such as the active directory administrative center.

The next step is to use these new active directory tools to create our business structure. This way when we configure the new employee Windows client and join it to the domain we can simulate an employee setting up their new work account. Additionally, these organizational groups allow use to set up group policies that will 
<img width="751" height="522" alt="image" src="https://github.com/user-attachments/assets/466fd7c7-72bc-41ed-812e-8efd5d055b65" />

Within these Organizational Units I created 3 accounts. An admin account for myself that I can later use instead of the default admin account on the domain controller and two employee accounts that can be used later when setting up the employee machines.
<img width="751" height="307" alt="image" src="https://github.com/user-attachments/assets/0b28c6e4-9893-4495-ae17-d47ceb3a3d9f" />

My next step is to set up Group Policies for these new organizational units and the domain. At the domain level I applied password security policies so that all users on the domain have password security enforced.
<img width="818" height="576" alt="image" src="https://github.com/user-attachments/assets/b30f83ed-0e37-4abd-a7a9-207693f93804" />
<img width="779" height="253" alt="image" src="https://github.com/user-attachments/assets/d0e1a1a1-89e6-4800-93a8-a674746f3fca" />







