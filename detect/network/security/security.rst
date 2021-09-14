.. _detect_security:

#####################
Securing Applications
#####################

Creating Security Policy
========================

Now that we’ve defined some categories, and assigned them to the respective VMs, we can begin to use those categories to form security policies that will be used to control traffic among these VMs. This capability is part of Flow micro-segmentation.

Flow is an application-centric network security product, which is tightly integrated into Nutanix AHV and Prism Central. Flow provides rich network traffic visualization, automation, and security for VMs running on AHV.

Microsegmentation is a component of Flow that uses simple policy-based management to secure VM networking. Using Prism Central categories, you can create a powerful distributed firewall. Combining this with Calm [TODO: Pete: Do they know what Calm is?] allows automated deployment of applications that are secured as they are created.

#. Within **Prism Central**, select :fa:`bars` **> Network & Security > Security Policies**.

#. Click **Create Security Policy > Secure Applications (App Policy) > Create**.

#. Fill out the following fields, and then click **Next**.

   - **Name** - *USER##*\-FaceRace
   - **Purpose** - Restrict unnecessary access to the FaceRace gaming machines
   - **Secure This App** - Apptype:##-FaceRace

   .. figure:: images/appsec01.png

   .. note::
      If prompted, click *OK, Got it!* on the tutorial diagram of the *Create App Security Policy* wizard.

#. To allow for a more granular configuration of the security policy, click **Set rules on App Tiers, instead**, rather than applying the same rules to all components of the application.

   .. figure:: images/apptierrules.png [TODO: Pete: Screenshot incorrect.]

#. Select **##-Web** from the drop-down.

#. Select **##-DataBase** from the drop-down.

   .. figure:: images/apptiers.png [TODO: Pete: Screenshot incorrect.]

   Next, you will define the *Inbounds* rules, which control which sources you will allow to communicate with the FaceRace VMs. You can allow all inbound traffic, or define whitelisted sources. By default, the security policy is set to deny all incoming traffic.

   In this scenario, we will allow inbound TCP traffic to the FaceRace web tier on TCP port 80 from all clients.

#. Under **Inbounds**, click :fa:`fa-plus-circle` **Add Source**.

#. Fill out the following fields to allow all inbound IP addresses, and then click **Add**.

   - **Add source by:** - Subnet/IP
   - **Enter a subnet.** - 0.0.0.0/0

   .. note::

      Sources can also be specified by category, allowing for greater flexibility as this data can follow a VM regardless of changes to its network location.

#. To create an inbound rule, ensure the *Subnet/IP* of 0.0.0.0/0 is still highlighted, and then select :fa:`fa-plus-circle` to the left of **AppTier ##-Web**.

#. Choose **Select a Service**, fill out the following fields, and then click **Save**:

   - **Protocol/Service** - TCP
   - **Ports/Service Details** - 80

   .. figure:: images/inbound.png [TODO: Pete: Screenshot incorrect.]

   .. note::

      Multiple protocols and ports can be added to a single rule.

#. Under **Inbounds**, click :fa:`fa-plus-circle` **Add Source**.

#. Fill out the following fields, and then click **Add**.

   - **Add source by:** - Subnet/IP
   - **Enter a subnet.** - <PRISM-CENTRAL-IP-ADDRESS>/32 (ex. 10.42.52.39/32)

   .. note::

      The /32 denotes a single IP address, as opposed to a subnet range.

#. Choose **Select a Service**, fill out the following fields, and then click **Save**:

   - **Protocol/Service** - TCP
   - **Ports/Service Details** - 22

#. Repeat previous step for **AppTier ##-Database** to allow communication with the database VM.

   .. figure:: images/tierconfig.png [TODO: Pete: Screenshot incorrect.]

   By default, the security policy allows the application to send all outbound traffic to any destination. The only outbound communication required for your application is to communicate with your DNS server.

#. Under **Outbound**, select **Allowed List Only** from the drop-down menu, and then click :fa:`fa-plus-circle` **Add Destination**.

#. Fill out the following fields, and then click **Add**:

   - **Add source by:** - Subnet/IP
   - **Enter a subnet.** - <AUTOAD-IP-ADDRESS>/32 (ex. 10.42.52.41/32)

   .. figure:: images/domainip.png [TODO: Pete: Screenshot is super blurry.]

#. Select :fa:`fa-plus-circle` to the right of **AppTier ##-Web**.

#. Choose **Select a Service**, fill out the following fields, and then click **Save**:

   - **Protocol/Service** - UDP
   - **Ports/Service Details** - 53

#. Repeat this for **AppTier ##-Database**.

   .. figure:: images/tierconfig02.png [TODO: Pete: Screenshot incorrect.]

Each tier of the application communicates with other tiers, and the policy must allow this traffic. Some tiers such as the Web tier do not require communication within the same tier.

