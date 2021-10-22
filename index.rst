.. title:: Nutanix Security Bootcamp

.. toctree::
   :maxdepth: 2
   :caption: Prevent
   :name: _prevent
   :hidden:

   prevent/start/start
   prevent/auth/auth
   prevent/stig/stig

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
   :caption: Optional Labs (Instructor Led)
   :name: _optional
   :hidden:

   optional/infection/im
	optional/syslog/syslog

.. toctree::
   :maxdepth: 2
   :caption: Appendix
   :name: _appendix
   :hidden:

   appendix/glossary
   appendix/access/access
   appendix/network/network
   appendix/ad_scheme/ad_scheme
   appendix/getting_help/getting_help

##########
Background
##########

Blips and Chitz Inc. is a hugely popular entertainment arcade that supports gaming machines, a payment application, desktops for corporate staff, and a customer information database.

From a strategic perspective, properly protecting this data helps maintain the company's competitive advantages. All of the collected customer information and payment card details must be kept confidential due to strict regulatory guidelines including, but not limited to:

  - PCI DSS - The Payment Card Industry Data Security Standard is a set of security standards designed to ensure that ALL companies that accept, process, store or transmit credit card information maintain a secure environment.
  - CCPA - The California Consumer Privacy Act is a state statute intended to enhance privacy rights and consumer protection for residents of California, United States.
  - GDPR - The General Data Protection Regulation is a regulation in EU law on data protection and privacy in the European Union (EU) and the European Economic Area (EEA).

Blips and Chitz Inc. have just purchased a Nutanix cluster to support production workloads.

   .. figure:: images/1.png

You are the sole Security Engineer, and your responsibilities are both varied and numerous. You don’t have a lot of time to learn new security tools and operating systems, let alone spend weeks or longer  on dedicated training in order to deploy these tools in production. Simply put, you need security to just work.

In terms of your background, you have some familiarity with the Linux command line, but would likely need help with certain commands. You understand basic networking security principles, but you’re unfamiliar with new technologies like micro-segmentation. Lastly, you have zero experience with analytics platforms, and data archiving technologies like object based write-one ready-many (WORM) enabled data protection.

You forward all logs to a syslog server, then use a SIEM (Security Incident Event Management) which is used by an outsourced SOC (Security Operations Center). For audit purposes, you have to be able to show evidence of log collection for the platform and for the virtual infrastructure powering Blips and Chitz Inc.

Your boss Roy has requested that the Nutanix cluster be ready to support production workloads by the end of the week. This tight timeline is driven in part because a new Qualified Security Assessor (QSA) will be visiting next week to begin to conduct the annual Blips and Chitz Inc. security audit for PCI DSS. While you immediately voiced your concerns that this time frame isn’t feasible, Roy knows you’ll try your best to implement this new platform ahead of the audit.

While you drank this morning's coffee, you read about a new variant of ransomware known as Krombopulous. It is gaining notoriety, and has recently been effective at disrupting the local hospital. This new malware variant is highly adaptable and pervasive, which is what prompted Blips and Chitz Inc. to purchase additional Nutanix products to further protect the company's sensitive data on this cluster. Rick Sanchez, the Systems Architect, sent you a `Tech Brief <https://www.nutanix.com/viewer?type=pdf&path=/content/dam/nutanix/resources/solution-briefs/tb-ransomware.pdf>`_ which outlines the benefits to utilizing these products.

If all this wasn't enough, Roy wants you to demonstrate to the board how these tools can be used to limit the exposure of ransomware within the Nutanix cluster, thus giving the board members peace of mind when considering expansion of this environment. The board meeting is at the end of the week.

###############
Getting Started
###############

Welcome to the Nutanix Security Bootcamp!

This bootcamp highlights the intrinsic security benefits of our core platform, and the data plane security enhancements available via microsegmentation, analytics, and any automation that can be leveraged to prevent, detect, and recover from malware attacks such as ransomware.

What's New (Last updated 10-22-21)
=================================

Labs are updated for the following software versions:

- AOS: 5.20.2 LTS
- PC : pc.2021.9
- Files: 3.8.1.3
- Files Analytics: 3.0

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

Optional Labs (Instructor Led)
==============================

- Simulating An Attack

Introductions
=============

- Name
- Familiarity with Nutanix

Initial Setup
=============

- Take note of the passwords being used.
- Log in to your virtual desktops.