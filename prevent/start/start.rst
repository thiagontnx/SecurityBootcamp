.. _prevent_start:

################################
Secure Access & System Hardening
################################

You have just been informed that the deployment of the cluster is completed and the access details have been emailed to you. Your first job is to ensure that the platform is hardened according to `NIST SP800-53 <https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final>`_ guidelines and that all system default passwords are changed from the vendor-supplied defaults.

When trying to get acquainted with Nutanix, you received a `Tech Note: TN-2026 <https://portal.nutanix.com/page/documents/solutions/details?targetId=TN-2026-Information-Security:TN-2026-Information-Security>`_ from your Nutanix Account team, the Account Executive, Morty Smith, and his Systems Architect, Rick Sanchez.

You think back to all the time and effort you poured into hardening and maintaining alignment to a secure baseline for the old infrastructure. If all that was truly not required with Nutanix, it could mean shaving off a considerable amount of time to make this system production-ready.

STIGs (Security Technical Implementation Guide) are a hardening guide, used to perform the process of system and security hardening, each Nutanix node in a cluster is covered by these STIGs, to harden both the hypervisor (AHV) and the Controller VM (CVM) which provides all of the Nutanix services. To satisfy the compliance requirements, you can now provide evidence of this system state via the STIG report of the nodes.

Going further, these hardening steps are continually kept current with an automated self-healing daemon [TODO: Pete: Do people know what a daemon is, or should we replace that term?]. This piqued your interest and Rick provided you a guide below [TODO: Pete: Where?] which you can use to test the self-healing aspect of the platform. Afterward, you’re looking forward to being able to relax, safe in the knowledge that no more weekends will be sacrificed on the altar of compliance!

.. figure:: images/2.jpg
