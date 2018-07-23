Deploy the BIG-IP
-----------------

In Module 2 we will deploy the BIG-IP into the AWS VPC created in Module 1.



F5 publishes CFTs on a regular basis to Github.



Launch CFT into existing VPC
````````````````````````````

We'll using the instructor provided CFT to launch a BIG-IP into the VPC that already exists.

First, we need to create and save a key pair.

1. In the AWS Management Console, navigate to :guilabel:`EC2` and then :guilabel:`Key Pairs`
2. Click :guilabel:`Create Key Pair` and name it ``Student#-BIG-IP``.
3. Click :guilabel:`Create` and it will download the ``Student#-BIG-IP.pem`` file to your local machine. Be sure to keep track of this file as you will need it to access the BIG-IP later.

Next, we're ready to deploy the CFT.

1. Got to: |CFT-template|
2. At the ``Select Template`` page, ensure you are still in the same region where you created your VPC, note the template URL is already selected, and click :guilabel:`Next`.
3. Create a :guilabel:`Stack name` of ``Student#-BIG-IP-CFT``
4. Find your ``Student#-VPC-CFT`` VPC in the drop down.
5. Select the ``Student#-VPC-CFT-`` for Management, External, and Internal subnets in the drop downs.
6. Ensure the :guilabel:`BIG-IP Image Name` is set to ``AWAF25Mbps``
7. Ensure the :guilabel:`AWS Instance Size` is set to ``t2.large``.
8. Utilize the ``Student#-BIG-IP`` key in the drop down for :guilabel:`SSH Key`
9. Enter the Lab Public IP (this will be given in the classroom) in the :guilabel:`Source Address(es) for Management Access`
10. Enter ``0.0.0.0/0`` in the :guilabel:`Source Address(es) for Web Application Access (80/443)` field.
11. Leave all other fields at default values and select :guilabel:`Next`.
12. Leave all fields in the :guilabel:`Options` page at defaults and select :guilabel:`Next`.
13. Review the settings, check the :guilabel:`I acknowledge that AWS CloudFormation might create IAM resources` box and click :guilabel:`Create`.
14. Refresh the page to see the status of the deployment.


Set the admin password for BIG-IP VE
````````````````````````````````````
To initially change the password for the BIG-IP management utility we need to connect via SSH and then modify the admin password.

1.  First, you will need to change the permissions of the ``Student#-BIG-IP.pem`` key pair you saved above. (For example, ``chmod 400 Student#-BIG-IP.pem``)
2.  Next, find the EIP that the CFT created for the ``Management`` interface of your BIG-IP instance by going to :guilabel:`EC2 -> Network Interfaces` and filtering for ``Student#``. Note the IP address for the ``Management`` interface.
3.  You can connect using an SSH utility - make sure to use ``admin`` as the username (do not use ``root``) and the ``Management EIP`` from the previous step. Use the ``Student#-BIG-IP.pem`` key pair you saved when you created the instance in Lab 1. For example: ``ssh -i Student#.pem admin@<EIP-of-Management>``
4.  After connecting via SSH issue the command ``modify auth password admin`` - change the admin password to one that you will remember
5.  Save the password change by issuing the command ``save sys config``
6.  You can now connect to the BIG-IP Web UI on HTTPS using the EIP for the management interface (bypass the self-signed cert warning) and the credentials admin/<password-from-step-4>
#.  Once logged in to the F5 management console click on System, Resource Provisioning.
#.  Select ASM, Fraud Protection Service, and iRules Language Extensions (iRulesLX).
#.  Click on Submit and then OK.  The admin console will be inaccessible for a couple minutes as the new options are enabled.


.. |github| raw:: html

   <a href="https://github.com/F5Networks/f5-aws-cloudformation/tree/master/supported/standalone/3nic/existing-stack/payg" target="_blank">F5's Github repository</a>

.. |CFT-template| raw:: html

   <a href="https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new?templateURL=https:%2F%2Fs3-external-1.amazonaws.com%2Fcf-templates-k2dflj3mk02p-us-east-1%2F2018201LuF-template191z9ht7gde7&redirectId=DesignTemplate" target="_blank">F5 Advanced WAF Cloud Formation Template</a>