# CODTECH_T2
## WEB APPLICATION PENETRATION TESTING
## Personal information 
- Name : Devarsh Mehta
- Company : CODTECH IT SOLUTIONS PVT.LTD
- ID : CT08DAL
- Domain : Cyber Security & Ethical Hacking
- Duration: 20th Dec 2024 To 20th Jan 2025
- Mentor : Neela Santhosh kumar
## Overview
- A web application penetration testing project involves systematically evaluating the security of a web application by simulating real-world attacks to identify 
  vulnerabilities, weaknesses, and misconfigurations that could be exploited by malicious actors. The goal is to discover and address these issues to enhance the 
  application's security.
## Objective
- Identify Scope
- Identify The Weakness
- Exploit Vulnerability
- Precautions
- Enhance Security Features
## Tools
- Burpsuite
- sqlmap or Jsql
- ZAP proxy
- Metasploit Framework
- Nessus
## Perform Task
### Details of site where we performed the web application Testing
***1.XSS (Cross Side Scripting):*** Cross-Site Scripting (XSS) is a type of security vulnerability typically found in web applications. It allows attackers to inject malicious scripts into web pages viewed by other users. These scripts can execute in the victim's browser, leading to various malicious activities such as stealing cookies, session tokens, or other sensitive information.
- **Target** : http://testphp.vulnweb.com
- **Impact:** XSS can allow attackers to steal sensitive data, impersonate users, and distribute malware, leading to serious security breaches.
- Step 1: identify the target Link
![Screenshot 2024-12-24 175919](https://github.com/user-attachments/assets/17bf24d7-eb94-49df-a7bb-b54ca5522219)

- Step 2: Let’s Try to Search some name/items
 ![Screenshot 2024-12-24 180233](https://github.com/user-attachments/assets/ffe4cecf-7e47-4d65-b856-bd391908ed21)


- Step 3: Now Let’s see the page source
 ![Screenshot 2024-12-24 180548](https://github.com/user-attachments/assets/eeb64679-48ae-48c3-bff5-c4f7445d3627)

- It look’s like a payload injectable there no sanitizing and prevention of JavaScript or html payload Injections.

- Step 4: Now let’s inject a xss payload 
```payload
  Payload:<script>alert(‘You Have been hacked’)</script>
```
![Screenshot (34)](https://github.com/user-attachments/assets/6c75cd3c-1722-40ca-ae89-1de0e17afd14)
Now Hit the enter and see	
![Screenshot (35)](https://github.com/user-attachments/assets/cb704ad6-72fa-4659-9184-727c29606fcf)
XSS Found successfully.

***2.SQL injection:*** SQL Injection is a critical security vulnerability that allows attackers to manipulate SQL queries by injecting malicious code into input fields, potentially leading to unauthorized access, data theft, or destruction of the database.
- **Target** : http://testphp.vulnweb.com/artists.php?artist=1
- **Impact:** The impact of SQL Injection includes unauthorized access to sensitive data, data theft, data modification or deletion, loss of database integrity, administrative control over the database, and potential for further system compromise. It can also lead to severe reputational damage and legal consequences for the affected organization.
- Step 1:Identify the Target Website
![Screenshot (36)](https://github.com/user-attachments/assets/77a754aa-b7ad-468a-96dd-7f414f2cd33d)
- Step 2: In the URL artist=1 is look like sql injectable so let’s open kali linux and open “SQL map”
```Command
  Command:  sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 --dbs
```
![Screenshot (37)](https://github.com/user-attachments/assets/aa6441bb-914d-48dc-8100-804a8c635b79)
![Screenshot (38)](https://github.com/user-attachments/assets/6c550566-39e2-4620-ba55-465addc30b1d)
- Here you can see there are 2 databases Found : 1.acuart 2.information_schema
- Step 3:  Now I can use database acuart and find some information.
```command
 Command: sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart --columns
```
![Screenshot (39)](https://github.com/user-attachments/assets/df21d954-52fe-44e3-9292-1d5990714c56)
![Screenshot (40)](https://github.com/user-attachments/assets/9b53ccee-b70f-44d4-a847-fccbb4547d10)
- You can see I have found users table etc. columns let’s find more details from tables.
```command
Command:  sqlmap -u http://testphp.vulnweb.com/artists.php?artist=1 -D acuart -T users -C uname,pass –dump
```
![Screenshot (41)](https://github.com/user-attachments/assets/23624949-d07f-4c6e-966c-639b4885f310)
![Screenshot (42)](https://github.com/user-attachments/assets/8c7e0095-abec-4209-9b0c-91801ae0a8a5)
- With the help of I can found the username and password of the website.


***3.Insecure Authentication Mechanism:*** Insecure authentication mechanisms can lead to unauthorized access, data breaches, and various security vulnerabilities. They often involve weak password policies, lack of multi-factor authentication, improper session management, and insecure password storage practices.
- **BUG:** 2FA Bypass
- **Impact:** Insecure authentication mechanisms can lead to unauthorized access, data breaches, and compromised sensitive information.
- Step 1:  identify the Website
  •	My credentials: wiener:peter 
  •	Victim's credentials carlos:montoya
  ![Screenshot (43)](https://github.com/user-attachments/assets/4362b5d4-4099-4e54-a510-67be15bb0be8)
- Step 2: Now Click on my account and Open login page
  ![Screenshot (44)](https://github.com/user-attachments/assets/1b9c7d93-8c92-49a1-83b0-2256d982cae1)
- Step 3: Login the page Using credentials 
  • Id: wiener   Pass: peter
![Screenshot (50)](https://github.com/user-attachments/assets/3d99df8b-ebfb-45b6-9a2c-b39dfcbaecaf)
- Step 4: Now It will ask a 4 digit OTP for 2FA(2Factor authentication)
  ![Screenshot (51)](https://github.com/user-attachments/assets/30a52f6a-997b-4098-bf23-ab3fb5dff343)
- On the Top of The page You can see "Email Client" click on it.
  ![Screenshot (53)](https://github.com/user-attachments/assets/fc302a0a-4451-49fb-8839-12cf7ed8bc89)
- You can see OTP is: 0206,Now lets login with OTP
- Step 5: Login and check the URL
  ![Screenshot (54)](https://github.com/user-attachments/assets/90f87e1b-0a46-4966-8184-b89bfd87855d)
  ![Screenshot (55)](https://github.com/user-attachments/assets/0ee648dd-1c5a-4ac0-870a-e4cc405a774b)
***You can see url:***  https://0a43002104d4e1bd82b339c700a800a8.web-security-academy.net/my-account?id=wiener
- Now Logout Form Wiener and login with attacker Credentials.
- Step 6: Logout Form wiener account and login with Target credentials
  Target : Id: carlos    pass: montoya
 ![Screenshot (56)](https://github.com/user-attachments/assets/6a95af6a-38d3-4c55-9605-5a00aa01b5d8)
- It will ask for OTP
  ![Screenshot (57)](https://github.com/user-attachments/assets/8561651f-dc0c-44ac-a3a3-7055a43a960f)
- OTP is sent on Target email Id so we can identify the url first
- Step 7: identify url
```url
Default_URL:  https://0a43002104d4e1bd82b339c700a800a8.web-security-academy.net/login2
```
- now just edit url and and write “/my-account” and remove “/login2”
```url
Edited_URL: https://0a43002104d4e1bd82b339c700a800a8.web-security-academy.net/my-account
```
![Screenshot (59)](https://github.com/user-attachments/assets/85b9bdcc-9dc6-4ff4-b479-7248b40179d9)
![Screenshot (60)](https://github.com/user-attachments/assets/83d494be-2a8f-45d6-affb-57aeef730f6c)
- You can see 2FA has been bypass successfully and enter into carlos account.

## Conclusion: 
-  Web Application Penetration Testing is critical for detecting and addressing security flaws in web applications.
- By performing thorough testing and providing remediation recommendations, we can enhance the security posture of web applications and protect them from potential attacks.
