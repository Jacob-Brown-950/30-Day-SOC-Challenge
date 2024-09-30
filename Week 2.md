## Week 2: Sysmon and Log Ingestion

This week, we focused on setting up Sysmon for Windows Server, integrating it with Kibana, and deploying Elastic Agents on our Ubuntu server. Below are the detailed steps taken during this process.

1. **Downloaded Sysmon onto Windows Server**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2022%20Downloaded%20Sysmon%20via%20RDP%20Connection.PNG)

2. **Downloaded a popular config file (Olaf config)**  
   - Make sure to place this config file into the Sysmon folder for optimal configuration.  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2023%20Popular%20config%20for%20sysmon%2C%20download%20this%20file%20to%20the%20sysmon%20folder!.PNG)

3. **Running Sysmon in PowerShell as an administrator**  

4. **Verified Sysmon installation using Event Viewer**  
   - Utilized the Services application to observe Sysmon loading as a service in real time.  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2024%20Successful%20Sysmon%20and%20install%20and%20seeing%20it%20in%20real%20time%20become%20a%20process.PNG)

5. **Opened Sysmon in Event Viewer to view Event IDs and logs**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2025%20Just%20seeing%20the%20event%20IDs%20being%20generated%20by%20sysmon.PNG)

6. **Added custom Windows Event Logs integration on Kibana**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2025%20On%20kibana%2C%20go%20add%20the%20custom%20windows%20event%20logs%20integrations%20so%20we%20can%20ingest%20sysmon.PNG)

7. **Obtained the channel name for Sysmon**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2026%20Get%20your%20channel%20name%20so%20you%20can%20fill%20in%20info%20when%20adding%20custom%20windows%20event%20logs.PNG)

8. **Entered necessary information for Sysmon logs integration**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2027%20Enter%20info%20for%20sysmon%20event%20log%20integration.PNG)

9. **Added Sysmon configuration to my existing policy**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2028%20add%20to%20your%20existing%20policy%20for%20the%20project.PNG)

10. **Configured Windows Defender to log specific events**  
    - Focused on important events (1116, 1117, and 5001) to reduce log volume.  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2029%20same%20process%20as%20sysmon%20for%20defender%2C%20but%20add%20specific%20event%20IDs%20you%20find%20important%20on%20the%20documentation.PNG)

11. **Verified that my policies are active**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2030%20Verify%20policies%20are%20now%20up%20and%20running.PNG)

12. **Troubleshooting: No logs received initially**  

13. **Adjusted firewall policy in Vultr to allow port 9200**  
    - Allowed access from anywhere for ease of future operations.  

14. **Successful log retrieval!**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2031%20We%20got%20logs!.PNG)

15. **Spun up a Linux server**  

16. **Observed a failed login attempt from a malicious IP**  
    - This reinforces the need for robust monitoring and response measures.  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2032%20looking%20at%20failed%20logon%20attempts%20already.PNG)

17. **Installing Elastic Agent on the Ubuntu server**  

18. **Created a new policy for Linux endpoint**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2033%20We%20are%20going%20to%20create%20a%20new%20agent%20policy.PNG)

19. **Reviewed logs to be ingested from the Linux endpoint**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2034%20We%20can%20see%20here%20what%20logs%20we%20are%20ingesting%20for%20linux%20endpoints.PNG)

20. **Added a new agent and executed the curl script**  
    - Used `--insecure` due to the self-signed certificate.  

21. **Agent successfully connected!**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2036%20Looking%20good!%20Our%20agent%20has%20been%20connected.PNG)

22. **Checked if we are ingesting logs; success!**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2037%20seeing%20if%20we%20are%20successfully%20getting%20those%20logs.PNG)

23. **Set up a query for failed login attempts with additional details**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2038%20Setting%20up%20a%20query%20in%20our%20data%20to%20filter%20Failed%20login%20attempts%2C%20include%20IP%2C%20username%2C%20and%20region%20used.PNG)

24. **Saved the search and created a new alert rule**  
    - This alert will generate numerous notifications, but it serves as a practical exercise for my project!  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2040%20Creating%20the%20query%20rule%2C%20and%20implementing%20it.PNG)

25. **Developed a map for the dashboard to track failed authentication attempts**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2041%20Created%20a%20map%20to%20track%20the%20geolocation%20of%20failed%20authentication%20attempts.PNG)

26. **Repeated the process for successful authentication attempts**  

27. **Dashboard successfully created!**  
    ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2042%20Dashboard%20Successfully%20Created.PNG)

This concludes Week 2 of the 30-Day SOC Analyst Challenge.
