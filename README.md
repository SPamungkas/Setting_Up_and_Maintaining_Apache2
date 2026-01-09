# Setting_Up_and_Maintaining_Apache2
Technical guide and documentation for deploying, configuring, and managing an Apache2 Web Server on Linux.

# About Me
Information Systems graduate, currently transitioning to Cyber Security. Previously served as a Technician at Oil and Gas Industry (Pertamina Patra Niaga vendor), where I developed a highly disciplined approach to managing critical infrastructure compliance and 24/7 reliability. Currently formalizing expertise through an intensive cybersecurity bootcamp at Dibimbing, I am eager to apply this technical foundation and structured approach to a security operations role.

# Tools
- Virtual Machine
- Kali Linux
- Apache2

# 1. Installation and Package Verification 
The deployment began with ensuring the system was up-to-date and that the Apache2 package was installed at its latest stable version.

```bash
# Installing Apache2 and upgrading packages in a single command string
sudo apt-get install apache2 && sudo apt-get upgrade -y
```
<p align="center">
  <img width="500" height="251" alt="image" src="https://github.com/user-attachments/assets/7f9ddb89-03c1-414b-ba50-a71e18e46e93" />
  <br>
</p>
I utilized the && operator to chain the installation and upgrade commands, ensuring a streamlined workflow. Since Apache2 was already present on my system, the output confirmed that "apache2 is already the newest version". This step is vital in server administration to ensure that the software is patched against known vulnerabilities and that we are working with the most stable features available in the official repositories.

# 2. Service Operational Verification
Once the installation was confirmed, I performed a status check to ensure the Apache2 service was initialized and operating in the background.
```bash
# Verifying the current status of the Apache2 service
sudo systemctl status apache2
```
<p align="center">
  <img width="500" height="291" alt="image" src="https://github.com/user-attachments/assets/36f6232c-f0ec-4c86-ada3-660ddff5f2bc" />
  <br>
</p>
I executed the systemctl status command to monitor the services health. The output provided critical information, including the "active (running)" status and the service's Main PID (Process ID). This confirms that the web server is successfully listening for requests and that the initial configuration is stable. Verifying service uptime is a routine but essential task in maintaining server availability and reliability.

# 3. Network Interface and IP Identification
To access the web server from other devices or verify its network presence, I needed to identify the internal IP address assigned to the Virtual Machine.
```bash
# Identifying the IP address of the VM
ip a
```
<p align="center">
  <img width="500" height="263" alt="image" src="https://github.com/user-attachments/assets/e561ba1c-fa0c-41b0-bd98-b4e782500899" />
  <br>
</p>
I used the ip a show command to inspect the network interfaces. By identifying the IP address assigned to the primary interface (typically eth0), I established the exact entry point for web traffic. Understanding how to locate a server's IP address is fundamental for configuring DNS, setting up virtual hosts, and ensuring the server is reachable within the network architecture.

# 4. Custom Directory Structure and Web Content Deployment
To demonstrate organized web server management, I created a dedicated directory for my web content instead of using the default root. This approach is essential for managing multiple websites on a single server.
```bash
# Creating a personalized directory within the web server root
sudo mkdir /var/www/satria
```
<p align="center">
  <img width="500" height="162" alt="image" src="https://github.com/user-attachments/assets/1a4ab4c0-0d7d-4353-bf6a-6c8980cd77ca" />
  <br>
</p>
I initialized a custom directory named satria within /var/www/. By moving away from the default /var/www/html path, I demonstrated the ability to structure web assets professionally. This setup is the first step toward configuring Apache Virtual Hosts, allowing the server to distinguish between different projects or domains. This organized workflow is crucial for scalability and maintaining clear boundaries between different hosted applications.
<br>
<br>
After establishing the custom directory, I proceeded to deploy the website content by migrating a pre-developed HTML template from my home directory to the production web root.

```bash
# Copying the custom index.html to the specialized web directory
sudo cp /home/satria/index.html /var/www/satria/

# Verifying the file transfer
ls /var/www/satria
```
<p align="center">
  <img width="500" height="157" alt="image" src="https://github.com/user-attachments/assets/20773593-6294-49ad-a5ff-0e39c4fa25d8" />
  <br>
