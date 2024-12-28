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

* Create Username and Passport

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


### Step 6
### Step 7
### Step 8
### Step 9
### Step 10
### Step 11
### Step 12

### Learning Objectives Completed:
---


