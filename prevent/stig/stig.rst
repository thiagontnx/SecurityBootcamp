.. _prevent_stig:

################################################
Security Technical Implementation Guides (STIGs)
################################################

Security is in the DNA of the Nutanix platform. As a result, a significant portion of our business is from sectors of industry that care deeply about security, including federal, local, and state governments, financial services, healthcare, retail, and beyond. Security is automatically part of every configuration and deployment, enabled by default, and continuously monitored for compliance against the security baselines.  Nutanix doesn’t just have a single STIG, we apply multiple STIGs automatically, and continuously verify against them.

   ..note ::
      
      What is a STIG?

      The description of a STIG is publicly available on the Defense Information Systems Agency, Information Assurance Support Environment web site:

      The Security Technical Implementation Guides (STIGs) are the configuration standards for DOD IA and IA-enabled devices/systems. Since 1998, Defense Information Systems Agency (DISA) has played a critical role enhancing the security posture of DoD’s security systems by providing the Security Technical Implementation Guides (STIGs). The STIGs contain technical guidance to lock down information systems and software that might otherwise be vulnerable to a malicious computer attack.

.. _stig_reports:

STIG Reports on Nutanix Nodes
=============================

You can run a STIG report, which will check on all the individual STIG controls, and verify which are compliant with your system, and which are not.

#. Within **Prism Central**, select :fa:`bars` **> Compute * Storage > VMs**.

#. If there are any filters listed in the search bar in the top left-hand corner, click the :fa:`times` to clear them.

#. Observe the IP address of any CVM, which will be named as *NTNX-<DATACENTER>-<CLUSTER>-#-CVM* as shown below.

   .. figure:: images/cvmipaddress.png

#. SSH into any CVM via Terminal, PuTTy, or similar using the following credentials:

      - **User Name** - `nutanix`
      - **Password**  - `nutanix/4u`

#. Change to the root directory of the CVM:

   ``cd /``

#. List the files available to the root user within the `/root` directory:

   ``sudo -u root ls -l /root``

   Executable files contain *x* in the permission string, as shown in this sample output:
   
   .. figure:: images/sudoroot.png

   There are three files that end in `_stig.sh`, where its name corresponding to the output format it will display.

#. In this example, we’ll run the generic text output:

   ``sudo -u root ./root/report_stig.sh``

   The output will be written to the root user log folder.

#. List the files in the folder, and note the name of the report.

   ``sudo -u root ls -l /home/log | grep STIG``

#. Copy the report to the nutanix home directory, substituting the actual file name for the asterisks.

   ``sudo -u root cp /home/log/STIG-report-**-**-****-**-**-** /home/nutanix``

#. List the files in the /home/nutanix folder.

   ``ls -l ~``

#. Change the owner of the report file to be the Nutanix user, substituting the actual file name for the asterisks.

   ``sudo -u root chown nutanix:nutanix /home/nutanix/STIG-report-**-**-****-**-**-**``

#. Log in to your *USER##*\-WinTools VM using the following credentials:

      - **User Name** - `administrator`
      - **Password**  - `nutanix/4u`
      
#. Open **WinSCP** from within the *Tools* folder on the desktop.

#. Fill out the following fields, click **Save**, and then click **Login**.

      - **Host name** - <CVM-IP-ADDRESS>
      - **User name**  - `nutanix`
      - **Password**  - <CVM-PASSWORD>

   .. figure:: images/winscp1.png

#. Within *WinSCP*, select **Desktop** from the top left-hand corner drop-down.

#. Select the `STIG-report-**-**-****-**-**-**` file, click **Download**, and then click **OK**.

   .. figure:: images/winscp2.png

#. Close *WinSCP* and the *Tools* folder window.

Analyzing the STIG Report
=========================

You now have the STIG report, and can use it to evaluate the current compliance state of the system, or for validation and accreditation requirements for security compliance.

This will report the results of all elements that make up the Nutanix STIG, and the report will show the compliance result for each of the checks contained within the STIG.

#. Right-click on the `STIG-report-**-**-****-**-**-**` file on your *USER##*\-WinTools VM desktop, and choose **Open with Sublime Text**.

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

Security Configuration Management Automation (SCMA) Self-Healing Lab
===========================================================================

To make a system truly scalable, it must address security misconfigurations automatically, whether you’re managing four nodes or four hundred.

With Nutanix, Security Configuration Management is automated with SCMA. SCMA is a `saltstack <https://en.wikipedia.org/wiki/Salt_(software)>`_ `daemon <https://en.wikipedia.org/wiki/Daemon_(computing)>`_ that runs as a scheduled `cron <https://en.wikipedia.org/wiki/Cron>`_ job. If the daemon spots an inconsistency, it both corrects and logs the event. The CVM self-heals deviations to the secure state. This state is established according to industry best practices, along with information we've gathered over the years from our customers.

Testing Automation
------------------

From the report you generated in :ref:`STIG Reports on Nutanix Nodes`, download it or access it from the console in order to get the state of the check *All world-writable directories must be group-owned by root, sys, bin, or an application group*. The result of the check should be *yes*.

#. Return to your SSH session.

#. We will now test to confirm the system is self-healing from security violations via SCMA. The result of the check should be *yes*, as shown below.

   ``sudo -u root grep -A 4 -B 1 "All world-writable directories " /home/log/STIG-report-**-**-****-**-**-**``

   .. figure:: images/scma1.png

Now we'll compromise the system, so that the result of this check is *no*, and then manually fix the issue.

#. Verify the current ownership.

   ``sudo -u root ls -l / | grep tmp``

   .. figure:: images/scma2.png

#. Change the group ownership.

   ``sudo -u root chown root:nutanix /tmp``

#. Verify the ownership change:

``sudo -u root ls -l / | grep  tmp``

   .. figure:: images/scma3.png

#. Re-run the report to see if this change has been detected. 

   ``sudo -u root ./root/report_stig.sh``

   ``sudo -u root grep -A 4 -B 1 "All world-writable directories " /home/log/STIG-report-**-**-****-**-**-**``

   The result of the check is *no*, indicating a finding.

   .. figure:: images/scma4.png

#. Run the *salt-call* command to fix this vulnerability.

   ``sudo -u root salt-call state.sls security/CVM/fdpermsownerCVM``

#. List the directory again, and note that the "compromise" has been reverted.

   ``sudo -u root ls -l / | grep tmp``

   .. figure:: images/scma5.png
 
   In this example, we manually ran the *salt-call* command. It is set to automatically run all checks on a daily basis by default. You can adjust the cadence of this check to run hourly, if so desired.

#. Close your SSH session.

Takeaways
   - Nutanix uses STIGs to verify compliance.
   - Nutanix uses daily checks to self-remediate issues.