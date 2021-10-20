.. _detect_category:

##############
Categorization
##############

You observe that VMs are already being created to support one of the most popular gaming apps, King Drog FaceRace. This workload is supported centrally by the Nutanix cluster, and delivered via the gaming machines on the game floor via the following VMs:

   -  **User**\ *##*-FaceRace-Web
   -  **User**\ *##*-FaceRace-DB

   .. figure:: images/9.png

Customers swipe their payment cards for access to game credits, and log in to track high scores. These machines collect cardholder data (CHD) such as the primary account number (PAN) and other personally identifiable information (PII). These VMs need to be isolated from the rest of the network in order to meet PCI DSS guidelines for segmentation of the cardholder data environment (CDE). The payment and user information must be protected from unauthorized access.

Prism Central uses categories as metadata to tag VMs to determine how policies will be applied. We need to add categories to identify all of our *King Drog FaceRace* application VMs.

#. Within **Prism Central**, select :fa:`bars` **> Administration > Categories**.

#. Select the checkbox for **AppType**, and then click **Actions > Update**.

   .. figure:: images/10.png

#. Click the :fa:`plus-circle` icon to add an additional category value.

#. Specify **##-FaceRace** (ex. 01-FaceRace) as the value name, and then click **Save**.

   .. figure:: images/apptype01.png

   Next, we need to define the different tiers of the FaceRace application.

   - **##**-Prod-FaceRace-Web       (*Production* Web tier)
   - **##**-Prod-FaceRace-DB        (*Production* Database tier)
   - **##**-Dev-FaceRace-Web        (*Development* Web tier)
   - **##**-Dev-FaceRace-DB         (*Development* Database tier)

#. Deselect the checkbox for **AppType**, select the checkbox for **AppTier**, and then click **Actions > Update**.

#. Click the :fa:`plus-circle` icon for each additional category values:

   - **##-Web**
   - **##-Database**

   .. figure:: images/12.png

#. Click **Save**.

Assigning Categories to VMs
===========================

In this exercise, you’ll assign your custom categories to the VMs supporting *King Drog FaceRace*. This will help align access to the proper resources, security, and protection policies within the environment.

#. Select :fa:`bars` **> Compute & Storage > VMs**.

#. Select all four of your **User##-FaceRace** VMs, and then click **Actions > Manage Categories**.

   .. figure:: images/categ001.png

   By selecting more than one VM, we’re simultaneously defining categories values that will be common to them: the AppType category value that we defined earlier.

 #. In the search bar, enter **AppType:##-FaceRace**, click :fa:`plus-circle`, and then click **Save**.

   .. figure:: images/categ02.png

   We now need to assign the appropriate tier category value to each of the VMs.

#. Deselect both **User##-FaceRace-DB** VMs, and then click **Actions > Manage Categories**.

#. In the search bar, type **AppTier:##-Web**, click the :fa:`plus-circle`, and then click **Save**.

   .. figure:: images/categweb.png

#. De-select the **User##-FaceRace-Web** VMs, select the **##-FaceRace-DB** VMs, and then click **Actions > Manage Categories**.

#. In the search bar, type **AppTier:##-Database**, click the :fa:`plus-circle`, and then click **Save**.

   .. figure:: images/categdb.png

Next, we'll create a security policy.