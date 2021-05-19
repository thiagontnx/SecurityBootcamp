.. _detect_fa:

------------------------------------------------
Monitoring Data Services
------------------------------------------------

Files Analytics
++++++++++++++

In Prism Central > Services > Files > click on File Servers
Click on Manage in the Actions column from the File Server TheRocketFS 

A new window will appear sending you to Prism Element
Click on TheRocketFS and select File Analytics from the menu


Your Files Analytics Dashboard will show metrics like Top 5 active users, Top 5 accessed files and File Operations

While in your environment everything looks normal, those widgets are essential to detect unusual or anomalous behavior – such as repeated failed authentications, an increase in network traffic, or a large volume of file updates and touchpoints.
Let’s create an Anomaly Rule to detect suspicious activity based on action
Click on the gear > Define Anomaly Rules

Define Anomaly Rules
In Events, select Rename
Minimum Operation % 10
Minimum Operation Count 5
User All Users
Type Hourly
Interval 1
Click Check Mark, and then Save.

Note:
This is a one time configuration, if you see this step already performed, that means that you are  sharing your cluster with someone who has gone through it.
In this step we are mimicking what an attack or deliberately mean behavior should look like. Examples are a malicious script repeatedly accessing data or someone trying to steal multiple files, private information from the company.
Alternatively, you can send an Anomaly Alert to one or more email addresses
Now, let’s generate activity on the File Server, you will be required to connect to your User##-WinTools VM via RDP (preferred) or console, using NTNXLAB\adminuser## pass:  nutanix/4u. You can check its IP by going to Virtual Infrastructure > VMs > User##WinTools VM IP column
Once you connect to your User##WinTools VM, ensure that you have mapped out TheRocketFS File Server to drive Z:
If not mapped, open windows explorer, right click on computer > Map Network Drive > \\TheRocketFS.ntnxlab.local\User##-FaceRace

Open PowerShell console and navigate to Z:\Sample Data_Small\Sample Data\Technical PDFs and run the following command:
Get-ChildItem *.pdf | foreach {start-process $_.fullname}
Notice that your WinTools VM will open almost 100 pdf files at once.

Now, let's go back to File Analytics, hamburger menu > Audit Trails
Check Users and search for adminuser##
Under Action column, select Audit Trail
In Filter by Operations, select Read, and then click Apply.

Since you define such behavior as an Anomaly, if you go back to the Files Analytics menu (it takes 1 hour for the Anomaly scan to work, you might want to finish the next section and come back here), you should see a warning message under Anomalies Alerts

Go to hamburger menu > Anomalies and check the in-depth Anomaly report

Note:
This is the exact expected behavior when your environment is being attacked and File Analytics helps identify Anomaly trends in your environment.