#. To define intra-app communication, click **Set Rules within App**.

   .. figure:: images/withinapp.png [TODO: Pete: Screenshot incorrect.]

#. Click **AppTier ##-Web > Edit**, and under *Can VMs in this tier talk to each other?* select **No** to prevent communication between VMs in this tier.

   There are only two VMs (Prod and Dev) within the tier currently, but scale-out operations will apply this policy to all VMs in this category preventing their ability to communicate with one another - regardless of how many VMs are deployed.

#. While **AppTier:Web** is still selected, click :fa:`fa-plus-circle` to the right of **AppTier ##-Database** to create a tier-to-tier rule.

#. Choose **Select a Service**, fill out the following fields, and then click **Save**:

   - **Protocol/Service** - TCP
   - **Ports/Service Details** - 3306

   .. figure:: images/tiertotier.png [TODO: Pete: Screenshot incorrect.]

#. Click **Next** to review the security policy.

#. Click **Save and Monitor** to save the policy.

   .. figure:: images/save.png

Testing Security Policy
=======================

Now that we have created our first security policy, we need to test it.
Note that we configured our policy in *Monitor* mode, which means that we are not yet enforcing any inbound and outbound traffic rules.

#. Within **Prism Central**, select :fa:`bars` **> Compute & Storage > VM**.

#. Note the IP address for *USER##*\-Dev-FaceRace-Web.

#. Go to your *USER##*\-Prod-FaceRace-Web*, right-click, and then select **Launch Console**.

#. Login using the following credentials:

   - **Username** - centos
   - **Password** - nutanix/4u

#. Start a continuous ping to your *USER##*\-Dev-FaceRace-Web VM IP by entering the command ``ping <USER##-DEV-FACERACE-WEB-IP-ADDRESS>``. Let this run for a few moments to confirm communication, and then cancel it by hitting CTRL+C.

   .. figure:: images/ping01.png

#. Within **Prism Central**, select :fa:`bars` **> Compute & Storage > VM**.

#. Note the IP address for *USER##*\-Dev-FaceRace-DB.

#. Go to your *USER##*\-Prod-FaceRace-DB*, right-click, and then select **Launch Console**.

#. Login using the following credentials:

   - **Username** - centos
   - **Password** - nutanix/4u

#. Start a continuous ping to your *USER##*\-Dev-FaceRace-DB VM IP by entering the command ``ping <USER##-DEV-FACERACE-DB-IP-ADDRESS>``. Let this run for a few moments to confirm communication, and then cancel it by hitting CTRL+C.

   .. figure:: images/ping02.png

#. To enforce the security policy we created, select :fa:`bars` **> Network & Security > Security Policies**.

#. Click on your *User##-FaceRace* policy. Note that Flow is observing the traffic between the VMs in the policy.

   .. figure:: images/monitor.png [TODO: Pete: Screenshot incorrect.]

#. Within your *AppType ##-FaceRace*, hover the mouse cursor over the dotted line between two circles inside *AppTier ##-Web* and *AppTier ##-Database* to observe the communication within the application tiers.

   .. figure:: images/webtier.png [TODO: Pete: Highlight CANNOT.]

   .. figure:: images/dbtier.png [TODO: Pete: Highlight CAN.]

   .. note::

      If you click **Discovered** immediately below the *AppTier ##-Database** tier, you'll see the traffic from the ping commands you initiated.

   .. figure:: images/blocked.png

#. To enforce this security policy, click **Enforce** in the upper right-hand corner.

   .. figure:: images/enforce01.png

#. Type **ENFORCE**, and then click **Confirm**.

   .. figure:: images/enforce02.png

#. Return to the consoles of *USER##*\-Prod-FaceRace-Web and *USER##*\-Prod-FaceRace-DB.

#. Restart the continuous ping commands in both console windows by hitting the up arrow, followed by enter. You should notice that, while *USER##*\-Prod-FaceRace-Web *cannot* ping *USER##*\-Dev-FaceRace-Web, *USER##*\-Prod-FaceRace-DB *can* ping *USER##*\-Dev-FaceRace-DB.

   .. figure:: images/ping03.png

#. Cancel the ping command in both consoles by hitting CTRL+C, but leave both console windows open.

   Another way to test if the application is working properly is to open a browser and test its functionality.

#. Open a new browser tab and enter <USER##-PROD-FACERACE-WEB-IP-ADDRESS>.

   .. figure:: images/store01.png

#. Select **Stores > Add New Store**.

   .. figure:: images/store02.png

#. Fill out the information, and then click **Submit**.

#. If the store was created, this confirms that your application is working as expected, and that the web tier can communicate with the database tier.

   .. figure:: images/store03.png

Congratulations! Your security policy is working to restrict the required traffic to the VMs supporting FaceRace app.
