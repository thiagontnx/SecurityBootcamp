.. _recover_protect:

###########################
Protecting Your Environment
###########################

Creating a Protection Policy
============================

#. Within *Prism Central*, select :fa:`bars` **> Data Protection and Recovery > Protection Policies**.

#. Click **Create Protection Policy**. Fill out the following fields, and then click **Save**.

   - **Policy name** - *USER##*\-Local (ex. USER01-Local)
   - **Primary Location > Location** - Local AZ
   - **Cluster** - <YOUR-CLUSTER> (ex. PHX-POC074)

   .. figure:: images/localaz.png

#. Click **Add Local Schedule**. Fill out the following fields, and then click **Save Schedule**:

   - **Take Snapshot Every** - Hour(s) 1
   - **Retention Type** - Linear (default)
   - **Retention on Local AZ : <CLUSTER>** - 5 Recover Points

#. Within the **Recovery Location** click **Cancel**, and then click **Next**.

#. Within the *Search for a category* field, select **AppType:##-FaceRace** (ex: Apptype:01-FaceRace), and then click **Add > Create**.

You now have a continuous stream of snapshots protecting these VMs, making it possible to roll back your FaceRace application to a previous point in time.

Recovery Of A Compromised VM
============================

You've identified that your *User##-Dev-FaceRace-Web* VM has been compromised by ransomware. You'll need to act quickly to prevent this VM from sending or receiving traffic by quarantining it.

#. Within Prism Central, select :fa:`bars` **> Compute and Storage > VMs**.

#. Select **User##-Dev-FaceRace-Web**, and then click **Actions > Quarantine VMs**.

   .. figure:: images/quar01.png

#. Select **Strict**, and then click **Quarantine**.

   .. figure:: images/quar02.png

   .. note::

      Quarantining a VM using *Strict* mode will prevent the VM from sending or receiving traffic. While not used here, there is also *Forensics* mode, which restricts the VM to only being able to communicate with specified VMs. This enables investigation of the VM, while still preventing all other traffic.

      The red icon next to the VM name means that it has been quarantined.

         .. figure:: images/quar03.png

      If you were now to ping the *User##-Dev-FaceRace-Web* VM from any other VM, you would observe that the ping would fail.

Bring an infected VM back to a stable state
===========================================

We will now restore your compromised VM to the previous known-good state, and confirm it is operating as expected.

#. Within *Prism Central*, select :fa:`bars` **> Compute and Storage > VMs**.

#. Click on **User##-Dev-FaceRace-Web > Recovery Points**.

#. Select the latest snapshot, click **Restore** from the *Actions* drop-down, and then click **Restore**.

#. Return to :fa:`bars` **> Compute and Storage > VMs**, and open the console for the restored copy of the VM (ex: User01-Dev-FaceRace-Web_clone1).

#. Confirm you are able to communicate with other VMs by performing a ping test to them.

Within seconds you were able to not only avert a potential disaster by immediately quarantining an infected VM, but restore the VM to normal operation.