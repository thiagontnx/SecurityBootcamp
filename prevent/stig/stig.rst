.. _prevent_stig:

------------------------------------------------
STIG
------------------------------------------------

STIG reports on Nutanix nodes:	6
Analyzing the STIG Report	8
Ricks’ SCMA (Saltstack) Self-Healing Lab:

STIG reports on Nutanix nodes
+++++++++++++
You can run a STIG report, which will check on all the STIGs and verify which are compliant with your system or not.
The steps to run the STIG report are as follows:
#. Connect to any Controller VM (CVM) as the nutanix user via SSH (Using Terminal, PuTTy, or similar program)
#. Change to the root directory of the CVM
   
   .. note:: 

   cd / 

#.List the files available to the root user within the /root directory. Executable files contain x in the permission string.
   
   .. note:: 

   sudo -u root ls -l /root

You should see a similar output:
   
   .. note::

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
   
There should be three .sh files that end in _stig.sh and the name corresponds to the output format. You’ll want to run the one that outputs in the format you prefer.
#. In this example, we’ll run the generic text output “report_stig.sh”

   .. note::
   sudo -u root ./root/report_stig.sh
 
The output will go into the root user log folder.

#. List the files in the folder and note the name of the report.

   .. note::
   sudo -u root ls -l /home/log | grep STIG

#. Copy the report to the nutanix home directory, substituting the actual file name for the asterisks.
      
   .. note::
   sudo -u root cp /home/log STIG-report-**-**-****-**-**-** /home/nutanix

#. List the files in the /home/nutanix folder.
      
   .. note::
   ls -l ~

#. Change the owner of the report file to be the Nutanix user, substituting the actual file name for the asterisks.
      
   .. note::
   sudo -u root chown nutanix:nutanix /home/nutanix/STIG-report-**-**-****-**-**-**

#.1 Use a secure copy tool (SCP, WINSCP, PSCP, etc) to copy the report results file to your workstation from the CVM.
   
   .. note::
   Note: Be sure to login to the CVM using the nutanix username and browse to its home directory to find the file we created above.
