<h1>Web Application Security Controls</h1>

[Project 2:Network Access Controls](https://github.com/user-attachments/files/17174727/dombrowiak_CST620_Project2.pdf)

<h2>Description</h2>
Understanding how to install a web server and enable secure communications with the web server.


<h2>Tools Utilized</h2>

- <b>Wampserver</b> 
- <b>Command Prompt</b>
- <b>Windows Defender Firewall</b>
- <b>Mate Terminal</b>
- <b>Notepad++</b>

<h2>Environments Used </h2>

- <b>Windows 10</b>
- <b>Kali Linux</b>

<h2>Project Documentation</h2>
<h3>Windows Firewall Best Practices</h3>
Implementing effective network access control with the Windows Firewall involves several key best practices to ensure the security of your network environment. First, establish a comprehensive firewall policy that outlines the rules and permissions for inbound and outbound traffic. This policy should be regularly reviewed and updated to reflect changes in your network architecture and security requirements.</br>
Segment your network into zones based on trust levels and apply appropriate firewall rules to each zone. For example, you may have separate zones for the internal network, DMZ (demilitarized zone), and external network. Limit the communication between these zones to only what is necessary for business operations, thereby reducing the attack surface (Fortinet, 2023).</br>
Utilize Windows Firewall's advanced security features such as advanced security rules, connection security rules, and authenticated firewall exceptions to enhance your network's defense capabilities. These features allow you to create more granular rules based on specific criteria such as application, user, or authentication status (Matarazzo, 2023).</br>
Regularly monitor and log firewall events to detect and respond to any suspicious or unauthorized activities. Analyzing firewall logs can provide valuable insights into potential security threats and help you fine-tune your firewall rules for better protection.</br>
Enable built-in Windows Firewall settings such as stealth mode, which helps conceal your network's presence from unauthorized scans and probes. Additionally, consider implementing IPsec (Internet Protocol Security) to encrypt network communications and authenticate the identity of communicating parties, further strengthening your network security posture.</br>
Lastly, educate your users about the importance of firewall security and provide training on how to recognize and respond to potential security threats. User awareness and vigilance are crucial to any effective network access control strategy. By following these best practices, you can maximize the effectiveness of the Windows Firewall in safeguarding your network against unauthorized access and malicious activities.</br>
<h3>Linux Firewall Best Practices</h3>
Implementing effective network access control with the Linux Firewall (IPTables) involves several key best practices to ensure the security of your network environment. First, develop a comprehensive firewall policy outlining rules for inbound and outbound traffic, regularly reviewing, and updating it to align with network changes and security needs.</br>
Segment your network into zones based on trust levels and apply appropriate firewall rules to each zone. This segmentation helps limit communication between zones, reducing the attack surface and enhancing network security (Landsberger, 2023).</br>
Utilize IPTables' advanced features such as stateful packet inspection, packet filtering, and Network Address Translation (NAT) to enhance your network defense capabilities. These features allow you to create precise rules based on criteria like source/destination IP addresses, ports, and protocols.</br>
Regularly monitor firewall logs and analyze firewall events to detect and respond to suspicious activities promptly. Log analysis provides valuable insights into potential security threats and helps fine-tune firewall rules for better protection.</br>
Implement additional security measures such as IPSet for managing large sets of IP addresses and SELinux (Security-Enhanced Linux) for enforcing mandatory access controls. These tools complement IPTables and strengthen your network's overall security posture (Red Hat, n.d.).</br>
Lastly, educate users about the importance of firewall security and provide training on recognizing and responding to potential security threats. User awareness and vigilance are critical components of an effective network access control strategy. By following these best practices, you can maximize the effectiveness of IPTables in safeguarding your network against unauthorized access and malicious activities.</br>

<h3>Windows Firewall Control Implementation and Testing</h3>

Running ‘nmap -Pn 10.11.71.4’ to view which ports are open. 
![image](https://github.com/user-attachments/assets/4b04166a-9b55-4ee4-9798-8adf0ebc29cf)

Initially pinging the Kali VM to see if the connection between the Windows VM and Kali was still accessible.
![image](https://github.com/user-attachments/assets/7c475064-1438-4f93-a0aa-5d631e9445da)

After inputting everything in Kali, I attempted to ping the VM again on Windows and the pings failed to go through.
![image](https://github.com/user-attachments/assets/a1d9a27e-b875-43ba-a3b8-8f509a637aa4)

<h3>Linux Firewall Control Implementation and Testing</h3>

Using the input ‘sudo iptables -L -v’ to see the current configuration of the iptables. It also shows that this is not secure because any packets can come through without a filter.
![image](https://github.com/user-attachments/assets/26142901-34d6-4452-ae67-bc20af245129)

Running the input ‘sudo iptables -A INPUT -i lo -j ACCEPT’ to allow traffic on the local host.
![image](https://github.com/user-attachments/assets/afa51738-56fb-45b4-9464-ea17c03f13c0)

Running the following: 
- iptables -A INPUT -p tcp --dport 22 -j ACCEPT
- iptables -A INPUT -p tcp --dport 80 -j ACCEPT
- iptables -A INPUT -p tcp --dport 443 -j ACCEPT
- iptables –L -v

![image](https://github.com/user-attachments/assets/3501767e-6b14-41e6-b66a-4e1c72462447)

Adding the access of the Windows VM with ‘iptables -R INPUT 2 -s 10.11.71.5 -p tcp --dport 22 -j ACCEPT
![image](https://github.com/user-attachments/assets/47f97709-eba7-4fce-b6c0-b3ebff47e566)

Running the below commands in Kali to change the rules in the iptables to deny the access of the Windows VM to Kali.
![image](https://github.com/user-attachments/assets/69f3e559-8ee9-4953-a9aa-ffb5919b17c9)

<h3>References</h3>
Fortinet. (2023). What Is a DMZ and Why Would You Use It? Fortinet. https://www.fortinet.com/resources/cyberglossary/what-is-dmz</br>
Landsberger, D. (2023, October 4). What Is Network Segmentation and Why It Matters? CompTIA. https://www.comptia.org/blog/security-awareness-training-network-segmentation</br>
Matarazzo, P. (2023, November 21). Windows Firewall overview - Windows Security. Learn.microsoft.com. https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/</br>
Red Hat. (n.d.). 4.2. SELinux and Mandatory Access Control (MAC) Red Hat Enterprise Linux 7 | Red Hat Customer Portal. Access.redhat.com. https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/virtualization_security_guide/sect-virtualization_security_guide-svirt-mac</br>
