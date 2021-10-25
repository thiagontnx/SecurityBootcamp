.. _detect_fa:

##############
File Analytics
##############

Defining Anomalies
==================

#. Within *Prism Central*, select :fa:`bars` **> Services > Files**.

#. Click on **File Servers** from the left-hand menu, and then click on **Manage** within the **Actions** column for **TheRocketFS**.

   .. figure:: images/manage.png

   A new browser tab will open.

#. Click on **TheRocketFS**, and then select **File Analytics**.

   .. figure:: images/fa.png

   Your *File Analytics* dashboard will show metrics for *Top 5 active users*, *Top 5 accessed files*, *File Operations*, and more.

   Everything looks normal right now. These widgets are essential to detect unusual or anomalous behavior, such as repeated failed authentications, an increase in network traffic, or a large volume of file updates and touch-points.

   Let’s create an *Anomaly Rule* to detect suspicious activity based on action.

#. Click on the :fa:`cog` **> Define Anomaly Rules >** :fa:`plus` **Define Anomaly Rules**.

   .. figure:: images/anomalyrules.png

#. Fill out the following information, click :fa:`check-circle`, and then click **Save**.

   - **Events** - Read
   - **Minimum Operation %** - 10
   - **Minimum Operation Count** - 50
   - **User** - All Users
   - **Type** - Hourly
   - **Interval** - 1

   Optionally, you can send an *Anomaly Alert* to one or more email addresses

   .. figure:: images/defineanomaly.png

   .. note::

      This is a one time configuration. If you see this step already performed, proceed to the next step.

   In this next step, we are mimicking what an attack or deliberately malicious behavior could look like. For example, a malicious script repeatedly accessing data, or someone trying to steal private information from the company.
   
#. Within Prism Central, identify the IP address for your *USER##*\-WinTools VM, and utilizing Windows Remote Desktop, log in using the following credentials:

   - **User Name** - adminuser##@ntnxlab.local (ex. adminuser01@ntnxlab.local) TODO: RDP rights not granted by default. Louie and I will work on this. Need a band-aid for now.
   - **Password** - nutanix/4u

#. Open *Windows Explorer*, right click on **This PC > Map Network Drive > \\\TheRocketFS.ntnxlab.local\\User##-FaceRace**. From the *Drive:* drop-down, select **F:**.

   .. figure:: images/winmap.png

#. Within your *USER##*\-WinTools VM, copy and paste the following link into Chrome to download the sample data `https://peerresources.blob.core.windows.net/sample-data/SampleData_Small.zip`. Once downloaded, click on it to open, and copy/paste the *Sample Data* folder to **F:\\**.

#. Open **PowerShell**, and navigate to ``F:\\Sample Data\\Technical PDFs``.

#. Run the command: ``Get-ChildItem *.pdf | foreach {start-process $_.fullname}``.

   This will open 99 PDF files within your browser.

#. Return to *File Analytics*, and then select :fa:`bars` **> Audit Trails**.

#. Select **Users** and search for **adminuser##**.

#. Under the **Action** column, click **View Audit**.

#. Within the *Filter by Operations* box, select **Read**, and then click **Apply**.

   .. figure:: images/audit.png

#. Since you have already defined this behavior as an anomaly, close this window, and then navigate to :fa:`bars` **> Anomalies**. Click on the *Anomaly Alerts* timeline.

   .. figure:: images/anomalerts01.png

	.. note::
		
		This may take up to one hour, so you may wish to move on, and circle back to check on this at a later time.

   .. figure:: images/anomalerts02.png

   .. figure:: images/anomareport.png

This is expected behavior when your environment is being attacked, and *File Analytics* helps identify anomaly trends in your environment.