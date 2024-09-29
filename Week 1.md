## Week 1: ELK Stack Setup and Fleet Server Configuration

- **Created a logical diagram** to represent the network, including the threat actor.  
  ![Network Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Network%20Logical%20Diagram.png)

- **Created a VPC 2.0 network** in Vultr.  
  ![VPC Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%202%20Click%20%22Add%20VPC%202.0%22.png)

- **Set up my Ubuntu 22.04 server VM** and ran updates.  

- **Downloaded Elasticsearch debx86_64** and configured the `elasticsearch.yml` file.  
  ![Elasticsearch Download](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%203%20Downloading%20Elasticsearch.png)

- *(Optional)* Added a firewall group setting to ensure only I can access the server, restricting access from the entire internet. (I did this and it actually caused some troubleshooting issues later!)

- **Successfully started and confirmed Elasticsearch** is running. During the download, save this information somewhere
  ![Elasticsearch Running](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%204%20Make%20Sure%20You%20Save%20This%20info!.png)

  - **Use the public IP for your elasticsearch config
  ![Find Public IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png)

  - Implementing the Config (Uncomment the port number and the IP)
  ![Configure yml File](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%206%20Configure%20elasticsearch%20yml%20file.png)

- **Downloaded Kibana debx86_64**, configured the `kibana.yml`, and started Kibana. (Same process as Elasticsearch)
  ![Configure yml File](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%207%20Configure%20Kibana%20yml.png)

  - Get Your Elasticsearch Token and save this somewhere, we need it later
  ![Elasticsearch Token](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%208%20Get%20your%20Token.png)
  
- **Issue 1 solved**: Firewall was only allowing port 22; ensured the port Kibana is on is allowed for remote access.

- **Ran `ufw allow 5601`** on the VM CLI to allow Kibana's port.  

- **Pasted the enrollment token** on the web GUI, received my **verification code**, and successfully completed the setup.
  ![Configure Web GUI](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%209%20Got%20in%20to%20Kibana!%20now%20paste%20your%20key%20in.png)

- Solved the **API integration error** by adding Kibana keys into the keystore. The **Kibana web GUI is fully functional**!  
  ![Access Your Encryption Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2011%20Get%20your%20encryption%20keys.png)

- Enter those Keys into your kibana Keystore one by one
- ![Enter Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2012%20Enter%20those%20keys%20into%20the%20keystore.png)

### Additional Changes:

- **Exposed RDP to the internet** to generate failed login logs for investigation later. Verified RDP connection via the web.  

### Fleet Server Setup:
- **Created a fleet server** and pointed it to the Vultr fleet server in Kibana.  
  ![Got Fleet Server IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2013%20Get%20Public%20IP%20of%20Fleet%20Server%20.png)
  ![Configure Fleet](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2014%20Point%20Fleet%20Server%20in%20Kibana%20to%20IP.png)
  ![Had to Add Firewall rule since I made it strict for it to work](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2016%20Add%20firewall%20rule%20to%20allow%20fleet%20server%20connection.png)

- **Deployed the agent** by running the script.  
  ![Agent Deployment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2017%20Agent%20Installed%20Successfuly!%20.png)

- **Issue 2 solved**: Added rule so the fleet server can communicate
  ![Kibana Fleet Server Configure](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2018%20Go%20to%20fleet%20and%20change%20the%20port!.png)

- Created a **policy for the Windows server** to install the agent and collect logs.

- **Allowed agent connection** on the fleet server (`ufw allow 8220`). 

- **Issue 3 solved**: Changed the fleet port from **443 to 8220** and added `--insecure` to handle the self-signed certificate issue.  
  ![Fleet Port Change](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2018%20Go%20to%20fleet%20and%20change%20the%20port!.png)

  ![Script Modification](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2019%20Fix%20the%20script%20and%20run%20again%2C%20success.png)

- Confirmed **connection and logs** flowing into the fleet dashboard. **Success!**  
  ![Logs in Fleet Dashboard](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2021%20See%20if%20you%20got%20logs!%20.png)

This concludes Week 1.

