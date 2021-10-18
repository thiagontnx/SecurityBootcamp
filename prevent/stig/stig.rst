.. _prevent_stig:

################################################
Security Technical Implementation Guides (STIGs)
################################################

Security is in the DNA of the Nutanix platform. As a result, a significant proportion of our business is from sectors of industry that care deeply about security, including federal, local, and state governments, financial services, healthcare, retail, and beyond. Security is automatically part of every configuration and deployment, enabled by default, and continuously monitored for compliance against the security baselines and Security Technical Implementation Guides.  Nutanix doesn’t just have a single STIG, we apply multiple STIGs automatically, and continuously verify against them.

What is a STIG?

The description of a STIG is publicly available on the Defense Information Systems Agency, Information Assurance Support Environment web site:

“The Security Technical Implementation Guides (STIGs) are the configuration standards for DOD IA and IA-enabled devices/systems. Since 1998, Defense Information Systems Agency (DISA) has played a critical role enhancing the security posture of DoD’s security systems by providing the Security Technical Implementation Guides (STIGs). The STIGs contain technical guidance to lock down information systems and software that might otherwise be vulnerable to a malicious computer attack.”


STIG Reports on Nutanix Nodes
=============================

You can run a STIG report, which will check on all the individual STIG controls, and verify which are compliant with your system, and which are not.

The steps to run the STIG report are as follows:

#. SSH into any CVM via Terminal, PuTTy, or similar using the following credentials:

      - **User Name** - nutanix
      - **Password**  - nutanix/4u

#. Change to the root directory of the CVM:

   ``cd /``

#. List the files available to the root user within the `/root` directory:

   ``sudo -u root ls -l /root``

   Executable files contain *x* in the permission string. You should see a similar output:
   
   .. code-block:: bash

      nutanix@NTNX-14SX35100046-A-CVM:10.21.71.29:~# sudo -u root ls -l /root
      total 248
      -rw-------. 1 root root   3314 Sep 11  2017 anaconda-ks.cfg
      drwxr-x---. 2 root root   4096 Dec 13 23:04 filesystems
      -rw-r-----. 1 root root   1132 May  3  2018 homeaudit.pp
      -rw-r-----. 1 root root   1231 May  3  2018 my-runcon.pp
      -rw-r-----. 1 root root    464 May  3  2018 my-runcon.te
      -rw-------. 1 root root   3222 Sep 11  2017 original-ks.cfg
      -rwxr-x---. 1 root root  10034 May  3  2018 report_open_jre8_stig.sh
      -rwx------. 1 root root 132760 Aug 30 23:50 report_stig.sh
      -rwxr-x---. 1 root root  72376 May  3  2018 report_web_stig.sh
      drwxr-x---. 2 root root   4096 Dec 13 23:17 sretools
      -rw-r-----. 1 root root    840 May  3  2018 sshdlocal.pp
   
   There are three files that end in `_stig.sh` with its name corresponding to the output format it will display.

#. In this example, we’ll run the generic text output:

   ``sudo -u root ./root/report_stig.sh``

   The output will be written to the root user log folder.

#. List the files in the folder, and note the name of the report.

   ``sudo -u root ls -l /home/log | grep STIG``

#. Copy the report to the nutanix home directory, substituting the actual file name for the asterisks.

   ``sudo -u root cp /home/log STIG-report-**-**-****-**-**-** /home/nutanix``

#. List the files in the /home/nutanix folder.

   ``ls -l ~``

#. Change the owner of the report file to be the Nutanix user, substituting the actual file name for the asterisks.

   ``sudo -u root chown nutanix:nutanix /home/nutanix/STIG-report-**-**-****-**-**-**``

#. Log into your your *USER##*\-WinTools VM using the following credentials:

      - **User Name** - administrator
      - **Password**  - nutanix/4u
      
#. Open **WinSCP** from within the *Tools* folder on the desktop.

#.  to copy the report results file to your workstation from the CVM. 

using the following credentials:

      - **User Name** - administrator
      - **Password**  - nutanix/4u

Be sure to login to the CVM using the nutanix username and password provided by the instructor to browse to its home directory to find the file we created above.

   .. figure:: images/winscp.png

Analyzing the STIG Report
=========================

You now have the STIG report, and can use it to evaluate the current compliance state of the system, or for validation and accreditation requirements for security compliance.

