# Week 1: ELK Stack Setup and Fleet Server Configuration

## Overview
In the first week of the project, I successfully set up the ELK stack and configured the Fleet Server. Below are the key activities and configurations completed.

---

### 1. Network Diagram
- **Created a logical diagram** to represent the network, including the threat actor. (Note: I placed the Windows and Ubuntu servers outside the VPC; accessing these could compromise the entire network.)
  
  ![Network Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Network%20Logical%20Diagram.png)

### 2. VPC Setup
- **Created a VPC 2.0 network** in Vultr.  
  ![VPC Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%202%20Click%20%22Add%20VPC%202.0%22.png)

### 3. Server Configuration
- **Set up my Ubuntu 22.04 server VM** and performed system updates.
- **Downloaded Elasticsearch** (`deb x86_64`) and configured the `elasticsearch.yml` file.  
  ![Elasticsearch Download](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%203%20Downloading%20Elasticsearch.png)

- *(Optional)* Added a firewall group setting to restrict access to the server. (This caused some troubleshooting issues later on.)

- **Confirmed that Elasticsearch is running** successfully. Make sure to save this information somewhere!  
  ![Elasticsearch Running](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%204%20Make%20Sure%20You%20Save%20This%20info!.png)

- **Use the public IP for your Elasticsearch config.**  
  ![Find Public IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png)

- **Implementing the Config**: Uncomment the port number and the IP in the config file.  
  ![Configure yml File](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%206%20Configure%20elasticsearch%20yml%20file.png)

- **Downloaded Kibana** (`deb x86_64`), configured the `kibana.yml`, and started Kibana (similar process as Elasticsearch).  
  ![Kibana Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%207%20Configure%20Kibana%20yml.png)

- Obtained your **Elasticsearch Token** and saved it for later use.  
  ![Elasticsearch Token](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%208%20Get%20your%20Token.png)

### 4. Troubleshooting
- **Issue 1 resolved**: The firewall was initially allowing only port 22; I ensured that the port for Kibana is also permitted for remote access.
- **Ran `ufw allow 5601`** on the VM CLI to allow Kibana's port.

- **Pasted the enrollment token** in the web GUI, received my **verification code**, and successfully completed the setup.  
  ![Kibana Access](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%209%20Got%20in%20to%20Kibana!%20now%20paste%20your%20key%20in.png)

- **Resolved API integration error** by adding Kibana keys into the keystore. Now, the **Kibana web GUI is fully functional**!  
  ![Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2011%20Get%20your%20encryption%20keys.png)

- Enter those Keys into your Kibana Keystore one by one.  
  ![Enter Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2012%20Enter%20those%20keys%20into%20the%20keystore.png)

### 5. Additional Changes
- **Exposed RDP to the internet** to generate failed login logs for later investigation. Verified RDP connection via the web.

### 6. Fleet Server Setup
- **Created a fleet server** and pointed it to the Vultr fleet server in Kibana.  
  ![Got Fleet Server IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2013%20Get%20Public%20IP%20of%20Fleet%20Server%20.png)  
  ![Configure Fleet](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2014%20Point%20Fleet%20Server%20in%20Kibana%20to%20IP.png)  
  ![Firewall Rule Adjustment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2016%20Add%20firewall%20rule%20to%20allow%20fleet%20server%20connection.png)

- **Deployed the agent** by running the script.  
  ![Agent Deployment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2017%20Agent%20Installed%20Successfuly!%20.png)

- **Issue 2 resolved**: Added a rule to allow communication between the fleet server and Kibana.  
  ![Kibana Fleet Server Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2016%20Add%20firewall%20rule%20to%20allow%20fleet%20server%20connection.png)

- Created a **policy for the Windows server** to install the agent and collect logs.
- **Allowed agent connection** on the fleet server with `ufw allow 8220`.

- **Issue 3 resolved**: Changed the fleet port from **443 to 8220** and added `--insecure` to handle the self-signed certificate issue.  
  ![Fleet Port Change](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2018%20Go%20to%20fleet%20and%20change%20the%20port!.png)  
  ![Script Modification](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2019%20Fix%20the%20script%20and%20run%20again%2C%20success.png)

- Confirmed **connection and logs** flowing into the fleet dashboard. **Success!**  
  ![Logs in Fleet Dashboard](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2021%20See%20if%20you%20got%20logs!%20.png)

---

This concludes Week 1.