</p>
I utilized the cp (copy) command with sudo privileges to move the index.html file. This action demonstrates a clear understanding of Linux file permissions, as writing to /var/www/ requires elevated administrative rights. By verifying the transfer with the ls command, I ensured that the web server now has the necessary resources to serve the personalized content. This workflow mimics a real-world deployment scenario where developers push code from a local environment to a live server directory.
<br>
<br>
To personalize the web content, I modified the HTML file directly through the terminal. Using a command line text editor like Nano allows for quick and efficient server-side updates without needing a graphical user interface.

```bash
# Editing the HTML file with root privileges
sudo nano index.html
```
<p align="center">
  <img width="500" height="51" alt="image" src="https://github.com/user-attachments/assets/72cf90d6-19c2-49a0-93ab-320caf9f9f63" />
  <br>
</p>
I invoked the nano editor with sudo privileges to modify the file. This elevation of privilege is mandatory because files within the /var/www/ directory are protected system resources.
<br>
<br>
In this phase, I populated the web page with specific technical content. I modified the HTML structure to reflect the project's objectives and to serve as a quick reference for Apache’s logging system.
<br>
<br>
Changes made during the edit:
<br>
- Title: Updated to "Assignment Day 4" for project identification.
<br>
- Personal Identity: Added my full name as the server administrator.
<br>
- Technical Definitions: Included clear explanations of access.log and error.log to demonstrate fundamental server monitoring knowledge.
<p align="center">
  <img width="500" height="401" alt="image" src="https://github.com/user-attachments/assets/e8420f3a-872a-44ff-a7f6-8d6e39b483fa" />
  <br>
</p>
By embedding the definitions of Access Logs and Error Logs directly into the homepage, I created a functional documentation page. Saving these changes using the Nano editor's write out function finalized the content preparation. This step illustrates the transition from a default server installation to a personalized, purpose built web environment. It also reinforces the concept that a web server's primary role is to serve structured data to the end-user.

# 5.Network Binding and Port Configuration
To ensure the web server is accessible over the network (and not just restricted to the local interface), I configured Apache to explicitly "listen" on the VM's assigned IP address. This is done by modifying the ports.conf file within the global Apache configuration directory.
```bash
# Navigating to the Apache configuration directory
cd /etc/apache2

# Editing the ports configuration file
sudo nano ports.conf
```
<p align="center">
  <img width="500" height="155" alt="image" src="https://github.com/user-attachments/assets/3a63cad3-e8b5-41ae-8c01-4b09daa647ad" />
  <br>
</p>
I accessed the /etc/apache2 directory to modify the ports.conf file. By adding the specific IP address of the VM, I performed IP Binding. This configuration tells the Apache service to monitor incoming traffic on that specific network interface. This is a crucial step in server hardening and network configuration, as it defines exactly how the server exposes itself to the internal network or the internet, preventing unintended access from other interfaces.
<br>
<br>
To avoid port conflicts (since the default port 80 was already occupied by the localhost service), I configured Apache to listen on a custom port. This exercise demonstrates the ability to manage network resources and resolve service collisions.
<p align="center">
  <img width="500" height="208" alt="image" src="https://github.com/user-attachments/assets/d692fd1e-1407-4ca9-a40f-b4b2284c8e9b" />
  <br>
</p>
I assigned the server to listen on Port 8088 specifically for the VM's IP address (192.168.85.128). During this process, I encountered a configuration conflict where Apache failed to start if multiple IP-specific listen directives were active simultaneously. To resolve this, I commented out the conflicting lines, ensuring the service could initialize properly.
<br>
<br>
After modifying the network port settings, the Apache service must be restarted to apply the new configurations. This ensures that the daemon stops using the old parameters and begins listening on the newly assigned port (8088).

```bash
# Restarting the Apache2 service to apply changes
sudo systemctl restart apache2
```
<p align="center">
  <img width="500" height="68" alt="image" src="https://github.com/user-attachments/assets/124b1211-24f1-4867-ac89-b76118570a83" />
  <br>
</p>
I executed the systemctl restart command to finalize the deployment. This is a critical step in the Change Management process, without a restart, the server would continue to attempt communication on the default port 80. By successfully restarting the service without errors, I confirmed that the syntax in ports.conf was correct and that the server is now officially broadcasting the custom web content over the network via port 8088.

