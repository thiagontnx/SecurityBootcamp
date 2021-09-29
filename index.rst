.. title:: Nutanix Security Bootcamp

.. toctree::
   :maxdepth: 2
   :caption: Prevent
   :name: _prevent
   :hidden:

   prevent/start/start
   prevent/auth/auth
   prevent/stig/stig
   prevent/syslog/syslog

.. toctree::
   :maxdepth: 2
   :caption: Detect - Networking
   :name: _detectnet
   :hidden:

   detect/network/start
   detect/network/category/category
   detect/network/security/security
   detect/network/isolate/isolate

.. toctree::
   :maxdepth: 2
   :caption: Detect - Data Services
   :name: _detectstg
   :hidden:

   detect/storage/start
   detect/storage/fa/fa
   detect/storage/faransom/faransom
   detect/storage/objects/objects


.. toctree::
   :maxdepth: 2
   :caption: Protect and Recover
   :name: _protect_recover
   :hidden:

   recover/start
   recover/protect/protect


.. toctree::
   :maxdepth: 2
   :caption: Optional Labs
   :name: _optional
   :hidden:

   optional/infection/im
   optional/leap/leap
  ..  optional/mine/mine

##########
Background
##########

Blips and Chitz Inc. is a hugely popular entertainment arcade that supports gaming machines, a payment application, desktops for corporate staff, and a customer information database.

From a strategic perspective, properly protecting this data helps maintain the company's competitive advantages. All of the collected customer information and payment card details must be kept confidential due to strict regulatory guidelines including:

  - PCI DSS - The Payment Card Industry Data Security Standard (PCI DSS) is a set of security standards designed to ensure that ALL companies that accept, process, store or transmit credit card information maintain a secure environment.
  - CCPA - The California Consumer Privacy Act is a state statute intended to enhance privacy rights and consumer protection for residents of California, United States.
  - GDPR - The General Data Protection Regulation is a regulation in EU law on data protection and privacy in the European Union (EU) and the European Economic Area (EEA).

Blips and Chitz Inc. have just purchased a Nutanix cluster, along with Files, File Analytics, Objects, and Flow to support production workloads.

   .. figure:: images/1.png

You are the sole Security Engineer, and your responsibilities are both varied and numerous. You don’t have a lot of time to learn new security tools and operating systems, let alone dedicate weeks worth of time to consuming training in order to deploy these tools in production. Simply put, you need security to just work.

In terms of your background, you have some familiarity with the Linux command line, but would likely need help with certain commands. You understand basic networking security principles, but you’re unfamiliar with new technologies like micro-segmentation. Lastly, you have zero experience with analytics platforms, and data archiving technologies like object based write-one ready-many (WORM) enabled data protection.

You forward all logs to a syslog server, then use a SIEM (Security Incident Event Management) which is used by an outsourced SOC (Security Operations Center) for altering. For audit purposes, you have to be able to show evidence of log collection for the platform and for the virtual infrastructure powering Blips and Chitz Inc.

Your boss Roy has requested that the Nutanix cluster be ready to support production workloads by the end of the week. This tight timeline is driven in part because a new Qualified Security Assessor (QSA) will be visiting next week to begin to conduct the annual Blips and Chitz Inc. security audit for PCI DSS. While you immediately voiced your concerns that this time frame isn’t feasible, but Roy knows you’ll try your best to implement this new platform ahead of the audit.

While you drank this morning's coffee, you read about a new variant of ransomware known as Krombopulous. It is gaining notoriety, and has recently been effective at disrupting the local hospital. This new malware variant is highly adaptable and pervasive, which is what prompted Blips and Chitz Inc. to additionally purchase Flow, Files, and Objects since those products further protect the company's sensitive data on this cluster. Rick Sanchez, the Systems Architect, sent you a `Tech Brief <https://www.nutanix.com/viewer?type=pdf&path=/content/dam/nutanix/resources/solution-briefs/tb-ransomware.pdf>`_ which outlines the benefits to utilizing these products.

Finally, Roy wants you to demonstrate to the board how these tools can be used to limit the exposure of ransomware within the Nutanix cluster, thus giving the board members peace of mind when considering expansion of the Nutanix environment. The board meeting is at the end of the week.

