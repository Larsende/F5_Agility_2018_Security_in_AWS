Deploy the BIG-IP
-----------------

In Module 2 we will deploy the BIG-IP into the AWS VPC created in Module 1.

F5 publishes CFTs on a regular basis to Github.

Launch BIG-IP into existing VPC
```````````````````````````````

We will use the instructor provided CFT to launch a BIG-IP into the VPC that already exists.

First, we need to create and save a key pair.

#. In the AWS Management Console, navigate to :guilabel:`EC2` and then under `Network & Security` to :guilabel:`Key Pairs` 
#. Click :guilabel:`Create Key Pair` and name it ``Student#-BIG-IP``.
#. Click :guilabel:`Create` and it will download the ``Student#-BIG-IP.pem`` file to your local machine. Be sure to keep track of this file as you will need it to access the BIG-IP later.
#.  You will need to change the permissions of the ``Student#-BIG-IP.pem`` key pair. 
  On a MAC, open a terminal and go to the folder you saved the ``Student#-BIG-IP.pem`` key pair. To change the file permissions type: 

  ``chmod 400 Student#-BIG-IP.pem``

Next, we're ready to deploy the CFT.

#. Got to: |CFT-template|
#. At the ``Select Template`` page, ensure you are still in the same region where you created your VPC, note the template URL is already selected, and click :guilabel:`Next`.
#. Create a :guilabel:`Stack name` of ``Student#-BIG-IP-CFT``
#. Find your ``Student#-VPC-CFT`` VPC in the drop down.
#. For the :guilabel:`Management Subnet AZ1` select ``Student#-VPC-CFT-MgmtSubnet`` (you may have to scroll down the list).
#. Similarly, assign the ``Student#-VPC-CFT-External Subnet`` and ``Student#-VPC-CFT-Internal Subnet`` subnets for :guilabel:`Subnet1` and :guilabel:`Subnet2`.
#. Ensure the :guilabel:`BIG-IP Image Name` is set to ``AWAF25Mbps``
#. Ensure the :guilabel:`AWS Instance Size` is set to ``t2.large``.
#. Utilize the ``Student#-BIG-IP`` key in the drop down for :guilabel:`SSH Key`
#. Enter ``0.0.0.0/0`` in the :guilabel:`Source Address(es) for Management Access`
#. Enter ``0.0.0.0/0`` in the :guilabel:`Source Address(es) for Web Application Access (80/443)` field.
#. Leave all other fields at default values and select :guilabel:`Next`.
#. Leave all fields in the :guilabel:`Options` page at defaults and select :guilabel:`Next`.
#. Review the settings, check the :guilabel:`I acknowledge that AWS CloudFormation might create IAM resources` box and click :guilabel:`Create`.
#. Refresh the page to see the status of the deployment. 
#. Wait until the status of the CFT shows ``CREATE_COMPLETE``


Set the admin password for BIG-IP VE
````````````````````````````````````
To initially change the password for the BIG-IP management utility we need to connect via SSH and then modify the admin password.

#. Go to :guilabel:`EC2` -> Instances -> instances
#.  Find the EIP that the CFT created for the ``Management`` interface of your BIG-IP instance by going to :guilabel:`EC2 -> Network Interfaces` and filtering for ``Student#-BIG-IP``. Note the ``IPv4 Public IP`` address for the ``Management`` interface.
#. You can connect using an SSH utility - make sure to use ``admin`` as the username (do not use ``root``) and the ``Management EIP`` from the previous step. Use the ``Student#-BIG-IP.pem`` key pair you saved when you created the instance in Lab 1. For example: 
    ``ssh -i Student#.pem admin@<EIP-of-Management>``
#.  After connecting via SSH issue the command ``modify auth password admin`` - change the admin password to one that you will remember
#.  Save the password change by issuing the command ``save sys config``
#.  You can now connect to the BIG-IP Web UI on HTTPS using the EIP for the management interface (bypass the self-signed cert warning) and the credentials admin/<password-from-step-4>
#.  Once logged in to the F5 management console click on System, Resource Provisioning.
#.  Select ASM, Fraud Protection Service, and iRules Language Extensions (iRulesLX).
#.  Unselect LTM 
#.  Click on Submit and then OK.  The admin console will be inaccessible for a couple minutes as the new options are enabled.


.. |github| raw:: html

   <a href="https://github.com/F5Networks/f5-aws-cloudformation/tree/master/supported/standalone/3nic/existing-stack/payg" target="_blank">F5's Github repository</a>

.. |CFT-template| raw:: html

   <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?templateURL=https:%2F%2Fs3-external-1.amazonaws.com%2Fcf-templates-k2dflj3mk02p-us-east-1%2F2018201LuF-template191z9ht7gde7&redirectId=DesignTemplate" target="_blank">F5 Advanced WAF Cloud Formation Template</a>