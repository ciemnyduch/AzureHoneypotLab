# Microsoft Azure Sentinel (SIEM) Honeypot Lab | Attack Map


##Thumbnail here


Credit to Joshua Madakor for this lab! [Video](https://www.youtube.com/watch?v=RoZeVbbZ0o0&list=PL_MvTIq1Tl-X04__sDhuQ89qo-g72DaBt&index=4&ab_channel=JoshMadakor)


### Description:
---


### Requirements & Tools:
---
1. Microsoft Azure Account
2. Third-party API: [ipgeolocation.io](https://ipgeolocation.io/)
3. Remote Desktop Protocol (RDP)
4. Powershell + Powershell [script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1) by Joshua Madakor
5. Azure Services


### Step 1: Create a Microsoft Azure Account
---
![image](https://github.com/user-attachments/assets/8deb7d76-7110-4e33-a772-00f1729dace2)

1. Create a free account on [Microsoft Azure](https://azure.microsoft.com/en-us/pricing/purchase-options/azure-account/search?ef_id=_k_CjwKCAiAmrS7BhBJEiwAei59i3nqC3P5eSWkXJuQuRKl1vvCL5bVSqYkn9AK-M-MmtREPbZqCM1HmBoCZqcQAvD_BwE_k_&OCID=AIDcmmfq865whp_SEM__k_CjwKCAiAmrS7BhBJEiwAei59i3nqC3P5eSWkXJuQuRKl1vvCL5bVSqYkn9AK-M-MmtREPbZqCM1HmBoCZqcQAvD_BwE_k_&gad_source=1&gclid=CjwKCAiAmrS7BhBJEiwAei59i3nqC3P5eSWkXJuQuRKl1vvCL5bVSqYkn9AK-M-MmtREPbZqCM1HmBoCZqcQAvD_BwE)
2. New accounts recieve a $200 credit.
### Step 2: Deploy and set up a Virtual Machine as a honeypot
---
* Start by creating the Virtual Machine (VM)
  
![image](https://github.com/user-attachments/assets/29c6cd0a-91f2-469e-a064-a8f5eb99ce69)

* Create Username and Password

![image](https://github.com/user-attachments/assets/6314c575-b371-4e05-b36a-a511ac714048)


![image](https://github.com/user-attachments/assets/01f3b16d-e865-4568-a34d-bb94dd96a6f0)

* Default Disk Settings
  
  * Go to Networking, switch from basic to advanced
  
  ![image](https://github.com/user-attachments/assets/9cabfaa7-0ca0-49f8-bd2e-10a385f15333)

  * Delete current inbound rule and create new inbound rule

![image](https://github.com/user-attachments/assets/f6e31f8f-347d-432c-ba51-a2a14b42a765)

![image](https://github.com/user-attachments/assets/16823d5a-6aac-4be6-8b4e-ecd532f1a514)

* Deploy Virtual Machine

![image](https://github.com/user-attachments/assets/525b9200-cdd4-4991-9cea-bd8c0712598e)

### Step 3: Log Analytics Workspace
---
* Select "Create Log Analytics Workspace" and place it in the same resource group
* Add it to the same region you selected

  ![image](https://github.com/user-attachments/assets/987b1652-fe38-44fe-b24e-8354728d2c56)

### Step 4: Setup Microsoft Defender for Cloud
---
* Search for "Microsoft Defender for Cloud"
* Under Management navigate to "Environment settings", open subscription and the Analytics Workspace named
  
![image](https://github.com/user-attachments/assets/fe3a0001-928b-4c8a-9e70-756af883a315)

* Go into Defender plans
* Turn both Cloud Security Posture Management and Servers to ON. 
* Leave SQL servers on machines OFF

![image](https://github.com/user-attachments/assets/d8190399-7640-441d-9367-1a67e4264d2d)

* Select All events under data collection

![image](https://github.com/user-attachments/assets/f0b99ba9-00ee-4089-92db-c2b5fd58fc6e)


* Click "Save" for each
  
### Step 5: Connect the Log Analytics Workspace to the Virtual Machine
---

* Go to Log Analytics Workspaces and Virtual Machines
* Hit connect

![image](https://github.com/user-attachments/assets/ac8f4608-2fb2-45f8-8461-b456d90fbe3e)

![image](https://github.com/user-attachments/assets/00c23dc1-1810-402b-8005-6e3bc02e9097)

### Step 6: Microsoft Sentinel
---

* Search for "Microsoft Sentinel"
* Connect workspace
* Click Log Analytics Workspace name and Add
  
  ![image](https://github.com/user-attachments/assets/63220bfc-a658-48cb-bfc6-54591663803d)

### Step 7: Disabling the Virtual Machine's Firewall
---

* Log into the Virtual Machine via RDP
* Type wf.msc in Start, then go to windows Defender Firewall Properties and turn the firewall off for Domain, Private and Public Profiles.
  
![image](https://github.com/user-attachments/assets/8997cdbc-0951-4610-a45c-53ccacd6f1eb)
  
* Ping the VM from your host
  
![image](https://github.com/user-attachments/assets/33bd436e-2232-4d6e-941c-dceda9306aa7)




### Step 8: Scripting the Security Log Exporter
---

* Copy this [script](https://github.com/joshmadakor1/Sentinel-Lab/blob/main/Custom_Security_Log_Exporter.ps1) (Authored by Joshua Madakor)
  
  ![image](https://github.com/user-attachments/assets/2b62bfb2-1d27-44df-94fa-d06c57b38baf)

* Open the script in Powershell ISE on the VM
  
  ![image](https://github.com/user-attachments/assets/00fd8afa-c931-4f7b-a7bd-63e871ae30a8)

* This next part requires an account with [ipgeolocation.io](https://ipgeolocation.io/)
* Use the API key and paste it in place of the API key in the script
* Save the script as "log-exporter"

  * Run the script and navigate to C:\ProgramData\failed_rdp
  * Copy the contents of failed_rdp
  * Warning: don't share your API key

### Step 9: Creating a custom log in Log Analytics Workspace
---

* In Log Analytics Workspace create a custom log by selecting Tables and New custom log (MMA-based)
* This allows data from the previous script to be ingested

![image](https://github.com/user-attachments/assets/ed13ac1d-ff19-4a60-b2cb-b18d5ca381bf)

* Select the copied "failed_rdp.log" file as the log sample

![image](https://github.com/user-attachments/assets/82da1910-da41-4ccb-b4db-fc2574f165d6)

* Default settings for Record delimiter

  * Choose Windows for Collection paths
  * For the path put: C:\ProgramData\failed_rdp.log
  * Name the custom log
  
![image](https://github.com/user-attachments/assets/0b79d68b-983e-4a30-a9f1-0e14b0ef1216)

* Finally click create

### Step 10: Query the Custom Log with KQL
---

### Step 11: Create World Attack Map in Microsoft Sentinel
---

### Step 12: Shut Down Resources
---


### Learning Objectives Completed:
---


