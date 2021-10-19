.. _detect_faransom:

####################################
File Analytics Ransomware Protection
####################################

Starting with AOS 5.19 and File Analytics 3.0, you can enable ransomware protection.

File Analytics scans files for ransomware in real-time, and notifies you via email in the event of a ransomware attack. By using the Nutanix Files file blocking mechanism, File Analytics prevents files with signatures of potential ransomware from carrying out malicious operations. Ransomware protection automatically scans for ransomware based on a curated list of signatures that frequently appear in ransomware files. Optionally, you can add additional signatures to the list.

File Analytics also monitors file shares for self-service restore (SSR) policies, and identifies shares that do not have SSR enabled in the ransomware dashboard. You can enable SSR through the ransomware dashboard by selecting shares identified by File Analytics.

Enabling Ransomware Protection
==============================

#. To enable Ransomware Protection, click :fa:`bars` **> Ransomware**

   .. figure:: images/enable.png

#. Click **Enable Ransomware Protection**, and then click **Enable**.

   .. figure:: images/enable2.png

   .. note::

      This is also a one-time setting. If you see that *Ransomware Protection* is enabled, you can review the options but no action is required.

   #. Click **Download (.csv)** to view which file extensions File Analytics will block by default.

   .. figure:: images/csv.png

#. Within the *Z:\\Sample Data\\Documents* folder, create a *.txt* file.

#. Rename to **Bootcamp.txt**.

#. Rename it again, changing only the file extension to **.jpg**.

#. Once again, change the file extension once more to **.Valley**.

   .. figure:: images/block.png

   This operation will fail as **.Valley** is one of the extensions that are blocked by Ransomware protection.

#. Click **Cancel** on the error prompt you received when you attempted to change the file extension.

#. Return to File Analytics, and then click :fa:`bars` **> Ransomware**.

#. Within the *Vulnerabilities* section, observe that this now displays the malicious attempt of creating a **.Valley** file. [TODO: Pete: Screenshot incorrect.]

   .. figure:: images/attempt01.png

Custom Reports
==============

   Let’s explore how to build a report in File Analytics.

#. Click on the :fa:`bars` **> Reports >** :fa:`plus` **Create a new report**.

#. Select **Pre-canned Report Templates**.

#. Select **Events** from the *Based on* drop-down.

#. Under *Define Filters*, select **Permission Denied {File Blocking} Events** from the *Pre-canned report template* drop-down.

#. Click on **Run Preview**.

   .. figure:: images/preview.png [TODO: Pete: Screenshot incorrect.]

   .. note::

      Feel free to customize and explore the reports in other ways, in this example we are targeting the actions that resulted in preventing a user (or script) from altering the file in a malicious way.