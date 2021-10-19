.. _prevent_auth:

##############
Authentication
##############

Changing Vendor Default Passwords
=================================

Changing vendor default passwords is an essential first step in the adoption of new platforms, and is often tested and measured in many compliance assessments. Failure to address this early critical step in system configuration can result in effectively leaving an open door to an attacker.

In a Nutanix deployment, there are several default passwords that we'll demonstrate how to change.

   .. note:

      Even though the Nutanix cluster you are using is dedicated to the Bootcamp, all of our automation is based on the current configured passwords. Changing those passwords will break our internal automation system. Instead, we are providing you with a video describing the process.

The first of which is Prism Element. Upon first log in, you are required to create a new, secure password for the local *Admin* account.

AHV is protected with a local account, with credentials `hashed <https://en.wikipedia.org/wiki/Cryptographic_hash_function>`_ and `salted <https://en.wikipedia.org/wiki/Salt_(cryptography)>`_ for further protection from potential `brute force <https://en.wikipedia.org/wiki/Brute-force_attack>`_ or `dictionary attacks <https://en.wikipedia.org/wiki/Dictionary_attack>`_.

   .. raw:: html

    <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262880324001" frameborder="0" allowfullscreen></iframe>

The CVM has two local accounts: *Nutanix* and *Admin*.

   .. raw:: html

    <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262879852001" frameborder="0" allowfullscreen></iframe>

The Intelligent Platform Management Interface (IPMI) is a way for remote administrators to ascertain the hardware state of the infrastructure Nutanix is running upon. In compliance with `California statute SB-327 <https://leginfo.legislature.ca.gov/faces/billTextClient.xhtml?bill_id=201720180SB327>`_, these are set using a unique password.

   - Username: *admin*
   - Password = <NODE-SERIAL-NUMBER>

    .. raw:: html

     <iframe width="560" height="315" src="https://players.brightcove.net/5850956868001/default_default/index.html?videoId=6262879977001" frameborder="0" allowfullscreen></iframe>

Cluster Lockdown
================

   ..note ::

      For the purposes of this Bootcamp, please do not make any changes to this section. These instructions are provided for illustration purposes only.

There are several options available within *Cluster Lockdown* section. You can enable or disable remote login via password, SSH key, or both. Disabling both remote login methods will enable *Cluster Lockdown*.

To further protect access to your cluster, you have the option of  introducing a layer of `non-repudiation <https://en.wikipedia.org/wiki/Non-repudiation>`_ to your access method. You can replace SSH password-based authentication with a public SSH key. Only the holder of the corresponding private key will be able to login.

#. Open ``https://<PRISM-CENTRAL-IP>/`` in a new browser tab, and log in.

   TODO: Look at above to see if it's what I want with that link.

#. Within Prism Central, select :fa:`bars` **> Prism Central Settings > Security > Cluster Lockdown**.

   This is where you would provide the name, along with your public key. As this setting is a one-time only configuration, this has already been provided for this bootcamp.

   You would uncheck the *Enable Remote Login with Password* box to disable remote login via password.

   .. figure:: images/clusterlockdown.png

.. _prevent_auth_dirservices:

Directory Services and Identity Providers
=========================================

The local *admin* user account should be protected via SSH keys, rather than a password. For regular day-to-day access by team members and end-users, a more secure way to provide member access to Prism is with the use of *Directory Services*. No passwords or hashes are stored on the cluster for directory services users, as authentication is passed through to the directory.

   .. note::

      While the Active Directory server (AutoAD) is already included, we've provided the below steps to illustrate what would be required to use an Active Directory (AD) environment.

#. Within Prism Central, select :fa:`bars` **> Prism Central Settings > Users and Roles > Authentication**, and then click :fa:`plus` **New Directory**.

   .. note::

      As you may have noticed in Prism Central, if you visit the *Authentication Configuration* menu, you have the option to connect to an Identity Provider (IdP), this further enhances access protocols by leveraging technologies like Single Sign On (SSO) and Multi-Factor Authentication (MFA).

      Currently Prism Central only supports Active Directory Federation Services (ADFS) as part of the SAML protocol. But you can register your appropriate account metadata in the same *Authentication Configuration* menu used above.

#. Once you are finished reviewing the *Authentication Configuration* section, click **Back**.

   To complete Active Directory configuration, you must map AD users to Prism Central roles.

#. Under *Users and Roles*, select **Role Mapping**, and then click :fa:`plus` **New Mapping**.

#. Specify **adminuser##** within the *Values* field, select **Cluster Admin** from the *ROLE* drop-down, and then click **Save**.

   .. figure:: images/rolemapping.png

#. Log out of Prism Central.

   .. figure:: images/signout.png

#. Log in to Prism Central as *adminuser##*. (ex. `adminuser01@ntnxlab.local`).

   .. figure:: images/login.png

   .. note::

      Throughout the rest of the bootcamp, you'll continue to use *adminuser##* for Prism Central.