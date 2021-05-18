.. _detect_isolate:

------------------------------------------------
Isolate Environments
------------------------------------------------

Isolate Environments
++++++++++++++++++++++++

Our FaceRace gaming machine is now properly secured from network activity outside the cluster, but to further ensure that we can’t access these machines from another VM from within the cluster we can provide Isolation Policies to all the VMs in our environment to create separation between virtual entities. 

This separation could be to ensure isolation between Development and Production VMs, or in our case, isolation between the Cardholder Data Environment (CDE) and the non-CDE (i.e. everything else!). 

Using the same method we used earlier we’re going to create some environments to delineate between entities that are part of the scope for a PCI assessment, namely this gaming application: 

In Prism Central > Virtual Infrastructure > Categories
Check box > Environment  |  Actions > Update
Here we will add two more environmental Categories: CDE & Non-CDE


Click Save

Now we need to assign the CDE category value to the FaceRace VMs and the Non-CDE category value to EVERYTHING else. 

In Prism Central, navigate to Virtual Infrastructure > VMs
Select both the FaceRace VMs that support our gaming application and click Actions > Manage Categories. 
In the search box type Environment:CDE
Click Save






Note: Normally we would create the inverse category value to assign to all other (Non-CDE) VMs within the environment. But for the purposes of this exercise, we will go straight to policy creation. 
Now that category values have been created and appropriately assigned to the VM’s we can create an Environment/ Isolation policy. 
Navigate In Prism Central to > Policies > Security
Create Security Policy
Click the radio button next to Isolate Environments (Isolation Policy) > Create
In the fields enter the following information: 
Name = PCIPolicy
Purpose = Isolate the CDE from the Non-CDE
Isolate this category = Environment:CDE
From this category = Environment:Non-CDE
Click Save and Monitor
Note: We don’t need to apply the isolation only with a subset of the data center, nor do we need to enable Policy Hitlogs for this policy at this time. 

When Enforced, this type of policy is a simple and effective way to achieve the desired isolation between sensitive environments that might contain Personal customer data, or for the creation of network security best practices i.e. creating a DMZ, or Honeypots. 
