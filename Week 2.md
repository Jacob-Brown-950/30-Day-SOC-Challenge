## Week 2

1. **Downloaded Sysmon onto Windows Server**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2022%20Downloaded%20Sysmon%20via%20RDP%20Connection.PNG)

2. **Downloaded a popular config file (Olaf config)**  
   - Make sure to put this into the Sysmon folder  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2023%20Popular%20config%20for%20sysmon%2C%20download%20this%20file%20to%20the%20sysmon%20folder!.PNG)

3. **Running it in PowerShell as an admin**  

4. **Downloaded Sysmon, used Event Viewer and Services application to see it load as a service in real time**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2024%20Successful%20Sysmon%20and%20install%20and%20seeing%20it%20in%20real%20time%20become%20a%20process.PNG)

5. **Opening Sysmon in Event Viewer and seeing Event IDs and logs**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2025%20Just%20seeing%20the%20event%20IDs%20being%20generated%20by%20sysmon.PNG)

6. **On our Kibana page, go add the custom Windows Event Logs integration**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2025%20On%20kibana%2C%20go%20add%20the%20custom%20windows%20event%20logs%20integrations%20so%20we%20can%20ingest%20sysmon.PNG)

7. **Getting channel name for Sysmon**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2026%20Get%20your%20channel%20name%20so%20you%20can%20fill%20in%20info%20when%20adding%20custom%20windows%20event%20logs.PNG)

8. **Enter info to get Sysmon logs**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2027%20Enter%20info%20for%20sysmon%20event%20log%20integration.PNG)

9. **Adding this to my existing policy for my project**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2028%20add%20to%20your%20existing%20policy%20for%20the%20project.PNG)

10. **Doing the same for Windows Defender, but I only want certain events to reduce too many logs (1116, 1117, and 5001)**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2029%20same%20process%20as%20sysmon%20for%20defender%2C%20but%20add%20specific%20event%20IDs%20you%20find%20important%20on%20the%20documentation.PNG)

11. **Now my policies are up and running, this is how it should look**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2030%20Verify%20policies%20are%20now%20up%20and%20running.PNG)

12. **Well, not getting any logs, so let’s troubleshoot**  

13. **All I had to do was add a firewall policy in Vultr to allow port 9200**  
   - Personally, I chose to allow from anywhere, just so it’s not a hassle in the future  

14. **We got logs!**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2031%20We%20got%20logs!.PNG)

15. **Spinning up Linux server**  

16. **Since this is public-facing, we can already see a failed login attempt from a malicious IP! Pretty cool**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2032%20looking%20at%20failed%20logon%20attempts%20already.PNG)

17. **Now we’re going to install our Elastic Agent onto our Ubuntu server**  

18. **Creating a new policy for Linux endpoint**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2033%20We%20are%20going%20to%20create%20a%20new%20agent%20policy.PNG)

19. **Looking at what logs it’s going to be ingesting**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2034%20We%20can%20see%20here%20what%20logs%20we%20are%20ingesting%20for%20linux%20endpoints.PNG)

20. **Now adding a new agent and running the curl script**  
   - Remember what happened last time? We’re using a self-signed certificate, so use `--insecure` at the end of the script

21. **Agent connected**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2036%20Looking%20good!%20Our%20agent%20has%20been%20connected.PNG)

22. **Seeing if we are ingesting logs, looks like we are!**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2037%20seeing%20if%20we%20are%20successfully%20getting%20those%20logs.PNG)

24. **Set up a query for failed login attempts with some additional columns of interesting info**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2038%20Setting%20up%20a%20query%20in%20our%20data%20to%20filter%20Failed%20login%20attempts%2C%20include%20IP%2C%20username%2C%20and%20region%20used.PNG)

25. **Go save your search and let’s create a new rule**  
   - Here’s what mine looks like. This is not a great alert since it’ll generate lots of unnecessary alerts, but I want to generate these for my project!  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2040%20Creating%20the%20query%20rule%2C%20and%20implementing%20it.PNG)

26. **Created a map to put on my dashboard for failed authentication attempts**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2041%20Created%20a%20map%20to%20track%20the%20geolocation%20of%20failed%20authentication%20attempts.PNG)

27. **Did the same for successful authentication attempts**  

28. **Dashboard successfully created!**  
   ![image](https://github.com/Jacob-Brown-950/30-Day-SOC-Challenge/blob/main/Screenshots/Step%2042%20Dashboard%20Successfully%20Created.PNG)

- This concludes Week 2

