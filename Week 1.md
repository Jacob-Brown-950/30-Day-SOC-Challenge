# Week 1: ELK Stack Setup and Fleet Server Configuration

## Overview
Hey everyone! In Week 1, I dove into setting up the ELK stack and configuring the Fleet Server. It wasn't all smooth sailing, but I learned a lot along the way and wanted to share the experience, tips, and some advice to help you out if you're setting this up for yourself.

---

### 1. Network Diagram
- **Created a logical diagram** to represent the network, including the threat actor. Here's a key point: I placed the Windows and Ubuntu servers outside the VPC. Why? Because if someone manages to compromise one of these servers, they could gain access to the entire network. Keep that in mind when designing your network for security!

  ![Network Diagram](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Network%20Logical%20View.png)

### 2. VPC Setup
- **Created a VPC 2.0 network** in Vultr. The setup was pretty straightforward, but if you're unfamiliar with Vultr, make sure you check out their docs. Setting up a secure environment from the get-go makes a world of difference later on.  
  ![VPC Setup](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%202%20Click%20%22Add%20VPC%202.0%22.png)

### 3. Server Configuration
- **Set up my Ubuntu 22.04 server VM** and ran updates. Pro tip: Always update your server after setting it up. It avoids compatibility issues down the line.
  
- **Downloaded Elasticsearch** (`deb x86_64`) and configured the `elasticsearch.yml` file. At this point, it's a good idea to keep a backup of your configuration files just in case you make any changes and something breaks.
  ![Elasticsearch Download](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%203%20Downloading%20Elasticsearch.png)

- *(Optional)* Added a firewall group to restrict access. This is where things got tricky. By locking down the firewall too tightly, I ended up blocking some important ports I needed later on, so I had to go back and allow those manually. If you're going the extra mile on security, make sure you have a list of the ports you'll need ahead of time.

- **Confirmed Elasticsearch is running** successfully. Make sure to note this information somewhere. You don't want to lose access after all that work!  
  ![Elasticsearch Running](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%204%20Make%20Sure%20You%20Save%20This%20info!.png)

- **Using the public IP** for Elasticsearch was the way to go. It made it easier to access later.  
  ![Find Public IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%205%20Set%20it%20to%20this%20so%20you%20can%20access%20it%20via%20SOC%20Laptop.png)

- **Configuring the `elasticsearch.yml` file**: Make sure to uncomment the port and IP settings in the config file. It's easy to overlook this step, and you might find yourself locked out without knowing why.  
  ![Configure yml File](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%206%20Configure%20elasticsearch%20yml%20file.png)

- **Downloaded and configured Kibana** (`deb x86_64`). Same process as Elasticsearch, but I made sure to match all the IPs and ports properly between them.  
  ![Kibana Configuration](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%207%20Configure%20Kibana%20yml.png)

- Saved the **Elasticsearch Token** for future use. You’ll need this to connect Kibana to Elasticsearch.  
  ![Elasticsearch Token](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%208%20Get%20your%20Token.png)

### 4. Troubleshooting
- **Firewall blocking ports** was a big hurdle. Initially, I only allowed port 22, forgetting about Kibana's port. I used `ufw allow 5601` to fix that. Lesson learned: Plan out your firewall rules carefully before diving in.
  
- **Entered the Kibana enrollment token** in the web GUI, got my **verification code**, and was good to go!
  ![Kibana Access](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%209%20Got%20in%20to%20Kibana!%20now%20paste%20your%20key%20in.png)

- **API Integration issues**: Turned out I needed to add Kibana encryption keys into the keystore to get it running. If you run into this issue, this step is a lifesaver.
  ![Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2011%20Get%20your%20encryption%20keys.png)

- Entering each key into the keystore manually was time-consuming but necessary.  
  ![Enter Kibana Keys](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2012%20Enter%20those%20keys%20into%20the%20keystore.png)

### 5. Additional Changes
- I decided to **expose RDP to the internet** (yes, risky, I know!) to generate some failed login attempts for later investigations. If you’re doing this too, make sure to keep it locked down once you're done. Always take security seriously!

### 6. Fleet Server Setup
- **Set up a Fleet Server** pointing to the Vultr fleet server in Kibana. This part was fairly smooth.  
  ![Got Fleet Server IP](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2013%20Get%20Public%20IP%20of%20Fleet%20Server%20.png)  
  ![Configure Fleet](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2014%20Point%20Fleet%20Server%20in%20Kibana%20to%20IP.png)

- Adjusted firewall rules to allow the fleet server connection.  
  ![Firewall Rule Adjustment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2016%20Add%20firewall%20rule%20to%20allow%20fleet%20server%20connection.png)

- **Deployed the agent** on my servers and everything synced up beautifully.  
  ![Agent Deployment](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2017%20Agent%20Installed%20Successfuly!%20.png)

- Created a **policy for my Windows server** to collect logs and made sure everything was connected via the fleet server. If you're doing the same, don't forget to allow port **8220** for the agent connection!

- Ran into another small issue: I had to **change the fleet port** from 443 to 8220 and add `--insecure` to deal with self-signed certs. If you’re using self-signed certs like I am, this will save you a headache.  
  ![Fleet Port Change](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2018%20Go%20to%20fleet%20and%20change%20the%20port!.png)  
  ![Script Modification](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2019%20Fix%20the%20script%20and%20run%20again%2C%20success.png)

- Finally, I saw **logs flowing into the fleet dashboard**. That's the moment you know everything is working!  
  ![Logs in Fleet Dashboard](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2021%20See%20if%20you%20got%20logs!%20.png)

---

This is all for Week 1! in **Week 2**, we’ll dive into using Sysmon to monitor and log system activity on Windows.
