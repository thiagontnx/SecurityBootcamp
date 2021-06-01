.. _detect_security:

----------------------
Securing Applications
----------------------

Security Policy Creation
+++++++++++++++++++++++++

Now that we’ve defined some Categories and assigned them to the respective VM’s we can begin to use those categories to form Security Policies that will be used to isolate traffic to and from these VM’s. This capability is part of Flow micro-segmentation. 

Flow is an application-centric network security product tightly integrated into Nutanix AHV and Prism Central. Flow provides rich network traffic visualization, automation, and security for VMs running on AHV.

Microsegmentation is a component of Flow that uses simple policy-based management to secure VM networking. Using Prism Central categories (logical groups), you can create a powerful distributed firewall. Combining this with Calm allows automated deployment of applications that are secured as they are created.

#. In **Prism Central**, select :fa:`bars` **> Policies > Security**
#. Click **Create Security Policy > Secure Applications (App Policy) > Create**.
#. Fill out the following fields:

- Name - User##-FaceRace
- Purpose - Restrict unnecessary access to the FaceRace gaming machines
- Secure this app - AppType: User##-FaceRace

   .. figure:: images/policy01.png

#. Click **Next**.


   .. note::
      If prompted, click OK, Got it! on the tutorial diagram of the Create App Security Policy wizard.


#. To allow for a more granular configuration of the security policy, click **Set rules on App Tiers** instead, rather than applying the same rules to all components of the application.

   .. figure:: images/apptierrules.png


#. Select **Web** from the drop-down.
#. Select **DataBase** from the drop-down.

   .. figure:: images/apptiers.png

Next, you will define the Inbound rules, which control which sources you will allow to communicate with the FaceRace application VMs. You can allow all inbound traffic, or define whitelisted sources. By default, the security policy is set to deny all incoming traffic.

In this scenario, we want to allow inbound TCP traffic to the FaceRace web tier on TCP port 80 from all clients.

#. Under **Inbound**, click **+ Add Source**.
#. Fill out the following fields to allow all inbound IP addresses:

- Add source by: - Select Subnet/IP
- Specify 0.0.0.0/0

#. Click **Add**.

   .. note::
      Sources can also be specified by Categories, allowing for greater flexibility as this data can follow a VM regardless of changes to its network location.

#. To create an inbound rule, select the **+ icon** that appears to the left of **AppTier:Web**.
#. Choose Select a Service.
#. Fill out the following fields:

- Protocol/Service - TCP
- Ports/Service Details - 80

   .. figure:: images/inbound.png

   .. note::
      Multiple protocols and ports can be added to a single rule.

#. Click **Save**.
#. Under **Inbound**, click **+ Add Source**.
#. Fill out the following fields:

- Add source by: - Select Subnet/IP
- Specify Your Prism Central IP/32

   .. note::
      The /32 denotes a single IP as opposed to a subnet range.

#. Click **Add**.
#. Select the **+ icon** that appears to the left of **AppTier:Web**, specify **TCP port 22** and click **Save**.
#. Repeat previous step for **AppTier:Database** to allow communication with the database VM.

   .. figure:: images/tierconfig.png

By default, the security policy allows the application to send all outbound traffic to any destination. The only outbound communication required for your application is to communicate with your DNS server.

#. Under **Outbound**, select **Allowed List Only** from the drop-down menu, and click **+ Add Destination**.
#. Fill out the following fields:

- Add source by: - Select Subnet/IP
- Specify Your Domain Controller IP/32

   .. figure:: images/domainip.png

#. Click Add.
#. Select the **+ icon** that appears to the right of **AppTier:Web**, specify **UDP port 53** and click **Save** to allow DNS traffic. 
#. Repeat this for **AppTier:Database**.

   .. figure:: images/tierconfig02.png

Each tier of the application communicates with other tiers and the policy must allow this traffic. Some tiers such as the Web tier do not require communication within the same tier.

#. To define intra-app communication, click **Set Rules within the App**.

   .. figure:: images/withinapp.png

#. Click **AppTier:Web > Edit** and select **No** to prevent communication between VMs in this tier. There is only a single web VM within the tier currently but scale-out operations will apply this policy to all VMs in this category preventing their ability to communicate with one another. **True Micro-segmentation!**
#. While **AppTier:Web** is still selected, click the **+ icon** to the right of **AppTier:DB** to create a tier-to-tier rule.
#. Fill out the following fields to allow communication on **TCP port 3306** between the web and database tiers:

- Protocol - TCP
- Ports - 3306

   .. figure:: images/tiertotier.png

#. Click **Save**.
#. Click **Next** to review the security policy.
#. Click **Save and Monitor** to save the policy.

   .. figure:: images/save.png


** ADD PING VERIFICATION HERE **