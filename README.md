<h1>Web Application Security Controls</h1>

[Project 3: Web Application Security Controls](https://github.com/user-attachments/files/17174763/dombrowiak_CST620_Project3.pdf)

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
<h3>Web Application Security Best Practices</h3>
Ensuring robust security for web applications requires implementing a comprehensive set of best practices that address various potential vulnerabilities. One fundamental aspect is input validation and sanitization. Always validate and sanitize user inputs to prevent injection attacks such as SQL injection, cross-site scripting (XSS), and other forms of malicious data entry (Maury, 2023). Utilizing parameterized queries and prepared statements can significantly reduce the risk of SQL injection while employing encoding techniques and a Content Security Policy (CSP) can help mitigate XSS attacks. Additionally, input validation should be enforced on both the client and server sides to ensure comprehensive protection.</br>
Another critical best practice is the implementation of strong authentication and session management mechanisms. This includes using multi-factor authentication (MFA) to provide an additional layer of security beyond just usernames and passwords. Proper session management entails generating secure session IDs, using secure cookies, and setting appropriate session timeouts to prevent session hijacking (Gupta, n.d.). Employing secure, hashed passwords using algorithms like bcrypt, along with regular password strength assessments, helps safeguard against unauthorized access. Ensuring secure communication through HTTPS is also crucial, as it encrypts data transmitted between the client and server, preventing interception by malicious actors.</br>
Regular security testing and vulnerability assessments are vital for maintaining web application security. Conduct periodic penetration testing, code reviews, and automated vulnerability scanning to identify and address potential weaknesses. Keeping software and dependencies up to date is essential to protect against known vulnerabilities and exploits (InterSec, Inc., n.d.). Implementing a robust incident response plan allows for quick and effective action in the event of a security breach. Additionally, fostering a culture of security awareness within the development team through regular training and updates on the latest security threats and best practices can significantly enhance the overall security posture of the web application.</br>
<h3>Web Application Security Control Implementation and Testing</h3>

Accessing the Wampserver, by double-clicking the icon on the desktop.
![image](https://github.com/user-attachments/assets/9959d46f-8a1e-4e98-bab4-0448ef4f792b)

Accessing phpMyAdmin using the URL http://localhost/phpmyadmin.
![image](https://github.com/user-attachments/assets/46f257d2-9916-4d43-8745-246e4cb4217a)

Added the inbound rule for port 80.
![image](https://github.com/user-attachments/assets/26ec842e-1f3c-43d9-a2a2-cb18a57e7570)

Using Kali, I confirmed that the rule is set up and running properly by using nmap on my Windows VM.
![image](https://github.com/user-attachments/assets/c9722c28-40b3-4163-b939-ef4445d8c533)

I downloaded OpenSSL and created a certificate for secure communication with WAMP.
![image](https://github.com/user-attachments/assets/b8b2a885-ac34-4108-8d24-807ad2189c98)

I used the command ‘openssl req -new -x509 -nodes -sha1 -key private.key -out certificate.crt -days 36500’ and filled out the following information.
![image](https://github.com/user-attachments/assets/931dbbf9-92ab-4b14-a403-67f930ae48d0)

I updated the following by removing the pound symbol (#) next to the following in ‘httpd.conf’
- LoadModule ssl_module modules/mod_ssl.so
- Include conf/extra/httpd-ssl.conf
- LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
I updated the following sections in ‘httpd-ssl.conf’ 
- DocumentRoot "c:/wamp64/www"
- ServerName localhost:443
- ServerAdmin admin@example.com
- ErrorLog "${SRVROOT}/logs/error.log"
- TransferLog "${SRVROOT}/logs/access.log"
- SSLSessionCache "shmcb:${SRVROOT}/logs/ssl_scache(512000)"
- SSLCertificateFile "${SRVROOT}/conf/key/certificate.crt"
- SSLCertificateKeyFile "${SRVROOT}/conf/key/private.key"
- CustomLog "${SRVROOT}/logs/ssl_request.log"

After editing all of the above I restarted WAMP to make sure the connection is still established.
![image](https://github.com/user-attachments/assets/f0484c1d-9b8b-448e-8276-0c47654977fb)

Updated the following information in ‘httpd-vhosts.conf’
- SSLEngine on
- SSLCertificateFile "${SRVROOT}/conf/key/certificate.crt"
- SSLCertificateKeyFile "${SRVROOT}/conf/key/private.key

![image](https://github.com/user-attachments/assets/1147cb4d-2007-4b9c-9bbf-b740e63ad099)

I created a new inbound rule ‘WAMP 443’ while also disabling the original rule ‘WAMP 80’ making it a secure connection using HTTPS instead of port 80 being unsecured HTTP.
![image](https://github.com/user-attachments/assets/1b0b6520-6290-4313-a59e-e6a90c025ae4)

Restarted and double-checked the connection via Kali and Windows. Both are working correctly.
![image](https://github.com/user-attachments/assets/68920aa7-5461-40fb-be05-2025c32c7844)
![image](https://github.com/user-attachments/assets/5b50f7c1-cc6b-4064-9296-778732662748)

<h3>References</h3>
Gupta, D. (n.d.). What is Broken Authentication and How to Prevent it | LoginRadius Blog. Www.loginradius.com. https://www.loginradius.com/blog/identity/what-is-broken-authentication/</br>
InterSec, Inc. (n.d.). A Comprehensive guide to Penetration Testing: How to Protect Your Organization from Cyberattacks. Www.intersecinc.com. https://www.intersecinc.com/resources/guides/comprehensive-guide-to-penetration-testing</br>
Maury, J. (2023, February 28). How to Prevent Web Attacks Using Input Sanitization. ESecurityPlanet. https://www.esecurityplanet.com/endpoint/prevent-web-attacks-using-input-sanitization/</br>
