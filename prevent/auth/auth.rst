.. _prevent_auth:

##############
Authentication
##############

Changing Vendor Default Passwords
=================================

Changing vendor default passwords is an essential first step in the adoption of new platforms, and is often tested and measured in many compliance assessments. Failure to address this early critical step in system configuration can result in effectively leaving an open door to an attacker.

In a Nutanix deployment, there are several default passwords that we'll demonstrate how to change.

   .. note:

      Even though the Nutanix cluster you are using is dedicated to the Bootcamp, all of our automation is based on the current configured passwords. Changing those passwords will break our internal automation system. Instead, we are providing you with a video describing the process. We do have the process documented, if you need to perform the steps showed below, let your instructor know. [TODO: Pete: Recommend we add these steps within a note]

The first of which is Prism Element. Upon first log in, you are required to create a new, secure password for the local *Admin* account.

AHV is protected with a local account, with credentials hashed and salted for further protection from potential brute force or dictionary attacks.

   .. raw:: html

    <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262880324001" frameborder="0" allowfullscreen></iframe>

The CVM has two local accounts: *Nutanix* and *Admin*.

   .. raw:: html

    <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262879852001" frameborder="0" allowfullscreen></iframe>

The Intelligent Platform Management Interface (IPMI) is a way for remote administrators to ascertain the hardware state of the infrastructure Nutanix is running upon. In compliance with California statute SB-327, BMC [TODO: Pete: explain the statute? What is BMC?] 7.08 and later use a unique password.

   - Username: *admin*
   - Password = <NODE-SERIAL-NUMBER>

    .. raw:: html

     <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262879977001" frameborder="0" allowfullscreen></iframe>

Cluster Lockdown
================

To further protect access to your cluster, introduce a layer of non-repudiation [TODO: Pete: Will people know what this means?] to your access method. With Cluster Lockdown, you can replace SSH password-based authentication with a public SSH key. Only the holder of the corresponding private key will be able to login.

#. Open `https://<PRISM-CENTRAL-IP>/` in a new browser tab, and log in.

#. Within Prism Central, select :fa:`bars` **> Prism Central Settings > Security > Cluster Lockdown**.

   This is where you would provide the name, along with your public key. As this setting is a one-time only configuration, this has already been provided for this bootcamp.

   .. figure:: images/clusterlockdown.png

.. _prevent_auth_dirservices:

Directory Services and Identity Providers
=========================================

A local account is great for when you’re in a jam and need access when other authentication measures have failed, hence why this Local Admin user account should be protected via SSH keys rather than a password. For regular day-to-day access by team members and end-users, a more secure way to provide member access to Prism is with the use of Directory Services. No passwords or hashes are stored on the cluster for directory services users and authentication is passed through to the directory.

   .. note::

      We have already provided an Active Directory server (AutoAD) as part of the Bootcamp, but feel free to understand what information you need to add you own AD.

#. Within Prism Central, select :fa:`bars` **> Prism Central Settings > Users and Roles > Authentication**, and then click **+ New Directory**.

   .. figure:: images/dirlist.png

   .. note::

      As you may have noticed in Prism Central, if you visit the Authentication Configuration menu, you have the option to connect to an Identity Provider (IdP), this further enhances access protocols by leveraging technologies like Single Sign On (SSO) and Multi-Factor Authentication (MFA).

      Currently Prism Central only supports Active Directory Federation Services (ADFS) as part of the SAML protocol. But you can register your appropriate account metadata in the same Authentication Configuration menu used above.

#. Once you are finished reviewing the *Authentication Configuration* section, click **Back**.

   To complete Active Directory configuration, you must map AD users to Prism Central roles.

#. Under **Users and Roles**, select **Role Mapping**, and then click **+ New Mapping**.

#. Specify **adminuser##** within *Values*. Select **Cluster Admin** from the *Role* drop-down, and then click **Save**.

   .. figure:: images/rolemapping.png

   .. note::

      Each one of the participants are assign with a user number provided by your instructor. Replace ## with your corresponding number.

#. Log out of Prism Central.

   .. figure:: images/signout.png

#. Log into Prism Central as the AD user mapped in the previous step (ex. adminuser05@ntnxlab.local).

   .. figure:: images/login.png

.. raw:: html

   .. note::

      Throughout the rest of the bootcamp, you'll log in to Prism Central using this username.
