.. _detect_objects:

------------------------------------------------
Nutanix Objects
------------------------------------------------

Configuring WORM
+++++++++++++

You know the storage administrators for Blips and Chipz have created an object storage for Mortynight Run, the video surveillance system, and it needs archive data for regulatory purposes and improved security.
Your task will be to guarantee that the policies set for the repository are following your security guidelines.


Create Bucket In Prism
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

A bucket is a repository within an object store that can have policies applied to it, such as versioning, WORM (Write Once, Read Many), etc. By default, a newly created bucket is a private resource to the creator. The creator of the bucket by default has read/write permissions and can grant permissions to other users.
Go to Prism Central menu > Services > Objects
Click on the existing Object Store (mortynightrun) to manage it.
Check the existing user##-bucket and click Actions > Configure WORM to view its settings:

You realize your colleagues didn’t enable WORM and Versioning settings, so you have to do it yourself to protect the company’s data from attackers and for audit purposes.

Click Enable Version
Click Enable WORM and set the Retention Period to 3 years
Click Enable WORM to save the changes
Go back to Object Store landing page and check your bucket (user##-bucket) again then Actions > Update
Now set Permanently delete past versions after 3 months
Note:
You can configure WORM settings to align with your company’s security policy.
After you commit to these configurations, you will have a 24-hour grace period window where you can disable its settings, after 24 hours you can no longer change it and the system will follow this behavior, not even Nutanix support can modify it.

Click Save.
Note
WORM storage prevents the editing, overwriting, renaming, or deleting of data and is crucial in heavily regulated industries (finance, healthcare, public agencies, etc.) where sensitive data is collected and stored. Examples include emails, account information, voice mails, and more.
Note
Note that if WORM is enabled on the bucket, this will supersede any lifecycle policy, in this case, you set it to 3 years.

User Management
In this exercise, you will generate access and secret keys to access the object store that will be used throughout the lab.
In Prism Central, select  > Services > Objects
Click on Access Keys and click Add People.

Select Add people not in a directory service and enter your e-mail address.

Click Next.
Click Generate Keys to generate a key.

Click Download Keys to download a .txt file containing the Access Key and Secret Key.

Click Close.
Open the file with a text editor.


Note
Keep the text files open so that you have the access and secret keys readily available for future labs.
INFORMATIONAL ONLY - NO NEED TO TAKE ACTION
For security audits, you can revoke or renew access keys.
 Click on the Access Keys again

Select your user and click Manage on the far right side
You can select + Add Key to generate a new Access Key to this user or select its Access Key displayed and revoke access by clicking on the Delete button.
INFORMATIONAL ONLY - NO NEED TO TAKE ACTION
 
 
 
 
Adding Users to buckets_share
From the Objects UI, click on Object Stores.
Within the Object Store list, click mortynightrun
Check the box next to your user##-bucket bucket, and click Share from the Actions dropdown.
This is where you will be able to share your bucket with other users. You can configure read access (download), write access (upload), or both, on a per user basis.
Select the user you created earlier, with Read and Write permissions.
Click Save.


OBJECTS: VERSIONING AND ACCESS CONTROLS
Accessing & Creating Buckets With Objects Browser
In this exercise, you will use Objects Browser to create and use buckets in the object store using your generated access key.
Download the Sample Images
Click here to download the sample images to your local computer. Once the download is complete, extract the contents of the .zip file.
Use Object Browser to Create A Bucket
From the Objects UI, Locate the Objects Public IPs.

In a new browser tab paste the Objects Public IP, and add port 7200.

Enter the following fields for the user-created earlier, located in the .txt file, and click the Login button:
Access Key - Generated When User Created
Secret Key - Generated When User Created

Click the + and Upload file.
Navigate to the directory where you extracted the sample pictures, and upload one picture to your bucket. You may optionally repeat this process to upload multiple pictures.
Nutanix provides an intuitive interface to manage your object storage buckets and that is how easy it is to use the Objects Browser.
Object Versioning
Object versioning allows the upload of new versions of the same object for required changes, without losing the original data. Versioning can be used to preserve, retrieve and restore every version of every object stored within a bucket, allowing for easy recovery from unintended user action and application failures.
Open Notepad on your local machine.
Type “version 1.0” in Notepad, then save the file as UserXX.txt.
In Objects Browser, upload the text file to your user##-bucket bucket.
Make changes to the text file in Notepad and save it with the same name, overwriting the original file.
Upload the modified file to your bucket. If desired, you can update and upload the file multiple times.
Back in Prism, in the Objects UI, click on the ntnx-objects Object Store.
Look at the Num. Objects column for your user##-bucket bucket.



Note
You will see that there is an Object counted for every version of your test file. In the example above, I had three different files (two pictures and one text file) but within the text file, I have three different versions of it. Essentially, by keeping multiple versions of the same file, Nutanix Objects makes it possible to restore old versions at any point in time.
S3 compatible third-party tools can access previous versions of any given file for restoring purposes.
Since you chose Nutanix as your cloud provider, you now have a lot more time to do things you couldn’t before because you had to spend so much time operationalizing everything. It’s already Pub Time and you can safely get away from your desk for a couple of hours.