# 6. Configuring a Custom Virtual Host
To manage the website professionally, I moved away from the default Apache configuration and created a dedicated Virtual Host file. This practice allows a single Apache server to host multiple domains or projects with separate settings and directories.
```bash
# Creating a new Virtual Host configuration file
sudo nano /etc/apache2/sites-available/tugas.conf
```
<p align="center">
  <img width="500" height="60" alt="image" src="https://github.com/user-attachments/assets/d031ab89-3e69-47e2-9582-8cf0697548f9" />
  <br>
</p>
I accessed the /etc/apache2/sites-available/ directory to create a new configuration file named tugas.conf. In Linux server administration, files in sites-available act as blueprints. By creating a separate file instead of editing the default one, I ensured a modular and scalable setup.
<br>
<br>
Inside the tugas.conf file, I implemented a custom configuration to bridge the network port, the web directory, and the logging system. This setup ensures that the server knows exactly where to look for files and where to record activity.
<p align="center">
  <img width="500" height="177" alt="image" src="https://github.com/user-attachments/assets/42380f57-9ea4-4dc1-b6b8-6afd3b9cdd6d" />
  <br>
</p>
By customizing the ErrorLog and CustomLog directives, I established a professional monitoring workflow. Setting the LogLevel to info provides a balance between having enough data for troubleshooting without overwhelming the disk space with debug-level details.

# 7. Deployment and Browser Verification
This stage of the project was to verify that the web server successfully serves the custom HTML content over the network using the designated port and Virtual Host configuration. I opened a web browser and navigated to the following URL: http://192.168.85.128:8088/satria.html
<p align="center">
  <img width="500" height="297" alt="image" src="https://github.com/user-attachments/assets/627e95c8-72f3-44d6-aec5-1acc467b90cc" />
  <br>
</p>
The browser correctly displays the customized title "Assignment Day 4" and the technical descriptions of Apache logs.

# 8. Log Monitoring 
After successfully accessing the website via the browser, I verified that the activity was correctly recorded in the custom log files I created earlier. Monitoring logs is a vital skill for troubleshooting and security auditing.
```bash
# Displaying the last 5 entries of the custom access log
tail -n 5 satria_access.log
```
<p align="center">
  <img width="500" height="233" alt="image" src="https://github.com/user-attachments/assets/22014cbb-b9b5-4422-a745-d97a3eaab117" />
  <br>
</p>
By executing the tail -n 5 command, I could see the most recent interaction with the server. The output displayed the IP address of the client, the timestamp of the request, the HTTP method, and the status code. This confirms that the Custom Logging configuration in the Virtual Host is working perfectly, capturing real-time traffic data.

# 9. Error Handling and Negative Testing (404 Not Found)
To ensure the server correctly identifies and logs invalid requests, I performed a "Negative Test" by attempting to access a non-existent resource. I attempted to access the following URL: http://192.168.85.128:8088/icikiwir.html. Since icikiwir.html does not exist in the /var/www/satria directory, the server is expected to return a standard 404 Not Found HTTP status code.
<p align="center">
  <img width="500" height="241" alt="image" src="https://github.com/user-attachments/assets/bd8627bd-c369-465d-9580-38d8fd9b17c4" />
  <br>
</p>
This test confirms that the Apache web server is handling requests accurately. A 404 error is not a failure of the server itself, but a correct response indicating that the server is operational and can distinguish between available and unavailable resources.
<br>
<br>
After intentionally triggering a 404 Not Found error, I reexamined the access logs to confirm that the server correctly recorded the failed request. This step demonstrates the reliability of the logging system in capturing non standard events.

```bash
# Checking the last 5 entries to see the recorded 404 error
tail -n 5 satria_access.log
```
<p align="center">
  <img width="500" height="125" alt="image" src="https://github.com/user-attachments/assets/b3423034-ed8a-4d67-9e36-352b42478dba" />
  <br>
</p>
he output of the tail command clearly shows a GET request for /icikiwir.html followed by the HTTP status code 404. This proves that my custom Virtual Host configuration is effectively routing log data to satria_access.log.
<br>
<br>
The final verification step involves inspecting the Error Log. While the Access Log records the request, the Error Log provides diagnostic details that are essential for system debugging.

```bash
# Examining the last 5 entries of the custom error log
tail -n 5 satria_error.log
```
<p align="center">
  <img width="688" height="116" alt="image" src="https://github.com/user-attachments/assets/b7b48d9c-e24b-4f55-9fdb-10a820ce31bf" />
  <br>
</p>
By running tail -n 5 on satria_error.log, I can observe the server's internal response to the missing file.
