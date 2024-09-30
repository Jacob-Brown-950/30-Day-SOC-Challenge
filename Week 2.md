## Week 2

1. **Downloaded Sysmon onto Windows Server**  
   ![image](#)

2. **Downloaded a popular config file (Olaf config)**  
   - Make sure to put this into the Sysmon folder  
   ![image](#)

3. **Running it in PowerShell as an admin**  
   ![image](#)

4. **Downloaded Sysmon, used Event Viewer and Services application to see it load as a service in real time**  
   ![image](#)

5. **Opening Sysmon in Event Viewer and seeing Event IDs and logs**  
   ![image](#)

6. **On our Kibana page, go add the custom Windows Event Logs integration**  
   ![image](#)

7. **Getting channel name for Sysmon**  
   ![image](#)

8. **Enter info to get Sysmon logs**  
   ![image](#)

9. **Adding this to my existing policy for my project**  
   ![image](#)

10. **Doing the same for Windows Defender, but I only want certain events to reduce too many logs (1116, 1117, and 5001)**  
   ![image](#)

11. **Now my policies are up and running, this is how it should look**  
   ![image](#)

12. **Well, not getting any logs, so let’s troubleshoot**  
   ![image](#)

13. **All I had to do was add a firewall policy in Vultr to allow port 9200**  
   - Personally, I chose to allow from anywhere, just so it’s not a hassle in the future  
   ![image](#)

14. **We got logs!**  
   ![image](#)

15. **Spinning up Linux server**  
   ![image](#)

16. **Since this is public-facing, we can already see a failed login attempt from a malicious IP! Pretty cool**  
   ![image](#)

17. **Now we’re going to install our Elastic Agent onto our Ubuntu server**  
   ![image](#)

18. **Creating a new policy for Linux endpoint**  
   ![image](#)

19. **Looking at what logs it’s going to be ingesting**  
   ![image](#)

20. **Now adding a new agent and running the curl script**  
   - Remember what happened last time? We’re using a self-signed certificate, so use `--insecure` at the end  
   ![image](#)

21. **Agent connected**  
   ![image](#)

22. **Seeing if we are ingesting logs, looks like we are!**  
   ![image](#)

23. **Let’s create SSH brute force alerts and dashboard**  
   ![image](#)

24. **Set up a query for failed login attempts with some additional columns of interesting info**  
   ![image](#)

25. **Go save your search and let’s create a new rule**  
   - Here’s what mine looks like. This is not a great alert since it’ll generate lots of unnecessary alerts, but I want to generate these for my project!  
   ![image](#)

26. **Created a map to put on my dashboard for failed authentication attempts**  
   ![image](#)

27. **Did the same for successful authentication attempts**  
   ![image](#)

28. **Dashboard successfully created!**  
   ![image](#)

- This concludes Week 2

