.. _detect_im:

####################
Simulating An Attack 
####################

You’re impressed so far, but like the old Russian proverb states: Доверяй, но проверяй; Trust, but verify. How can you simulate an attack against Blips and Chitz, Inc.? You don’t have the necessary experience to conduct a penetration test yourself, so you go about trying to find a tool that can simulate an Advanced Persistent Threat (APT).

What is Infection Monkey?
=========================

Infection Monkey by Guardicore, is a tool that can be used to simulate and automate many of the same actions a penetration test would typically perform. While penetration tests by skilled professionals are more thorough and accurate, this can serve as an initial attempt to expose potential critical vulnerabilities in this new system.

Infection Monkey is an open source breach and attack simulation (BAS) platform that allows you to discover security gaps and fix them. It uses various methods to self propagate across a data center, and reports success to a centralized *Monkey Island* server. You can simulate credential theft, compromised machines and other security flaws, and mimic the what is commonly observed in ransomware attacks, albeit non-destructively. Infection Monkey is executed from a user-friendly, web-based GUI.

The Infection Monkey is comprised of two parts:

   - *Monkey* - A tool which infects other machines and propagates to them.
   - *Monkey Island* - A dedicated server to control and visualize the Infection Monkey's progress inside the data center.

Installing Infection Monkey
===========================

#. Log in to your *USER##*\-WinTools VM using the following credentials:

      - **User Name** - `administrator`
      - **Password**  - `nutanix/4u`

#. Download Infection Monkey, and the required Microsoft Visual C++ package. Both are found here: `http://10.42.194.11/workshop_staging/InfectionMonkey/`.
 
#. You will first install the Microsoft Visual C++ package *VC_redist.x64* followed by *InfectionMonkey*.

#. When launching *Infection Monkey*, two terminal screens will open. These terminal sessions are for the *MongoDB* instance, and *C&C Server* (Command and Control). Minimize, but do not close these windows.

   .. figure:: images/image012.png

#. Additionally, Chrome will launch. This session may initially time-out, as it takes a few minutes for the *MongoDB* and *C&C Server* services to start. Once they are ready, you can refresh Chrome, and continue.

#. When connecting to the web interface for the first time, you will be prompted to setup a username and password, or continue without a username/password. The instructor will create this login.

Configuring Infection Monkey
============================

[TODO: Pete: All screenshots in this section are incorrect. Use 5 pt red borders, and many can be made smaller to focus on only what we need to illustrate.]

#. Select the **Network** tab.

   .. figure:: images/image016.png

#. Set the *Scan depth* to **1**. This will prevent Infection Monkey from scanning other subnets and host outside of the local subnet.

   .. figure:: images/image017.png

#. Set your **Scan Target** to the subnet of your HPOC environment. [TODO: Pete: This could use 1-2 examples for the HPOC]

   .. figure:: images/image018.png

#. Click **Submit**.

   .. figure:: images/image019.png
 
This will provide enough configuration to get going. Feel free to explore the exploits that will be run, **add any username and passwords** to the **Credentials** section under the **Exploits** tab, add a drop file or command in the **Monkey** tab. There are many options to customize the configuration. [TODO: Pete: This section needs to be rewritten, add screen shots, etc. to make it clear]

Run Infection Monkey
====================

[TODO: Pete: All screenshots in this section are incorrect. Use 5 pt red borders, and many can be made smaller to focus on only what we need to illustrate.]

#. Click **Run Monkey**.

   .. figure:: images/image020.png

#. Click **Run on Monkey Island Server**.

   .. figure:: images/image021.png

   Infection Monkey will require approximately 10 minutes to discover machines on the network.

#. Select **Infection Map**. This provides a visual map of the discovered machines, exploits, etc. You can also view the *Security Reports* while it is running, but I suggest waiting until the scan has completed. This will provide more complete information on the findings.

   .. figure:: images/image022.png

Conclusion
++++++++++

   - Once completed with the initial runs of **Infection Monkey**, create a **Flow Security Policy** to lock down your application. Then, **rerun** Infection Monkey to determine whether your security policy is now preventing Infection Monkey from discovering and exploiting your VMs protected by the Security Policy. [TODO: Pete: This section needs to be rewritten, add screen shots, etc. to make it clear. It's not a conclusion, sounds like more steps to do to actually test!]