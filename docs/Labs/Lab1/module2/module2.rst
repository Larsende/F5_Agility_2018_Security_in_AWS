Deploy the BIG-IP
-----------------

In Module 2 we will deploy the BIG-IP into the AWS VPC created in Module 1. We will also launch the Hackazon instance to use for Application Security configurations in subsequent Labs.

Utilize CFTs from Github
````````````````````````

F5 publishes CFTs on a regular basis to Github.

Navigate to |github| and read through the documentation. Note the ``Prerequisites`` section that describes the requirements for the subnets created in Module 1



|

Launch CFT into existing VPC
````````````````````````````

We'll using the Github CFT to launch a second BIG-IP into the existing VPC that already exists.

First, we need to create and save a key pair.

1. In the AWS Management Console, navigate to :guilabel:`EC2` and the :guilabel:`Key Pairs`
2. Click and name it ``Student#-BIG-IP``.
3. Click :guilabel:`Create` and it will download the ``Student#-BIG-IP.pem`` file to your local machine. Be sure to keep track of this file as you will need it to access the BIG-IP later.

Next, we're ready to deploy the CFT.

Launch the CFT for the ``Hourly`` -> ``existing stack`` template.

.. figure:: ../images/CFT_hourly.png

1. At the ``Select Template`` page, ensure you are still in the same region where you created your VPC, note the template URL is already selected, and click :guilabel:`Next`.
2. Create a :guilabel:`Stack name` of ``Student#-CFT``
3. Find your ``Student#`` VPC in the drop down.
4. Select the Management, External, and Internal subnets in the drop downs.
5. Change the :guilabel:`BIG-IP Image Name` to ``Good25Mbps``
6. Change the :guilabel:`AWS Instance Size` to ``t2.medium``.
7. Utilize the ``Student#-BIG-IP`` key in the drop down for :guilabel:`SSH Key`
8. Enter the Lab Public IP in the :guilabel:`Source Address(es) for Management Access`
9. Enter ``0.0.0.0/0`` in the :guilabel:`Source Address(es) for Web Application Access (80/443)` field.
10. Leave all other fields at default values and select :guilabel:`Next`.
11. Leave all fields in the ``Options`` page at defaults and select :guilabel:`Next`.
12. Review the settings, check the ``I acknowledge that AWS CloudFormation might create IAM resources`` box and click :guilabel:`Create`.
13. Refresh the page to see the status of the deployment.


Set the admin password for BIG-IP VE
````````````````````````````````````
1.  Find the BIG-IP instance in the AWS Console under :guilabel:`EC2 -> Instances`
2.  Highlight the BIG-IP instance in the list and click :guilabel:`Connect`
3.  Follow the instructions regarding connecting with an SSH utility - however, substitute ``admin`` as the username instead of root and ensure you use the ``Management EIP`` (the Connect instructions may have the incorrect IP). Use the .pem key pair you saved when you created the instance in Lab 1. For example: ``ssh -i Student#.pem admin@<EIP-of-Management>``
4.  After connecting via SSH issue the command ``modify auth password admin`` - change the admin password to one that you will remember
5.  You can now connect to the BIG-IP Web UI on HTTPS using the EIP for the management interface (bypass the self-signed cert warning) and the credentials admin/<password-from-step-4>


.. |github| raw:: html

   <a href="https://github.com/F5Networks/f5-aws-cloudformation/tree/master/supported/standalone/3nic" target="_blank">F5's Github repository</a>