.. _network:

#####################
Network Configuration
#####################

The following tables detail the network IP Address assignments for multi-node and single node environments.

Multi-Node Reservations
=======================

.. list-table::
   :widths: 20 30 30
   :header-rows: 1

   * - IP Range
     - Service
     - Comments
   * - 10.x.x.7
     - Hyper-V Failover IP
     - 
   * - 10.x.x.8 - 10.x.x.14
     - Files
     - 
   * - 10.x.x.15
     - File Analytics
     - 
   * - 10.x.x.16 - 10.x.x.21
     - Objects
     - 
   * - 10.x.x.22
     - 
     - 
   * - 10.x.x.23
     - Beam
     - 
   * - 10.x.x.25 - 10.x.x.28
     - Hosts
     - 
   * - 10.x.x.29 - 10.x.x.32
     - CVMs
     - 
   * - 10.x.x.33 - 10.x.x.36
     - IPMI
     -
   * - 10.x.x.37
     - Cluster IP
     -  
   * - 10.x.x.38
     - Data Services IP
     - 
   * - 10.x.x.39
     - Prism Central
     - 
   * - 10.x.x.40
     - VCSA
     - vCenter
   * - 10.x.x.41
     - AutoAD
     - Windows Domain Controller
   * - 10.x.x.42
     - PrismOpsLabUtilityServer
     - Used for Prism Ops Labs
   * - 10.x.x.44
     - Era
     - 
   * - 10.x.x.45
     - Citrix DDC
     - 
   * - 10.x.x.50 - 10.x.x.125
     - Primary Network IPAM
     - vLAN 0
   * - 10.x.x.126 - 10.x.x.254
     - Secondary Network IPAM
     - Secondary vLAN

Single Node Reservations
========================

.. list-table::
   :widths: 11 11 11 11 20 20
   :header-rows: 1

   * - Partition 1
     - Partition 2
     - Partition 3
     - Partition 4
     - Service
     - Comments
   * - 10.38.x.1
     - 10.38.x.65
     - 10.38.x.129
     - 10.38.x.193
     - Gateway
     -  
   * - 10.38.x.5
     - 10.38.x.69
     - 10.38.x.133
     - 10.38.x.197
     - AHV Host
     - 
   * - 10.38.x.6
     - 10.38.x.70
     - 10.38.x.134
     - 10.38.x.198
     - CVM
     - 
   * - 10.38.x.7
     - 10.38.x.71
     - 10.38.x.135
     - 10.38.x.199
     - Cluster IP
     -
   * - 10.38.x.8
     - 10.38.x.72
     - 10.38.x.136
     - 10.38.x.200
     - Data Services
     -
   * - 10.38.x.9
     - 10.38.x.73
     - 10.38.x.137
     - 10.38.x.201
     - Prism Central
     - 
   * - 10.38.x.11
     - 10.38.x.75
     - 10.38.x.139
     - 10.38.x.203
     - AUTOAD
     - Windows Domain Controller
   * - 10.38.x.12
     - 10.38.x.76
     - 10.38.x.140
     - 10.38.x.204
     - Utility Server
     - Prism Ops Lab
   * - 10.38.x.14
     - 10.38.x.78
     - 10.38.x.142
     - 10.38.x.206
     - Era
     - 
   * - 10.38.x.15
     - 10.38.x.79
     - 10.38.x.143
     - 10.38.x.207
     - Citrix DDC
     - 
   * - 10.38.x.32 - 10.38.x.37
     - 10.38.x.96 - 10.38.x.101
     - 10.38.x.160 - 10.38.x.165
     - 10.38.x.224 - 10.38.x.229
     - Objects
     -
   * - 10.38.x.38 - 10.38.x.58
     - 10.38.x.102 - 10.38.x.122
     - 10.38.x.166 - 10.38.x.186
     - 10.38.x.230 - 10.38.x.250
     - Primary Network IPAM
     - 6 IPs free for static assignment