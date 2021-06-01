.. _prevent_start:

------------------------------------------------
Secure Access & System Hardening
------------------------------------------------

You have just been informed that the deployment of the cluster is completed and the access details have been emailed to you. Your first job is to ensure that the platform is hardened according to NIST SP800-53 guidelines and that all system default passwords are changed from the vendor-supplied defaults. 

When trying to get acquainted with Nutanix you received a Tech Note: TN-2026 from your Nutanix Account team, the Account Executive, Morty Smith, and his Systems Architect, Rick Sanchez. 

The tech note outlines the security hardening of a Nutanix node. Rick (*burrrp), informed you that basically, all the early steps for system hardening are automated and built into the platform! 

This made you ecstatic since it could mean that all the work you’d previously done to harden and maintain alignment to a secure baseline in the old infrastructure was now gone!! If this is true, the Nutanix platform just saved a considerable amount of time from your current workflow! 

Before you kick back and enjoy that well-earned rest, you know that in order to satisfy the compliance requirements for evidence of this system state you are required to output the STIG (Security Technical Implementation Guide) of the nodes. STIGs are a hardening guide, used to perform the process of system & security hardening, and in this case, each Nutanix node has its own STIG to harden both the hypervisor AHV and the Controller VM which provides all of the Nutanix services. 

Going further, these hardening steps are kept current with an automated self-healing daemon. This really piqued your interest and Rick provided you a guide below which you can use to test the self-healing aspect of the platform.  Afterward, you’re looking forward to being able to relax, safe in the knowledge that no more weekends will be sacrificed on the altar of compliance!

.. figure:: images/2.jpg