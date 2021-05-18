.. title:: Nutanix Security Bootcamp

.. toctree::
   :maxdepth: 2
   :caption: Prevent
   :name: _prevent
   :hidden:

   prevent/start/start
   prevent/stig/stig
   prevent/auth/auth

.. toctree::
   :maxdepth: 2
   :caption: Detect
   :name: _detect
   :hidden:

   detect/start/start
   detect/category/category

.. toctree::
   :maxdepth: 2
   :caption: Recover
   :name: _recover
   :hidden:

Background
++++++++++

You are the Security Engineer at **Blips and Chitz Inc.**, a hugely popular entertainment arcade that has to support gaming machines, a payment application, some desktops for corporate staff, and a customer information database.

All of the collected customer information and payment card details have to be kept confidential due to strict regulatory guidelines such like; PCI DSS, CCPA, and GDPR to name a few, but from a strategic perspective properly protecting this data helps maintain the corporate competitive advantages.

Blips and Chitz Inc, have just purchased a Nutanix cluster together with Frame, Files, Objects and Flow licenses all of which are intended to support production workloads.

.. figure:: images/1.png

As the sole Security Engineer for Blips and Chitz your responsibilities are varied and numerous, you don’t have a lot of time to learn new security tools and Operating System(s), let alone dedicate weeks worth time to consuming training in order to deploy these tools in production. Simply put, you need security to work, intrinsically, and you need it fast!

In terms of your background, you have some familiarity with the Linux command line but would likely need help with certain commands, and you understand basic networking security principles, but you’re unfamiliar with new technologies like micro-segmentation and have zero experience with analytics platforms like Files Analytics and data archiving technologies like object based WORM enabled data protection.

Due to resource constraints you forward all logs to a Syslog server then use a SIEM (Security Incident Event Management) which is used by an outsourced SOC (Security Operations Center) for altering. For audit purposes, you have to be able to show evidence of log collection for the platform and for the virtual infrastructure powering Blips and Chitz.

Your boss, Roy, was sold on this new platform called “Nutanix” and has just requested that the Nutanix cluster be ready to support production workloads by the end of the week, this tight timeline is driven in part because a new Qualified Security Assessor (QSA) will be visiting next week to begin to conduct the annual Blips and Chitz security audit for PCI DSS. You immediately voiced your concerns that this timeframe isn’t feasible, but Roy knows you’ll try your best to get something to him.

Roy has also informed you that a new variant of ransomware known as Krombopulous is gaining notoriety and has recently been effective at disrupting the local hospital. This new malware variant is highly adaptable and pervasive which is what prompted Blips and Chitz into purchasing the portfolio products Flow, Files, and Objects since they further protect the sensitive data on this cluster. Roy hands you a Tech Brief (https://www.nutanix.com/viewer?type=pdf&path=/content/dam/nutanix/resources/solution-briefs/tb-ransomware.pdf) which outlines their benefits.

Finally, Roy wants you to demonstrate to the board by the end of the week how these tools can be used to limit the exposure of the Krombopulos Ransomware virus within the Nutanix cluster thus giving the board members peace of mind when considering repeat Nutanix purchases.
