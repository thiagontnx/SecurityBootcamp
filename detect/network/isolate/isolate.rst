.. _detect_isolate:

####################
Isolate Environments
####################

Our FaceRace gaming machines are now properly secured from network activity outside the cluster. We want to ensure that we prevent access from other VMs from within the cluster. To achieve this, we can provide isolation policies to all the VMs in our environment.

The environments we will create enable isolation between the cardholder data environment (CDE) and the non-CDE (i.e. everything else). Similar to the previous section, we will add two more environmental categories: *CDE* and *Non-CDE*.

#. Within **Prism Central**, select :fa:`bars` **> Administration > Categories**.

#. Select **Environment > Actions > Update**.

#. Under **Values**, click :fa:`plus-circle`, create **##-CDE** and **##-Non-CDE** entries, and then click **Save**.

   .. figure:: images/envcat.png

   Next we will assign the *CDE* category value to the **##-Prod-FaceRace** VMs, and the *Non-CDE* category value to "everything else".

#. Select :fa:`bars` **> Compute & Storage > VMs**.

#. Select both the *USER##*\-Prod-FaceRace-Web and *USER##*\-Prod-FaceRace-DB VMs, and then click **Actions > Manage Categories**.

#. Specify **Environment:##-CDE** (ex. `Environment:01-CDE`) as the value name, and then click **Save**.

   .. figure:: images/cdecat01.png

#. Deselect both the *USER##*\-Prod-FaceRace-Web VMs, select both the *##-Dev-FaceRace-Web* and *##-Dev-FaceRace-DB* VMs, and click **Actions > Manage Categories**.

#. Specify **Environment:##-Non-CDE** (ex. `Environment:01-Non-CDE`) as the value name, and then click **Save**.

   .. figure:: images/cdecat02.png

   Now that category values have been created and appropriately assigned to the VMs, we can create an isolation policy.

#. Select :fa:`bars` **> Network & Security > Security Policies**.

#. Click **Create Security Policy > Isolate Environments (Isolation Policy) > Create**.

#. In the fields enter the following information:

   - **Name** - User##-PCIPolicy
   - **Purpose** - Isolate CDE from Non-CDE
   - **Isolate this category** - Environment:##-CDE
   - **From this category** - Environment:##-Non-CDE

#. Click **Save and Monitor**.

   .. figure:: images/pci.png

   This type of policy is a simple and effective way to achieve the desired isolation between sensitive environments that might contain personal customer data, or for the creation of network security best practices (i.e. creating a DMZ, or honeypots).

Testing the Isolation Policy
============================

As we did during our security policy testing, we will enforce the new isolation policy, and confirm it is working as expected.

#. Return to the consoles of *USER##*\-Prod-FaceRace-DB, and restart the continuous ping command by hitting the up arrow, followed by enter.

#. Click on your **USER##-PCIPolicy**.

#. Hover your mouse over the dotted line to the right of *Environment ##-CDE*. You'll notice that Flow is observing the traffic between the VMs in the policy.

   .. figure:: images/traffic.png

#. To activate the isolation policy, click **Enforce** in the upper  right-hand corner of your screen.

#. Type **ENFORCE**, and then click **Confirm**.

   .. figure:: images/enforce.png

#. Return to your **##-Prod-FaceRace-DB** console. Observe that the pings now fail, as we are blocking the Production (CDE) environment from Development (Non-CDE).

#. You may cancel the ping command, log out of both console sessions, and then close the console windows.

Congratulations for going above and beyond and isolate your production application environment.