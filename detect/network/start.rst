.. _detect_day2:

###################################
Securing the Virtual Infrastructure
###################################

Your first hands-on experience with Nutanix was productive. You were impressed that it was all accomplished in less than a day. The automation helped alleviate much of the "grunt work" you used to complete on a quarterly basis, if not more often.

As you sit down at your desk, sipping your coffee, you log in to the Nutanix console to notice that VMs are already starting to be created. Your peers don’t waste any time, do they?

This gives you pause. This cloud-like consumption method, while great for end-users, could quite easily get out of hand if the VMs they create aren’t appropriately (and automatically!) protected. You recall a session that Rick gave on Flow micro-segmentation. It began by assigning categories to VMs, so they could later be acted upon as a logical group, such as being protected with policies for security and backup.

Nutanix Flow provides:

   - Multiple system categories out of the box that are used to quickly group virtual machines. Security policies can then be applied using these categories. You can choose the existing categories, or add your own.

   - A detailed visualization of communications between VMs, which can aid in categorizing and grouping workloads, making it simple and straight-forward to set the right policies for the environment.

Nutanix Flow has already been enabled for this environment, however we've include the steps required below.

#. Within Prism Central, select :fa:`bars` **> Prism Central Settings**.

#. Under *Flow*, select **Microsegmentation**.

#. Select the **Enable Microsegmentation** check box, and then click **Save**.

   .. figure:: images/enableflow.png