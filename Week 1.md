## Week 1: ELK Stack Setup and Fleet Server Configuration

Hey everyone! Welcome to Week 1 of the **30-Day SOC Analyst Challenge**. This week, I jumped into setting up the **ELK stack** and got the **Fleet Server** configured. There were a few bumps along the way, but I’ve learned a ton and will walk you through everything I did, why I did it, and share some helpful tips to make your setup process smoother if you're following along.

---

### 1. **Created a Network Diagram**
- I started off by creating a **logical network diagram** to visualize the setup, including the threat actor. One important thing to note: I placed the Windows and Ubuntu servers **outside the VPC**. Why? Because if an attacker manages to compromise one of these servers, they could gain access to the entire network. Something to keep in mind when designing your network!  
  ![Network Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Network%20Logical%20View.PNG)

### 2. **VPC Setup**
- Next, I set up a **VPC 2.0 network** in Vultr. It was a pretty straightforward process, but if you’re new to Vultr, I recommend checking out their documentation for a smooth setup. A secure environment from the start can save you headaches later on!  
  ![VPC Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%202%20Click%20%22Add%20VPC%202.0%22.png)

### 3. **Server Configuration**
- **Set up my Ubuntu 22.04 server VM** and ran updates. A quick tip: always update your server immediately after setting it up to avoid compatibility issues later.  
- **Downloaded Elasticsearch** (`deb x86_64`) and configured the `elasticsearch.yml` file. It’s a good idea to **back up your configuration files**—you never know when you’ll need to roll back a change.  
  ![Elasticsearch Download](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%203%20Downloading%20Elasticsearch.png)
  
- *(Optional)* I added a **firewall group** to restrict access. This was where things got tricky: I accidentally blocked some important ports and had to go back and adjust them manually. If you’re locking down your firewall, make sure you have a list of the ports you need ahead of time.

- **Confirmed Elasticsearch was running** successfully. Be sure to note this info somewhere so you don’t lose access down the road.  
  ![Elasticsearch Running](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%204%20Make%20Sure%20You%20Save%20This%20info!.png)

- I used the **public IP** for Elasticsearch, which made it easier to access later.  
  ![Find Public IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png)

- **Configured the `elasticsearch.yml` file**: Don’t forget to uncomment the port and IP settings. This is an easy step to overlook, and you might find yourself locked out without realizing why.  
  ![Configure yml File](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%206%20Configure%20elasticsearch%20yml%20file.png)

- **Downloaded and configured Kibana** (`deb x86_64`), which followed the same process as Elasticsearch, but I made sure to match the IPs and ports correctly.  
  ![Kibana Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%207%20Configure%20Kibana%20yml.png)

- Saved the **Elasticsearch Token** for future use. You’ll need this to connect Kibana to Elasticsearch.  
  ![Elasticsearch Token](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%208%20Get%20your%20Token.png)

### 4. **Troubleshooting**
- **Firewall blocking ports** was a big hurdle. Initially, I only allowed port 22 for SSH access and forgot about Kibana’s port. I used `ufw allow 5601` to fix that. Lesson learned: Plan out your firewall rules carefully!  
- **Entered the Kibana enrollment token** in the web GUI, got my **verification code**, and was good to go!  
  ![Kibana Access](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%209%20Got%20in%20to%20Kibana!%20now%20paste%20your%20key%20in.png)

- **API Integration issues**: Turned out I needed to add **Kibana encryption keys** into the keystore to get it running. If you run into this issue, this step is a lifesaver.  
  ![Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2011%20Get%20your%20encryption%20keys.png)

- Manually entering each key into the keystore was time-consuming but necessary to get everything working.  
  ![Enter Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2012%20Enter%20those%20keys%20into%20the%20keystore.png)

### 5. **Additional Changes**
- I took a slightly risky step and **exposed RDP to the internet** to generate some failed login attempts for later analysis. If you do the same, make sure to **lock it back down** after you’re done. Security first, always!

### 6. **Fleet Server Setup**
- **Set up a Fleet Server** pointing to the Vultr fleet server in Kibana. This part was smooth sailing once everything was configured.  
  ![Got Fleet Server IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2013%20Get%20Public%20IP%20of%20Fleet%20Server%20.png)  
  ![Configure Fleet](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2014%20Point%20Fleet%20Server%20in%20Kibana%20to%20IP.png)

- Adjusted **firewall rules** to allow the fleet server connection.  
  ![Firewall Rule Adjustment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2016%20Add%20firewall%20rule%20to%20allow%20fleet%20server%20connection.png)

- **Deployed the agent** on my servers and everything synced up perfectly.  
  ![Agent Deployment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2017%20Agent%20Installed%20Successfuly!%20.png)

- Created a **policy for my Windows server** to collect logs, and made sure everything was connected via the fleet server. Don’t forget to allow port **8220** for the agent connection!

- Ran into a small issue: I had to **change the fleet port** from 443 to 8220 and use `--insecure` to deal with self-signed certificates. If you’re using self-signed certs, this step will save you some headaches.  
  ![Fleet Port Change](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2018%20Go%20to%20fleet%20and%20change%20the%20port!.png)  
  ![Script Modification](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2019%20Fix%20the%20script%20and%20run%20again%2C%20success.png)

- Finally, I saw **logs flowing into the fleet dashboard**—a rewarding moment when you know everything is working as expected!  
  ![Logs in Fleet Dashboard](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2021%20See%20if%20you%20got%20logs!%20.png)

---

That wraps up Week 1! In **Week 2**, we’ll dive into using **Sysmon** to monitor and log system activity on Windows. Stay tuned for more!
