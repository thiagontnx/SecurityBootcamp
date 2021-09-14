.. _detect_isolate:

####################
Isolate Environments
####################

Our FaceRace gaming machines are now properly secured from network activity outside the cluster. We want to ensure that we prevent access from other VMs from within the cluster. To achieve this, we can provide isolation policies to all the VMs in our environment.

The environments we will create environments to enable isolation between the cardholder data environment (CDE) and the non-CDE (i.e. everything else). Similar to the previous section, we will add two more environmental categories: *CDE* and *Non-CDE*.

#. Within **Prism Central**, select :fa:`bars` **> Administration > Categories**.

#. Select **Environment > Actions > Update**.

#. Under **Values**, click :fa:`fa-plus-circle` and create **##-CDE** and **##-Non-CDE** entries, and then click **Save**.

   .. figure:: images/envcat.png [TODO: Pete: Screenshot incorrect.]

   Next we will assign the *CDE* category value to the **##-Prod-FaceRace** VMs, and the *Non-CDE* category value to "everything else".

#. Within **Prism Central**, select :fa:`bars` **> Compute & Storage > VMs**.

#. Select both the *USER##*\-Prod-FaceRace-Web and *USER##*\-Prod-FaceRace-DB VMs, and then click **Actions > Manage Categories**.

#. In the search box type **Environment:##-CDE**, and click **Save**.

   .. figure:: images/cdecat01.png

#. Within **Prism Central**, select :fa:`bars` **> Compute & Storage > VMs**.

#. Select both the *##-Dev-FaceRace-Web* and *##-Dev-FaceRace-DB* VMs, and click **Actions > Manage Categories**.

#. In the search box type **Environment:##-Non-CDE**, and then click **Save**.

   .. figure:: images/cdecat02.png [TODO: Pete: Screenshot incorrect.]

   Now that category values have been created and appropriately assigned to the VMs, we can create an isolation policy. 

#. Within **Prism Central**, select :fa:`bars` **> Network & Security > Security Policies**.

#. Click **Create Security Policy > Isolate Environments (Isolation Policy) > Create**.

#. In the fields enter the following information: 

   - **Name** - User##-PCIPolicy
   - **Purpose** - Isolate the CDE from the Non-CDE
   - **Isolate this category** - Environment:CDE
   - **From this category** - Environment:Non-CDE

#. Click **Save and Monitor**.

   .. figure:: images/pci.png [TODO: Pete: Screenshot incorrect.]

   When enforced, this type of policy is a simple and effective way to achieve the desired isolation between sensitive environments that might contain personal customer data, or for the creation of network security best practices (i.e. creating a DMZ, or honeypots).

Testing the Isolation Policy
============================

Just like we did during our security policy testing, we will enforce the new isolation policy, and then confirm it is working.

#. Within Prism Central, select :fa:`bars` **> Network & Security > Security Policies**, and then click on your **##-PCIPolicy**.

   You'll notice that Flow is observing the traffic between the VMs in the policy.

#. To activate the isolation policy, click **Enforce**, in the upper-right corner of your screen.

   .. figure:: images/enforce01.png 

#. Type **ENFORCE**, and then click **Confirm**.

   .. figure:: images/enforce002.png

#. Return to your **##-Prod-FaceRace-DB** console.

#. Restart the continuous ping commands within both console windows by hitting the up arrow, followed by enter.

#. Observe that the pings will now fail, as we are blocking the Production (CDE) environment from Development (Non-CDE).

#. You may cancel the ping commands in both console windows, log out of both sessions, and close the console windows.

Congratulations for going above and beyond and isolate your production application environment.