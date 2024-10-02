# Week 3: Brute Force RDP Attack Simulation and Mythic C2 Setup

## Steps

### 1. Finding Exposed RDP Servers
- **Using Shodan**: Search for servers with exposed RDP on the default port.
  ![Shodan Search](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2043%20Creating%20an%20account%20with%20shodan%20and%20searching%20port%203389.PNG)
- **Using Censys**: Perform the same search to verify results.
  ![Censys Search](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2044%20Using%20Censys%20for%20Finding%20open%20RDP%20ports%20too.PNG)

### 2. Monitoring Failed RDP Attempts
- Created a log query for failed RDP attempts and confirmed my own failed login.
  ![Failed RDP Log Query](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2045%20Saving%20a%20log%20query%20for%20Failed%20RDP%20Login%20Attempts%2C%20seeing%20my%20own%20log!.PNG)
- Created an alert for failed RDP attempts.
  ![Alert Generation](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2046%20Creating%20the%20Alert%20rule%20for%20failed%20RDP%20Attempts.PNG)
- Executed a brute force attack on my Windows server to generate an alert.
  ![Brute Force Alert](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2047%20Generating%20an%20alert%20via%20brute%20force%20RDP.PNG)

### 3. Configuring Detection Rules
- **Detection Rule Setup**:
    - Current rules only query thresholds; need to create detection rules under **Security**.
      ![Detection Rule Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2048%20This%20is%20where%20we%20make%20REAL%20alerts.PNG)
    - Opted for preconfigured rules or created a new one to experiment. I chose to make my own.
      ![Preconfigured Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2049%20Lets%20Create%20a%20new%20rule.PNG)
    - Configured data involved in the new rules, mirroring the process used for SSH attempts.
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png)
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2050%20Select%20this%20type%20of%20rule.PNG)
      ![Configuring New Rules](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2052%20My%20new%20rules%20are%20set.PNG)

### 4. Data Visualization
- Developed tables for dashboard visualization:
    - **Failed and Successful SSH Attempts** to the exposed Ubuntu server.
      ![SSH Attempts Visualization](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2054%20Created%20some%20tabled%20for%20my%20dashboard%20to%20visualize%20SSH%20data%20on%20my%20linux%20server.PNG)
    - **RDP Activity Tracking** on the exposed Windows server.
      ![RDP Activity Table](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2055%20Made%20some%20tables%20for%20the%20RDP%20activity%20on%20Windows%20Server.PNG)

### 5. Attack Diagram Creation
- Created an attack diagram outlining the threat actor's process.
  ![Attack Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2056%20Network%20Attack%20Diagram.PNG)

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
  ![Ubuntu Server Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2057%20Install%20Mythic%20Github%20Repo.PNG)
- Checked Docker status before restarting the service.
  ![Docker Status](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2058%20run%20the%20docker%20install%20command%20in%20your%20mythic%20directory.PNG)

### 7. Starting Mythic
- Run the following command to start Mythic:
    ```bash
    make
    ./mythic-cli start
    ```

### 8. Configuring Mythic
- Tightened firewall rules, allowing exceptions for Windows and Ubuntu servers.
  ![Firewall Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2059%20This%20is%20what%20my%20firewall%20looks%20like%20now%2C%20only%20allowing%20my%20windows%20and%20linux%20server%2C.PNG)
- Accessed Mythic web GUI:
    - Default user: mythic_admin
    - Find password with:
        ```bash
        cat .env | grep -i admin_password
        ```
  ![Mythic GUI Login](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2060%20Get%20your%20mythic%20admin%20password.PNG)
  ![Mythic GUI Login](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2061%20We're%20in%20the%20mythic%20dashboard!.PNG)

### 9. Preparing for the Attack
- Created a target file on the Windows VM with the admin password called "passwords.txt."
- Moved to Kali Linux machine wordlists directory and prepared `rockyou.txt`:
    ```bash
    gunzip rockyou.txt.gz
    head -n 50 rockyou.txt > ~/Documents/top_50_words.txt
    ```
  ![Preparing Wordlists](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2062%20lets%20access%20our%20wordlists%20directory.png)

### 10. Brute Force with Crowbar
- Added the Windows password to the wordlist for easier access, simulating an attack as if someone brute-forced.
- Installed Crowbar:
    ```bash
    sudo apt-get install -y crowbar
    ```
  ![Crowbar Installation](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2064%20Crowbar%20Successfully%20installed.png)

- **Brute Force Command**:
    ```bash
    crowbar -b RDP -u Administrator -C top_50_words.txt -s 155.138.220.109
    ```
  ![Brute Force Command](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2066%20Successful%20brute%20force!.png)

### 11. RDP Session Access
- Used `xfreerdp` to access the RDP session:
    ```bash
    xfreerdp /u:Administrator /p:Winter2024! /v:155.138.220.109
    ```
  ![Accessing RDP Session](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2067%20Successfully%20in%20the%20RDP%20session!.png)
- Executed commands for intelligence gathering:
   

