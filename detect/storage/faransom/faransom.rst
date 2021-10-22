.. _detect_faransom:

####################################
File Analytics Ransomware Protection
####################################

File Analytics scans files for ransomware in real-time, and notifies you via email in the event of a ransomware attack. By using the Nutanix Files file blocking mechanism, File Analytics prevents files with signatures of potential ransomware from carrying out malicious operations. Ransomware Protection automatically scans for ransomware based on a curated list of signatures that frequently appear in ransomware files. Optionally, you can add additional signatures to the list.

File Analytics also monitors file shares for self-service restore (SSR) policies, and identifies shares that do not have SSR enabled in the ransomware dashboard. You can enable SSR through the ransomware dashboard by selecting shares identified by File Analytics.

Enabling Ransomware Protection
==============================

#. Within the *Files Analytics* dashboard, click :fa:`bars` **> Ransomware**.

#. Click **Enable Ransomware Protection**, and then click **Enable**.

   .. note::

      This is a one-time setting. If you see that *Ransomware Protection* is enabled, you can review the options but no action is required.

#. Click :fa:`fa-download` **Download (.csv)**, and then open the .csv file. It lists which file extensions File Analytics will block by default.

   .. figure:: images/csv.png

#. Within your *USER##*\-WinTools VM, navigate to the *F:\\\Sample Data\\\Documents* folder.

#. Create a new *.txt* file by right-clicking in an empty space, choosing **New** :fa:`caret-right` **Text Document**, and then hitting **Enter**. The file will be created with the name *New Text Document.txt*.

   .. figure:: images/textdoc.png

#. Rename the file to *bootcamp.txt*.

#. Click the **View** menu, and then check the box for **File name extensions**.

   .. figure:: images/fileext.png

#. Change the file extension to **.jpg**, and then click **Yes**.

#. Change the file extension to **.Valley**, and then click **Yes**.

   .. figure:: images/block.png

   This operation fails, as **.Valley** is one of the extensions that are blocked by Ransomware Protection, listed in the *.csv* file.

#. Click **Cancel** on the *File Access Denied* dialogue box.

#. Return to the *File Analytics* dashboard. Within the *Vulnerabilities* section, observe that this now displays the malicious attempt of creating a **.Valley** file.

   .. figure:: images/attempt.png

Custom Reports
==============

   Let’s explore how to build a report in File Analytics.

#. Click on the :fa:`bars` **> Reports >** :fa:`plus` **Create a new report**.

#. Select **Pre-canned Report Templates**.

#. Select **Events** from the *Based on* drop-down.

#. Under *Define Filters*, select **Permission Denied {File Blocking} Events** from the *Pre-canned report template* drop-down.

#. Click on **Run Preview**.

   .. figure:: images/preview.png

   .. note::

      Feel free to customize and explore the reports in other ways, in this example we are targeting the actions that resulted in preventing a user (or script) from altering the file in a malicious way.