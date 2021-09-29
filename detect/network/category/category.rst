.. _detect_category:

##############
Categorization
##############

You observe that VMs are already being created to support one of the most popular gaming apps, King Drog FaceRace. This workload is supported centrally by the Nutanix cluster, and delivered via the gaming machines on the game floor by the following VMs:

.. raw:: html

-  **User**\ *##*-FaceRace-Web
-  **User**\ *##*-FaceRace-DB

.. figure:: images/9.png

Customers swipe their payment cards for access to game credits, and log in to track high scores. These machines collect cardholder data (CHD) such as the primary account number (PAN) and other personally identifiable information (PII). These VMs need to be isolated from the rest of the network in order to meet PCI DSS guidelines for segmentation of the cardholder data environment (CDE). The payment and user information must be protected from unauthorized access.

Prism Central uses categories as metadata to tag VMs to determine how policies will be applied. We need to add categories to identify all of our FaceRace application VMs.

#. Within **Prism Central**, select :fa:`bars` **> Administration > Categories**.

#. Select the checkbox for **AppType**, and then click **Actions > Update**.

   .. figure:: images/10.png

#. Click the :fa:`fa-plus-circle` icon to add an additional category value.

#. Specify **##-FaceRace** as the value name, and then click **Save**.

   .. figure:: images/apptype01.png

   Next, we need to define the different tiers of the FaceRace application.

   - **##**-Prod-FaceRace-Web       (*Production* Web tier)
   - **##**-Prod-FaceRace-DB        (*Production* Database tier)
   - **##**-Dev-FaceRace-Web        (*Development* Web tier)
   - **##**-Dev-FaceRace-DB         (*Development* Database tier)

#. Within **Prism Central**, select :fa:`bars` **> Administration > Categories**.

#. Select the checkbox for **AppTier**, and then click **Actions > Update**.

#. Click the :fa:`fa-plus-circle` icon to add additional category values:

   - **##-Web**
   - **##-Database**

.. figure:: images/12.png  [TODO: Pete: Screenshot incorrect.]

#. Click **Save**.

Assigning Categories to VMs
===========================

In this exercise, you’ll assign your custom categories to the VMs supporting King Drog FaceRace. This will help align access to the proper resources, and security and protection policies within the environment.

#. Within **Prism Central**, select :fa:`bars` **> Compute & Storage > VMs**.

#. Select your **##-FaceRace** VMs, and then click **Actions > Manage Categories**.

   .. figure:: images/categ001.png

   .. note::

      By selecting more than one VM, we’re simultaneouly defining categories values that will be common to them: the AppType category value that we defined earlier.

 #. In the search bar, enter **AppType:##**, click :fa:`fa-plus-circle`, and then click **Save**.

   .. figure:: images/categ02.png

   We now need to assign the appropriate tier category value to each of the VMs.

#. Deselect both **##-FaceRace-DB** VMs, and then click **Actions > Manage Categories**.

#. In the search bar, type **AppTier:##-Web**, click the :fa:`fa-plus-circle`, and then click **Save**.

   .. figure:: images/categweb.png [TODO: Pete: Screenshot incorrect.]

#. De-select the **##-FaceRace-Web** VMs, select the **##-FaceRace-DB** VMs, and then click **Actions > Manage Categories**.

#. In the search bar, type **AppTier:##-Database**, click the :fa:`fa-plus-circle`, and then click **Save**.

   .. figure:: images/categdb.png [TODO: Pete: Screenshot incorrect.]

Next, we'll create a security policy.