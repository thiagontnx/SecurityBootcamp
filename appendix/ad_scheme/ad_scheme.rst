.. _ad_scheme:

################################
Active Directory User and Groups
################################

Each cluster has a dedicated domain controller VM - AUTOAD - responsible for providing Active Directory services for the *ntnxlab.local* domain. The domain is pre-populated with the following users and groups:


.. list-table::
   :widths: 15 10 20
   :header-rows: 1

   * - Group
     - Username(s)
     - Password
   * - Administrators
     - Administrator
     - nutanix/4u
   * - SSP Admins
     - adminuser01 - adminuser25
     - nutanix/4u
   * - SSP Developers
     - devuser01 - devuser25
     - nutanix/4u
   * - SSP Consumers
     - consumer01 - consumer-25
     - nutanix/4u
   * - SSP Operators
     - operator01 - operator-25
     - nutanix/4u
   * - SSP Custom
     - custom01 - custom25
     - nutanix/4u
   * - Bootcamp Users
     - user01 - user25
     - nutanix/4u