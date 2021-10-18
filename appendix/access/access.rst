.. _access:

#########################
Accessing the Environment
#########################

Nutanix employees are able to access the Hosted POC environment with the `corporate GlobalProtect VPN <https://gp.nutanix.com>`_, or via either method covered below.

Partners and customers can gain access to the Hosted POC environment using the following:

Lab Access User Credentials
===========================

PHX Based Clusters:

  - Username: PHX-POC###-User## (User01 through User20. Ex. PHX-POC123-User15)
  - Password: *<PROVIDED BY INSTRUCTOR>*

RTP Based Clusters:

  - Username: RTP-POC-User (User01 through User20. Ex. RTP-POC123-User15)
  - Password: *<PROVIDED BY INSTRUCTOR>*

Frame VDI
=========

Users can also access the HPOC through a Frame on AHV session.

Log in to: https://console.nutanix.com/x/labs

  .. list-table::
    :widths: 20 20 20
    :header-rows: 1

    * - Access From
      - Type
      - Credentials
    * - Nutanix 
      - Internal
      - NUTANIXDC
    * - Prospect/Customer/Partner
      - External 
      - Lab Access User Credentials

Parallels VDI
=============

Users can also access the HPOC through a non-persistent Windows 10 virtual desktop.

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

  .. list-table::
    :widths: 20 20 20
    :header-rows: 1

    * - Access From
      - Type
      - Credentials
    * - Nutanix 
      - Internal
      - NUTANIXDC
    * - Prospect, Customer, Partner
      - External 
      - Lab Access User Credentials

The WIN10 desktop can be accessed through a locally installed Parallels client or via HTML5.

  .. figure:: images/1.png

The local client is recommended, but the HTML5 client is a great option for users unable to install applications on their device.

  .. figure:: images/2.png

Pulse Secure VPN
================

.. note::
  
  Use of the VPN solution requires attendees to install the Pulse agent on their device. Attendees may not have local administrator access to their device to allow for installation.</font></strong>

Refer to your automation@nutanix.com *Reservation Confirmation* e-mail for the *Lab Access User Credentials* associated with the reservation.

Each reservation receives 20 accounts in the format of <Cluster Name>-User<01-20>, using the same password associated with the reservation.

#. Log in to https://xlv-uswest1.nutanix.com (for PHX clusters) or https://xlv-useast1.nutanix.com (for RTP clusters) using one of the provided accounts.

#. Under *Client Application Sessions*, click **Start** to the right of *Pulse Secure* to download the client.

#. Install and open **Pulse Secure**.

#. Add connection:

  - **Type** - Policy Secure (UAC) or Connection Server
  - **Name** - HPOC VPN
  - **Server URL** - https://xlv-uswest1.nutanix.com or https://xlv-useast1.nutanix.com

    .. figure:: images/0.png

#. Connect using the provided credentials.