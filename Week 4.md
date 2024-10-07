# Week 4: Security & System Setup

Hey everyone! Welcome to Week 4 of the **30-Day SOC Analyst Challenge**. This week, I jumped into **Investigation** and got the **Elastic Defender** configured. I’ve learned a ton and will walk you through everything I did, why I did it, and share some helpful tips to make your setup process smoother if you're following along.

---

### 1. Query for svchost and Investigated Event ID 1
- Investigated event logs and queried for `svchost`. 
- We identified the original file name, which was a red flag. Even after renaming the file, the original name was still visible.
  
  ![svchost query image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2079%20Investigating%20logs%20generated%20by%20apollo.PNG)
  ![svchost query image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2080%20we%20can%20see%20the%20original%20file%20name%20even%20though%20we%20renamed%20it%20svc%20soc%20project.PNG)

### 2. Built a Search to Query Malicious Event
- Created a specific query to target the malicious event we had acted on, enabling us to build an alert for future detection.
  
  ![query search image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2081%20Built%20a%20search%20query%20so%20we%20can%20create%20an%20alert%20for%20this%20specific%20malicious%20activity.PNG)

### 3. Better Query for Rule Creation
- Modified the query to focus only on process creation, specifically looking for `Apollo.exe`.
  
  ![better query image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2082%20Actually%20heres%20a%20better%20query%20to%20make%20a%20rule%20from.PNG)

### 4. Creating a Rule (Custom Query, Not Threshold)
- Instead of using a threshold, created a rule using the default "custom query".
  
  ![rule creation image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2083%20What%20i%20did%20for%20my%20rule.PNG)

### 5. Dashboard for Suspicious Activity
- Built a dashboard to visualize suspicious activity using event IDs: `1`, `3`, and `5001`.
  
  ![dashboard image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2084%20Dashboard%20Created.PNG)

### 7. Download XAMPP
- Downloaded and installed XAMPP, leaving all default options in place.

  ![xampp download image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2085%20Download%20XAMPP%20on%20new%20windows%20Server%202022.PNG)

### 8. Configured XAMPP to Use Public IP
- Edited the `C:\XAMPP\properties` file to set the IP address to the public IP.

  ![xampp config image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2087%20Edit%20the%20config%20to%20point%20to%20my%20public%20IP.PNG)

### 9. Created Inbound Allow Rules for Ports 80 and 443
- Created an inbound allow rule for ports `80` and `443` in the firewall.

  ![firewall rule image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2088%20Created%20an%20inbound%20allow%20rule%20for%2080%20and%20443.PNG)

### 10. Started Apache and MySQL Services
- Started the Apache and MySQL services in the XAMPP control panel.

  ![xampp services image](path/to/your/image.png)

### 11. Edited phpMyAdmin and Config Files
- Made modifications in `phpMyAdmin` to configure it for external access by setting the public IP and credentials.
- Also edited the `config.inc.php` for the same purpose.

  ![phpmyadmin config image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2090%20edited%20some%20fields%20in%20the%20phpMyAdmin.PNG)
  ![phpmyadmin config image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2091%20edited%20the%20config%20inc%20file%20to%20point%20to%20our%20public%20IP.PNG)

### 12. Solved XAMPP Errors
- After configuration, resolved any errors with XAMPP setup.

  ![resolved xampp errors image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2091%20edited%20the%20config%20inc%20file%20to%20point%20to%20our%20public%20IP.PNG)
  ![resolved xampp errors image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2092%2C%20oops%20make%20sure%20you%20add%20your%20password%20to%20the%20config%20too.PNG)

### 13. Downloaded and Set Up osTicket
- Downloaded the free, self-hosted, open-source software `osTicket`.
  
  ![osticket download image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2094%20osTicket%20downloaded.PNG)

### 14. Extracted and Placed osTicket Files in XAMPP Directory
- Extracted the osTicket files and copied them to a new folder in the `xampp/htdocs` directory.

### 15. Initiated osTicket Installer
- Navigated to the public IP and `/osticket/upload` to start the osTicket installation.
- Renamed `ost-sampleconfig` to `ost-config`.

  ![osticket installer image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2096%20navigate%20to%20your%20public%20IP%20with%20osticket%20upload%20to%20find%20the%20installer.PNG)

### 16. Created Database in phpMyAdmin for osTicket
- Created the necessary database in phpMyAdmin before proceeding with the osTicket installation.

### 17. Completed osTicket Installation
- Successfully completed the osTicket installation process.

  ![osticket install success image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2099%20osticket%20installation%20complete.PNG)

### 19. Logged into osTicket Staff Control Panel
- Successfully logged into the staff control panel of osTicket.

  ![osTicket login image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20101%20logged%20into%20my%20staff%20control%20panel.PNG)

### 20. Integrated ELK Stack API with osTicket
- Connected the osTicket API to the private IP of the ELK stack.

  ![elk integration image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20102%20connected%20admin%20portal%20API%20to%20my%20ELK%20Private%20IP.PNG)

### 21. Successfully Built ELK Stack Connector
- Built a connector in the ELK stack using the API key provided by osTicket.
  
  ![elk connector image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20103%20built%20a%20connector%20for%20my%20osTicket%20and%20elastic%20stack.PNG)

### 22. Sent a Test Payload to Confirm Functionality
- Sent a test payload to ensure the connection and integration was working properly.

  ![test payload image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20104%20Succesfully%20tested%20the%20payload%20to%20confirm%20ticketing%20can%20communicate.PNG)

### 23. Investigated Ticket Flood (Alert Fatigue)
- Encountered a high volume of tickets due to configuration choices—this was not optimal and could lead to alert fatigue.
  
  ![ticket flood image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20105%20We%20got%20tons%20of%20tickets.PNG)

### 24. Investigated SSH and RDP Brute Force Alerts
- Investigated SSH and RDP brute force alerts to ensure security.

  ![brute force alerts image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20106%20Investigate%20an%20alert%20related%20to%20SSH%20brute%20force.PNG)
  ![brute force alerts image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20107%20Investigate%20an%20alert%20related%20to%20RDP%20brute%20force.PNG)

### 25. Investigated Mythic Agent Activity
- Investigated any potential activity related to the Mythic agent.
  
  ![mythic agent image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20108%20Investigated%20mythic%20agent.PNG)

### 26. Added Elastic Defender Integration
- Integrated Elastic Defender on the Windows endpoint to isolate it if needed.

  ![elastic defender image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20109%20downloading%20elastic%20defend.PNG)
  ![elastic defender image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%20110%20our%20windows%20endpoint%20is%20running%20defender%20and%20we%20can%20isolate%20it.PNG)

### Conclusion
This concludes Week 4's activities, which covered system setup, security investigations, rule creation, and system integrations.
