## Week 1: ELK Stack Setup and Network Configuration

- **Created a logical diagram** to represent the network, including the threat actor.
- **Creating a VPC 2.0 network** in Vultr.
- **Set up my Ubuntu 22.04 server** and ran updates.
- **Downloaded Elasticsearch debx86_64** and configured the `elasticsearch.yml` file.
- *(Optional)* Added a firewall group setting to ensure only I can access the server, restricting access from the entire internet.
- **Successfully started and confirmed Elasticsearch** is running.
- **Downloaded Kibana debx86_64**, configured the `kibana.yml`, and started Kibana.
- **Issue 1 solved**: Firewall was only allowing port 22; ensured the port Kibana is on is allowed for remote access.
- **Ran `ufw allow 5601`** on the VM CLI to allow Kibana's port.
- **Pasted the enrollment token** on the web GUI.
- Received **verification code** and successfully completed the setup.
- Solved the **API integration error** by adding Kibana keys into the keystore.
- The **Kibana web GUI is fully functional**!
