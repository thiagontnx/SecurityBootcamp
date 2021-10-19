.. _detect_fa:

##############
File Analytics
##############

Defining Anomalies
==================

#. Within **Prism Central**, select :fa:`bars` **> Services > Files**.

#. Click on **File Servers** from the left-hand menu, and then click on **Manage** within the **Actions** column for **TheRocketFS**.

   .. figure:: images/manage.png

   A new window will appear sending you to **Prism Element**

#. Click on **TheRocketFS**, and then select **File Analytics**.

   .. figure:: images/fa01.png

   Your *File Analytics* dashboard will show metrics like *Top 5 active users*, *Top 5 accessed files* and *File Operations*.

   .. figure:: images/fa02.png

   While everything looks normal right now, those widgets are essential to detect unusual or anomalous behavior – such as repeated failed authentications, an increase in network traffic, or a large volume of file updates and touch-points.

   Let’s create an *Anomaly Rule* to detect suspicious activity based on action.

#. Click on the :fa:`fa-cog` **>** :fa:`plus` **Define Anomaly Rules**

   .. figure:: images/anomalyrules.png [TODO: Pete: Screenshot incorrect.]

#. Fill out the following information, click :fa:`fa-check-circle`, and then click **Save**.

   - **Events** - Rename
   - **Minimum Operation %** - 10
   - **Minimum Operation Count** - 50
   - **User** - All Users
   - **Type** - Hourly
   - **Interval** - 1

   Alternatively, you can send an *Anomaly Alert* to one or more email addresses

   .. figure:: images/defineanomaly.png

   .. note::

      This is a one time configuration. If you see this step already performed, proceed to the next step.

   In this step, we are mimicking what an attack or deliberately malicious behavior could look like. For example, a malicious script repeatedly accessing data, or someone trying to steal private information from the company.

   Let’s generate activity on the Files Server.
   
#. Within Prism Central, identify the IP address for your *USER##*\-WinTools VM, and utilizing RDP, log in using the following credentials:

   - **User Name** - administrator@ntnxlab.local
   - **Password** - nutanix/4u

#. Open *Windows Explorer*, right click on **This PC > Map Network Drive > \\\TheRocketFS.ntnxlab.local\\User##-FaceRace**

   .. figure:: images/winmap.png [TODO: Pete: This needs a better screenshot.]

#. Within your *USER##*\-WinTools VM, download `Sample Data <https://peerresources.blob.core.windows.net/sample-data/SampleData_Small.zip>`_, and extract it to **Z:\**.

#. Open **PowerShell**, and navigate to:

   .. code-block::

      Z:\Sample Data\Technical PDFs

#. Run the command: ``Get-ChildItem *.pdf | foreach {start-process $_.fullname}``.

   Your WinTools VM will open 99 .PDF files within your browser.

   .. figure:: images/pdf.png

#. Return to *File Analytics*, and then select :fa:`bars` **> Audit Trails**.

#. Check **Users** and search for **adminuser##**

#. Under the **Action** column, click **View Audit**.

#. Within the *Filter by Operations* box, select **Read**, and then click **Apply**.

   .. figure:: images/audit.png

#. Since you have already defined such behavior as an anomaly, navigate to :fa:`bars` **> Anomalies**. You may see a warning message under *Anomalies Alerts*. This may take up to one hour.

   .. figure:: images/anomalerts.png

   .. figure:: images/anomareport.png

   This is the exact expected behavior when your environment is being attacked, and *File Analytics* helps identify anomaly trends in your environment.