# SOC-Analyst-Homelab
Homelab project to simulate an standard enterprise network being monitored by an SIEM tool/server and attacked by a Kali Linux machine

## 1.1 Download all of the necessary ISO files + Setup Virtualbox instances

In my homelab setup I will have a total of 5 machines. This includes a Windows Server 2022 Evaluation machine, 2 normal Windows "employee" machines (one on Windows 10 the other Windows 11), an attacker Kali Linux machine, and a Wazuh SIEM server. Before setting each of these up I gathered each of their ISO image files.

<img width="726" height="338" alt="image" src="https://github.com/user-attachments/assets/edbfeb8f-a883-4e99-91c8-a5ca4ee0b99d" />

After downloading each of the ISOs I configured each of the virtual machine instances with a default configuration for now that can be changed later depending on the resources needed. I also needed to re-enable virtualization in my BIOS because I previously disabled it.

<img width="951" height="722" alt="image" src="https://github.com/user-attachments/assets/72b0ad9d-367d-47c6-851a-fb631e42b510" />
