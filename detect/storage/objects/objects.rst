.. _detect_objects:

###############
Nutanix Objects
###############

Configuring WORM
================

The storage administrators for Blips and Chitz, Inc. have created an object storage for *Mortynight Run*, the video surveillance system. It needs to retain archive data for regulatory purposes, and improved security. Your task will be to guarantee that the policies set for the repository adhere to the company's security guidelines.

Create Bucket
=============

A bucket is a repository within an object store that can have policies applied to it, such as versioning, and WORM (Write Once, Read Many). By default, a newly created bucket is a private resource to the creator. By default, the creator of the bucket has read/write permissions, and can grant permissions to other users.

#. Within Prism Central, select :fa:`bars` **> Services > Objects**.

#. Click on the existing Object Store name **mortynightrun** to manage it.

#. Select **user##-bucket**, and then click **Actions > Configure WORM** to view its settings.

   .. figure:: images/worm.png

You realize your colleagues didn’t enable *WORM* and *Expiration* settings, so you will now proceed with those modifications in order to protect the company’s data from attackers and for audit purposes.

#. Click **Enable Version**.

#. Click **Enable WORM**, and set the *Retention Period* to **3 years**.

#. Click **Enable WORM** to save the changes.

   .. figure:: images/enableworm.png

#. Click on **user##-bucket**, and then select **Lifecycle** from the left-hand menu.

   .. figure:: images/createrule.png

#. Click **Create Rule**, and fill out the following information:

   - **Name** - *User##*\-Expiration Rule
   - **Scope** - All Objects

#. Click **Next**.

#. Click **Expiration**, and within the *Expire* section, set **Current Version 3 years** after last creation date.

   .. figure:: images/exp.png

   .. note::

      After you save the WORM configuration, you will have a 24-hour grace period window where you can disable its settings. After that time, you can no longer change it, and the system will permanently follow this behavior. Not even Nutanix support can modify it.

#. Click **Next > Done**.

   .. note::

      WORM storage prevents the editing, overwriting, renaming, or deleting of data and is crucial in heavily regulated industries (finance, healthcare, public agencies, etc.) where sensitive data is collected and stored. Examples include emails, account information, voice mails, and more.

      Note that if WORM is enabled on the bucket, this will supersede any lifecycle expiration policy.

   .. note::

      Tiering allows for infrequently used objects to be moved to the configured endpoints according to the configured lifecycle rule for tiering. The supported endpoints are AWS S3, and a separate Objects instance.

User Management
===============

In this exercise, you will generate access and secret keys to access the Object store that will be used throughout the lab.

#. Within *Prism Central*, select :fa:`bars` **> Services > Objects**.

#. Click on **Access Keys** :fa:`plus` **Add People**.

   .. figure:: images/addpeople03.png

#. Select **Add people not in a directory service**, and enter your e-mail address.

   .. figure:: images/addpeople.png

#. Click **Next**, and then click **Generate Keys**.

#. Click **Download Keys** to download a .txt file containing the *Access Key* and *Secret Key*.

   .. figure:: images/addpeople04.png

#. Click **Close**.

#. Open the file with a text editor.

   .. figure:: images/keys.png

	.. note::

		Keep the text file open, to have the access and secret keys readily available for future labs.

   .. note::

      You can always revoke or renew access keys.
    
Granting Bucket Access
======================

Next, you will grant other users access to your bucket. You can configure read/write access on a per user basis.

#. Click on **Object Stores > mortynightrun**.

#. Select **user##-bucket**, and then click **Actions > Share**.

#. Enter your e-mail address within the *People* field. Check both **Read** and **Write** checkboxes within the *Permissions* field, and then click **Save**.

   .. figure:: images/access.png

Objects Browser
===============

In this exercise, you will use the *Objects Browser* to create and access buckets in the object store.

#. Within your *USER##*\-WinTools VM, download sample images using this link: `https://s3.amazonaws.com/get-ahv-images/sample-pictures.zip`, and extract it to your desktop.

#. Within your *USER##*\-WinTools VM, open *Prism Central* and select :fa:`bars` **> Services > Objects**.

#. Click on **Objects Public IPs**.

   .. figure:: images/ip.png

#. Enter the *Access Key* and *Secret Key* from your .txt file, and then click **Login**.

#. Click on *user##*\-bucket. From the *Upload Objects* drop-down, select **Select Files**.

#. Navigate to the *sample-pictures* directory on your desktop, and upload one picture to your bucket. You may optionally repeat this process to upload multiple pictures.

   .. figure:: images/explorer.png

Object Versioning
=================

Object versioning allows the upload of new versions of the same object, while retaining the original data. Versioning can be used to preserve, retrieve, and restore every version of every object stored within a bucket. This allows for easy recovery situations such as unintended user action, or application failures.

#. Within your *USER##*\-WinTools VM, open *Notepad*.

#. Enter ``version 1.0``, and then save the file on your desktop as **user##.txt**.

#. Within *Objects Browser*, upload the text file to **user##-bucket**, and then click **Close** once the upload has completed.

#. Open *user##.txt*, modify the file to now contain ``version 2.0``, and then save the file.

#. Upload *user##.txt* once again to your bucket.

#. Return to *Prism Central*. Within *Object Stores**, click on **mortynightrun**, and then **user##-bucket**.

#. Look at the *Total number of objects* entry.

.. figure:: images/props.png

You will see that there is an object created for every version of your test file. By keeping multiple versions of the same file, Nutanix Objects makes it possible to restore old versions at any point in time. Additionally, S3 compatible third-party tools can access previous versions of any given file.