###############
Getting Started
###############

Welcome to the Nutanix Security Bootcamp!

This bootcamp highlights the intrinsic security benefits of our core platform, and the data plane security enhancements available via microsegmentation, analytics, and any automation that can be leveraged (where possible) to prevent, detect, and recover from malware attacks such as ransomware.

What's New (Last updated 9-28-21)
=================================

Labs are updated for the following software versions:

- AOS: 5.20.1.1 LTS
- PC : pc.2021.7
- Era: 2.2.0.1

Agenda
======

- Introductions
- Lab Setup

Security Labs
=============

- Prevent: Platform security: STIGs, SCMA, Auth, syslog
- Detect - Networking: Data security: Flow, uSeg, NetSec
- Detect - Data Services: Monitoring - Files, File Analytics, Objects, Testing
- Recover - Snapshots, Quarantine

Optional Labs
=============

- Flow Security Central
- Leap

Introductions
=============

- Name
- Familiarity with Nutanix

Initial Setup
=============

- Take note of the passwords being used.
- Log into your virtual desktops (connection info below).

Environment Details
===================

Nutanix Bootcamps are intended to be run within the Nutanix Hosted POC environment. Your cluster will be provisioned with all necessary images, networks, and VMs required to complete the exercises.

Credentials
-----------

.. note::

  The *<CLUSTER-PASSWORD>* is unique to each cluster and will be provided by the leader of the Bootcamp.

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Credential
     - Username
     - Password
   * - Prism Element
     - admin
     - *<CLUSTER-PASSWORD>*
   * - Prism Central
     - admin
     - *<CLUSTER-PASSWORD>*
   * - Controller VM
     - nutanix
     - *<CLUSTER-PASSWORD>*
   * - Prism Central VM
     - nutanix
     - *<CLUSTER-PASSWORD>*

Each cluster has a dedicated domain controller VM (*AutoAD*), responsible for providing AD services for the *NTNXLAB.LOCAL* domain. The domain is populated with the following Users and Groups:

.. list-table::
   :widths: 25 35 40
   :header-rows: 1

   * - Group
     - Username(s)
     - Password
   * - Administrators
     - Administrator
     - nutanix/4u
   * - SSP Admins
     - adminuser01-adminuser25
     - nutanix/4u
   * - SSP Developers
     - devuser01-devuser25
     - nutanix/4u
   * - SSP Consumers
     - consumer01-consumer25
     - nutanix/4u
   * - SSP Operators
     - operator01-operator25
     - nutanix/4u
   * - SSP Custom
     - custom01-custom25
     - nutanix/4u
   * - Bootcamp Users
     - user01-user25
     - nutanix/4u

Access Instructions
-------------------

The Nutanix Hosted POC environment can be accessed a number of different ways:

Lab Access User Credentials
^^^^^^^^^^^^^^^^^^^^^^^^^^^

PHX Based Clusters:
**Username:** PHX-POCxxx-User01 (up to PHX-POCxxx-User20), **Password:** *<PROVIDED-BY-INSTRUCTOR>*

RTP Based Clusters:
**Username:** RTP-POCxxx-User01 (up to RTP-POCxxx-User20), **Password:** *<PROVIDED-BY-INSTRUCTOR>*

Frame VDI
^^^^^^^^^

Login to: https://frame.nutanix.com/x/labs

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** credentials

Parallels VDI
^^^^^^^^^^^^^

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** credentials

Employee Pulse Secure VPN
^^^^^^^^^^^^^^^^^^^^^^^^^

Download the client:

PHX Based Clusters Login to: https://xld-uswest1.nutanix.com

RTP Based Clusters Login to: https://xld-useast1.nutanix.com

**Nutanix Employees** - Use your **NUTANIXDC** credentials
**Non-Employees** - Use **Lab Access User** credentials

Install the client.

In Pulse Secure Client, **Add** a connection:

For PHX:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - PHX
- **Server URL** - xlv-uswest1.nutanix.com

For RTP:

- **Type** - Policy Secure (UAC) or Connection Server
- **Name** - X-Labs - RTP
- **Server URL** - xlv-useast1.nutanix.com