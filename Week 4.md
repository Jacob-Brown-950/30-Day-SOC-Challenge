# Week 4: Security & System Setup

## Tasks Completed

### 1. Query for svchost and Investigated Event ID 1
- Investigated event logs and queried for `svchost`. 
- We identified the original file name, which was a red flag. Even after renaming the file, the original name was still visible.
  
  ![svchost query image](path/to/your/image.png)

### 2. Built a Search to Query Malicious Event
- Created a specific query to target the malicious event we had acted on, enabling us to build an alert for future detection.
  
  ![query search image](path/to/your/image.png)

### 3. Better Query for Rule Creation
- Modified the query to focus only on process creation, specifically looking for `Apollo.exe`.
  
  ![better query image](path/to/your/image.png)

### 4. Creating a Rule (Custom Query, Not Threshold)
- Instead of using a threshold, created a rule using the default "custom query".
  
  ![rule creation image](path/to/your/image.png)

### 5. Dashboard for Suspicious Activity
- Built a dashboard to visualize suspicious activity using event IDs: `1`, `3`, and `5001`.
  
  ![dashboard image](path/to/your/image.png)

### 6. Setup of Windows Server 2022 VM for osTicket
- Created a VM running Windows Server 2022 for osTicket.
  
  ![windows server image](path/to/your/image.png)

### 7. Download XAMPP
- Downloaded and installed XAMPP, leaving all default options in place.

  ![xampp download image](path/to/your/image.png)

### 8. Configured XAMPP to Use Public IP
- Edited the `C:\XAMPP\properties` file to set the IP address to the public IP.

  ![xampp config image](path/to/your/image.png)

### 9. Created Inbound Allow Rules for Ports 80 and 443
- Created an inbound allow rule for ports `80` and `443` in the firewall.

  ![firewall rule image](path/to/your/image.png)

### 10. Started Apache and MySQL Services
- Started the Apache and MySQL services in the XAMPP control panel.

  ![xampp services image](path/to/your/image.png)

### 11. Edited phpMyAdmin and Config Files
- Made modifications in `phpMyAdmin` to configure it for external access by setting the public IP and credentials.
- Also edited the `config.inc.php` for the same purpose.

  ![phpmyadmin config image](path/to/your/image.png)

### 12. Solved XAMPP Errors
- After configuration, resolved any errors with XAMPP setup.

  ![resolved xampp errors image](path/to/your/image.png)

### 13. Downloaded and Set Up osTicket
- Downloaded the free, self-hosted, open-source software `osTicket`.
  
  ![osticket download image](path/to/your/image.png)

### 14. Extracted and Placed osTicket Files in XAMPP Directory
- Extracted the osTicket files and copied them to a new folder in the `xampp/htdocs` directory.
  
  ![osTicket folder image](path/to/your/image.png)

### 15. Initiated osTicket Installer
- Navigated to the public IP and `/osticket/upload` to start the osTicket installation.
- Renamed `ost-sampleconfig` to `ost-config`.

  ![osticket installer image](path/to/your/image.png)

### 16. Created Database in phpMyAdmin for osTicket
- Created the necessary database in phpMyAdmin before proceeding with the osTicket installation.

  ![phpmyadmin database image](path/to/your/image.png)

### 17. Completed osTicket Installation
- Successfully completed the osTicket installation process.

  ![osticket install success image](path/to/your/image.png)

### 18. Ran the Command for osTicket Configuration
- Ran the required command to configure the `ost-config` file.
  
  ![osticket config command image](path/to/your/image.png)

### 19. Logged into osTicket Staff Control Panel
- Successfully logged into the staff control panel of osTicket.

  ![osTicket login image](path/to/your/image.png)

### 20. Integrated ELK Stack API with osTicket
- Connected the osTicket API to the private IP of the ELK stack.

  ![elk integration image](path/to/your/image.png)

### 21. Successfully Built ELK Stack Connector
- Built a connector in the ELK stack using the API key provided by osTicket.
  
  ![elk connector image](path/to/your/image.png)

### 22. Sent a Test Payload to Confirm Functionality
- Sent a test payload to ensure the connection and integration was working properly.

  ![test payload image](path/to/your/image.png)

### 23. Investigated Ticket Flood (Alert Fatigue)
- Encountered a high volume of tickets due to configuration choices—this was not optimal and led to alert fatigue.
  
  ![ticket flood image](path/to/your/image.png)

### 24. Investigated SSH and RDP Brute Force Alerts
- Investigated SSH and RDP brute force alerts to ensure security.

  ![brute force alerts image](path/to/your/image.png)

### 25. Investigated Mythic Agent Activity
- Investigated any potential activity related to the Mythic agent.
  
  ![mythic agent image](path/to/your/image.png)

### 26. Added Elastic Defender Integration
- Integrated Elastic Defender on the Windows endpoint to isolate it if needed.

  ![elastic defender image](path/to/your/image.png)

### Conclusion
This concludes Week 4's activities, which covered system setup, security investigations, rule creation, and system integrations.

---

Feel free to replace the `path/to/your/image.png` with the actual paths or URLs to your images, and adjust the descriptions to match your specific environment and setup.

