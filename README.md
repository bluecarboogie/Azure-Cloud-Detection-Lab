<h1>Azure Cloud Detection Lab</h1>

### [YouTube Demonstration](https://youtu.be/YOUR_YOUTUBE_VIDEO_LINK)

<h2>Description</h2>
The Azure Cloud Detection Lab is a comprehensive cybersecurity project designed to detect and respond to security threats within the Microsoft Azure cloud environment. This lab is entirely cloud-based, utilizing Microsoft Azure services and Microsoft Sentinel for advanced threat detection and monitoring.

<h2>Languages and Utilities Used</h2>

- Microsoft Azure
- Microsoft Sentinel

<h2>Environments Used</h2>

- Microsoft Azure Cloud Platform

<h2>Lab Walk-through:</h2>

<p align="center">
1. First I created a resource group which will contain a windows virtual machine, 
 azure sentinel resources and the log analytics workspace : <br/>
<img src="https://i.ibb.co/4tgPsHf/1-creating-resource-group.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
2. Then i created a windows virtual machine :  <br/>
<img src="https://i.ibb.co/FYJPTX5/2create-VM-1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
3 <br/>
<img src="https://i.ibb.co/FHnny86/3create-VM.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
4  <br/>
<img src="https://i.ibb.co/VtgshBm/4create-VM-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
5  <br/>
<img src="https://i.ibb.co/HX7wbhS/5create-VM-3.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
6. The virtual machine will be accessed via RDP(remote desktop protocol) this unfortunately leaves the public facing virtual machine open to being attacked via password brute forcing or a dictionary attack if the virtual machine’s ip address were to be scanned. To mitigate this risk a feature called Just In Time Access is enabled. Just In Time Access allows the virtual machine to only be accessed when a request is made and only can be accessed by the requester and can be restricted to certain IP addresses. :  <br/>
<img src="https://i.ibb.co/BBNw0pZ/6labvm-with-just-in-time-this-one.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
7. Next I am going to make a log analytics workspace that will store and log data collected from within the resource group. Additionally Microsoft sentinel(SIEM) will be added to the log analytics workspace 
:  <br/>
<img src="https://i.ibb.co/hXJy0Dg/7add-microsoft-sentinal-to-workspace.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
8. Microsoft Sentinel Overview:  <br/>
<img src="https://i.ibb.co/BLbGKL9/8microsoft-sentinal-overview-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
9. Create Log Analytics Workspace:  <br/>
<img src="https://i.ibb.co/p0frzzp/9create-log-analytics-workspace-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
10. Next i am going to use data connectors to get the data that will be collected into sentinel and create a data collection rule:  <br/>
<img src="https://i.ibb.co/pyvNZHR/10microsoft-data-connectors-1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
11. Windows Security Events via Azure Monitor Agent (AMA) - Being added to VM:  <br/>
<img src="https://i.ibb.co/X4T30QP/11windows-security-events-via-ama-being-added-to-vm.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
12. Windows Security Events via Azure Monitor Agent (AMA) - Data Collection Rule 1:  <br/>
<img src="https://i.ibb.co/9wmXWMF/12windows-security-events-via-ama-data-collection-rule1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
13. Windows Security Events via Azure Monitor Agent (AMA) - Data Collection Rule 2:  <br/>
<img src="https://i.ibb.co/LQ1MNHD/13windows-security-events-via-ama-data-collection-rule2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
14. Now i am going to make sure than everything is working by seeing if azure has registered the VM being logged into :  <br/>
<img src="https://i.ibb.co/3hZnYG1/14-VM-event-viewer.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
15. VM Event Viewer - Windows Security Events:  <br/>
<img src="https://i.ibb.co/VgNjwfj/15-VM-event-viewer1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
16. In the windows event viewer we can find out that the event ID for logging in is 4624 :  <br/>
<img src="https://i.ibb.co/hBQyK75/16-VM-event-viewer2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
17. VM Event Viewer - Windows Security Events:  <br/>
<img src="https://i.ibb.co/Rc1KQkd/17-VM-event-viewer3.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
18. Now we’re going to plug in the ID number into sentinel:  <br/>
<img src="https://i.ibb.co/GsJxbxC/18microsoft-sentinal-logs1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
19. Microsoft Sentinel Logs:  <br/>
<img src="https://i.ibb.co/W64tXTP/19microsoft-sentinal-logs-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
20. Sentinel uses the KQL language for data searching, when the ID number for logging in is inputted we can see that sentinel is working and is receiving logs:  <br/>
<img src="https://i.ibb.co/9sDWpy0/19microsoft-sentinal-logs-5.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
21. Microsoft Sentinel Logs:  <br/>
<img src="https://i.ibb.co/BcQRCGt/20microsoft-sentinal-logs-6.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
22. Scheduled tasks can be used by malicious actors as a persistence technique to stay on a victim machine https://attack.mitre.org/techniques/T1053/ :  <br/>
<img src="https://i.ibb.co/4ZVFkPV/21mitre-scheduled-task-attack-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
23. Now I'm going to create a custom rule that will detect whenever a certain scheduled task has been executed on the windows virtual machine, but first I will configure the virtual machine.:  <br/>
<img src="https://i.ibb.co/sj24wwh/22-VM-event-viewer-configuring.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
24. VM Event Viewer - Configuring:  <br/>
<img src="https://i.ibb.co/s1PTzWX/23-VM-event-viewer-configuring1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
25. VM Event Viewer - Configuring:  <br/>
<img src="https://i.ibb.co/JsR6V3n/24-VM-event-viewer-configuring2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
26. VM Event Viewer - Configuring:  <br/>
<img src="https://i.ibb.co/59k1B5w/25-VM-event-viewer-configuring3.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
27. Now I am going to create my malicious task. The task will be a scheduled opening of Microsoft PowerShell via the Windows task scheduler:  <br/>
<img src="https://i.ibb.co/Vx8mXHh/26-VM-creating-malicious-task.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
28. VM - Creating Malicious Task:  <br/>
<img src="https://i.ibb.co/0czc6NY/27-VM-creating-malicious-task1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
29. VM - Creating Malicious Task:  <br/>
<img src="https://i.ibb.co/3dgmgVk/28-VM-creating-malicious-task2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
30. VM - Creating Malicious Task:  <br/>
<img src="https://i.ibb.co/tLHCGyQ/29-VM-creating-malicious-task3.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
31. This shows that the scheduled task has been executed, now i'm going to use the provided event ID in microsoft sentinel:  <br/>
<img src="https://i.ibb.co/Ry1zRz1/30-VM-creating-malicious-task5.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
32. Looks like the scheduled tasks are showing up in sentinel, but they're not giving much data with the given KQL prompt so I am going to add more to it:  <br/>
<img src="https://i.ibb.co/Bygv68s/31microsoft-sentinal-logs-after-malicious-task.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
33. Now we are getting more information which would be pertinent during an investigation:  <br/>
<img src="https://i.ibb.co/bmpDsX8/32microsoft-sentinal-logs-after-malicious-task2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
34. Now I am going to create a query rule so that scheduled tasks will be logged in the Microsoft Sentinel incidents tab:  <br/>
<img src="https://i.ibb.co/C0h9KKy/33-Microsoft-sentinal-analytics.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
35. Microsoft Sentinel Analytics:  <br/>
<img src="https://i.ibb.co/z5TPhhs/34-Microsoft-sentinal-analytics-post-1.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
36. Microsoft Sentinel Analytics:  <br/>
<img src="https://i.ibb.co/82fvT9F/35-Microsoft-sentinal-analytics-post-2.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
37. Microsoft Sentinel Analytics:  <br/>
<img src="https://i.ibb.co/yQt64mM/36-Microsoft-sentinal-analytics-post-3.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
38. Microsoft Sentinel Analytics:  <br/>
<img src="https://i.ibb.co/zH9x0r9/37-Microsoft-sentinal-analytics-post-4.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
39. Microsoft Sentinel Analytics:  <br/>
<img src="https://i.ibb.co/3dZ5899/38-Microsoft-sentinal-analytics-post-5.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
<br />
<br />
40. This is the Sentinel incidents page after implementing our custom rule:  <br/>
<img src="https://i.ibb.co/tLMgyXV/39-36-2023-07-22-07-32-34-Untitled-Notepad.png" height="80%" width="80%" alt="Azure Cloud Detection Lab"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
