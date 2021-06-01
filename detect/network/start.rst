.. _detect_day2:

------------------------------------------------
Securing the Virtual Infrastructure
------------------------------------------------

The first-day hands-on with Nutanix was pretty busy but productive. You were impressed that it was all accomplished in a single day, and the automation really helped alleviate much of the grunt work you used to have to complete on a quarterly basis, if not more often. 

Now that you’re happy that you’ve sufficiently secured the platform plane, the work begins to secure the data plane. 

In the morning, after sipping your coffee you log into the Nutanix console and notice that VM’s are already starting to be created. Your peers don’t waste any time! 

   .. figure:: images/cafe.png

This gives you pause for concern, this cloud-like consumption method, although great for end-users, could quite easily get out of hand if the VM’s aren’t appropriately protected. You remember that one of the sessions that the Nutanix SE: Rick hosted was on Flow Micro-segmentation and it began by requiring you to “Categorize” the VM’s so they could later be protected with policies for security and backup. 
Flow provides multiple System categories out of the box, such as AppType, AppTier, and Environment, that are used to quickly group virtual machines. Security policies are applied using these categories. You can start using these pre-existing categories right away, or add your own categories for custom grouping.

Flow Micro-segmentation
+++++++++++++++++++++++++

Nutanix Flow provides a detailed visualization of communications between VMs along with assistance in categorizing and grouping workloads, making it simple and straight-forward to set the right policies for the environment.

For the sake of the labs, Nutanix Flow is already enabled, but you can see how to enable Flow. 
**Hint - it is a single checkbox in typical Nutanix fashion!**

#. Log on to the Prism Central web console.
#. Click the :fa:`bars`, select **Prism Central Settings** to display the Settings page.
#. Click **Microsegmentation** from the Settings menu (on the left).
#. Select the **Enable Microsegmentation** check box.

The Enable Microsegmentation dialog box is displayed.


   .. figure:: images/enableflow.gif


   .. glossary:: 
         “Compared to competitive products, this is the easiest microsegmentation product I've ever seen.”
         Roy, CSO for Blips and Chitz
