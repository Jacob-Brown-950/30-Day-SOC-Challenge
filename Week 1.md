## Week 1: ELK Stack Setup and Fleet Server Configuration

- **Created a logical diagram** to represent the network, including the threat actor.  
  ![Network Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Network%20Logical%20Diagram.png)

- **Created a VPC 2.0 network** in Vultr.  
  ![VPC Setup](path/to/image.png)

- **Set up my Ubuntu 22.04 server** and ran updates.  
  ![Ubuntu Server Setup](path/to/image.png)

- **Downloaded Elasticsearch debx86_64** and configured the `elasticsearch.yml` file.  
  ![Elasticsearch Download](path/to/image.png)

- *(Optional)* Added a firewall group setting to ensure only I can access the server, restricting access from the entire internet.  
  ![Firewall Group Setting](path/to/image.png)

- **Successfully started and confirmed Elasticsearch** is running.  
  ![Elasticsearch Running](path/to/image.png)

- **Downloaded Kibana debx86_64**, configured the `kibana.yml`, and started Kibana.  
  ![Kibana Download](path/to/image.png)

- **Issue 1 solved**: Firewall was only allowing port 22; ensured the port Kibana is on is allowed for remote access.  
  ![Firewall Issue Fix](path/to/image.png)

- **Ran `ufw allow 5601`** on the VM CLI to allow Kibana's port.  
  ![Allow Port 5601](path/to/image.png)

- **Pasted the enrollment token** on the web GUI, received my **verification code**, and successfully completed the setup.  
  ![Enrollment Token](path/to/image.png)

- Solved the **API integration error** by adding Kibana keys into the keystore. The **Kibana web GUI is fully functional**!  
  ![Kibana GUI](path/to/image.png)

### Additional Changes:
- **Modified the logical diagram**: Decided **not to put the Windows and Ubuntu server in the VPC** to prevent exposing the entire network if compromised.  
  ![Logical Diagram Update](path/to/image.png)

- **Exposed RDP to the internet** to generate failed login logs for investigation later. Verified RDP connection via the web.  
  ![RDP Exposed](path/to/image.png)

### Fleet Server Setup:
- **Created a fleet server** and pointed it to the Vultr fleet server in Kibana.  
  ![Fleet Server Setup](path/to/image.png)

- **Deployed the agent** by running the script.  
  ![Agent Deployment](path/to/image.png)

- **Issue 2 solved**: Added a firewall rule so the fleet server can communicate (`ufw allow 9200` on the ELK server for Elasticsearch).  
  ![Firewall Rule 9200](path/to/image.png)

- Created a **policy for the Windows server** to install the agent and collect logs.  
  ![Windows Server Policy](path/to/image.png)

- **Allowed agent connection** on the fleet server (`ufw allow 8220`).  
  ![Agent Connection 8220](path/to/image.png)

- **Issue 3 solved**: Changed the fleet port from **443 to 8220** and added `--insecure` to handle the self-signed certificate issue.  
  ![Fleet Port Change](path/to/image.png)

- Confirmed **connection and logs** flowing into the fleet dashboard. **Success!**  
  ![Logs in Fleet Dashboard](path/to/image.png)

This concludes Week 1.