This will report the results of all elements that make up the Nutanix STIG, and the report will show the compliance result for each of the checks contained within the STIG.

**Report Format**

.. code-block:: bash

   The first sentence says the check name
   The second sentence is an explanation of the check
   The third sentence is the legend for the result of the check
   The fourth sentence is the result of the check
   The fifth sentence is the completion status of the check

**Example of a Finding**

.. code-block::

   CAT I RHEL-07-021710 SRG-OS-000095-GPOS-00049 CCI-000381 CM-7 a, CM-7 b
   The telnet-server package must not be installed.
   The result of the check should be yes.  If no, then it's a finding
   no
   Completed.
 
**Example of a Non-Finding**

.. code-block::

   CAT II RHEL-07-021030 SRG-OS-000480-GPOS-00227 CCI-000366 CM-5 (1)
   All world-writable directories must be group-owned by root, sys, bin, or an application group.
   The result of the check should be yes.  If no, then it's a finding
   yes
   Completed.

.. Rick’s SCMA (Saltstack) Self-Healing Lab
.. ========================================

.. To make a system truly scalable, it must address security misconfigurations automatically, whether you’re managing four nodes or four hundred.

.. With Nutanix, Security Configuration Management is automated with SCMA. SCMA is a saltstack daemon that runs as a scheduled cron job. If the daemon spots an inconsistency, it both corrects and logs the event. The CVM self-heals deviations to the secure state. This state is established according to industry best practices, along with information we've gathered over the years from our customers.

.. **It’s not necessary to complete the following section but read through it and see the effectiveness of self-healing technology.** [TODO: Pete: If this is just a demonstration, it shouldn't be called a lab. And if we want folks to run through this, it needs more explanation and screen shots. I stopped here and didn't review the section until it gets updated.]

.. **Testing Automation:**

.. From the report you generated in `STIG Reports on Nutanix Nodes`_, download it or access it from the console in order to get the state of the following check:
.. All world-writable directories must be group-owned by root, sys, bin, or an application group. The result of the check should be yes.

.. Let us test if self-healing from security violations works with SCMA: 
.. #. Connect to any Controller VM (CVM) as the nutanix user via SSH (Using Terminal, PuTTy, or similar program)
.. #. Change to the root directory of the CVM

.. ``cd /``

.. You can search for this specific report from the CVM console where the report was run and using the following command, substituting the actual file name for the asterisks:

.. ``sudo -u root grep -A 4 -B 1 "All world-writable directories " /home/log/STIG-report-**-**-****-**-**-**``

.. It should say **yes** by default.

.. Let’s compromise the system so that this check says **“no”** and then manually fix the issue.

.. #. Verify the current ownership, type:

.. ``sudo -u root ls -l / | grep tmp``

.. You should see a similar output:

..    ::

..       drwxrwxrwt.  14 root root  1024 Dec 21 02:59 tmp

.. #. Change the group ownership by running:


.. ``sudo -u root chown root:nutanix /tmp``

.. #. Verify the ownership change:

.. ``sudo -u root ls -l / | grep  tmp``

.. You should see a similar output:

..    ::

..       drwxrwxrwt.  14 root **nutanix**  1024 Dec 21 03:16 tmp

.. After we have achieved this, let’s re-run the report to see if this change has been detected.

.. #. Run the following commands:

.. ``sudo -u root ./root/report_stig.sh``

.. ``sudo -u root grep -A 4 -B 1 "All world-writable directories " /home/log/STIG-report-**-**-****-**-**-**``

.. You should see a “no” this time, indicating a finding. 
.. #. So now you can manually run the salt call to fix this vulnerability:

.. ``sudo -u root salt-call state.sls security/CVM/fdpermsownerCVM``

.. #. List the / directory again and note that the ‘compromise’ has been reverted back.

.. ``sudo -u root ls -l / | grep tmp``

..    ::

..       drwxrwxrwt.  14 root root  1024 Dec 21 03:42 tmp
 
..    .. note::
..       In this example we manually ran the salt call, which is set to run against all checks daily by default. You can adjust the cadence of this check to run hourly if desired. 


..    - Takeaways
..       - Nutanix uses STIGs to verify compliance.
..       - Nutanix uses daily checks to self-remediate issues