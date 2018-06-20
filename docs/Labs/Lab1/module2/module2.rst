Deploy the BIG-IP
-----------------

In Module 2 we will deploy the BIG-IP into the AWS VPC created in Module 1. We will also launch the Hackazon instance to use for Application Security configurations in subsequent Labs.

Utilize CFTs from Github
````````````````````````

F5 publishes CFTs on a regular basis to Github.

Navigate to |github| and read through the documentation. Note the ``Prerequisites`` section that describes the requirements for the subnets created in Lab 1.

When ready, launch the CFT for the ``Hourly`` -> ``existing stack`` template. Utilize the Github documentation to complete the deployment into your Student# VPC lab environment.


.. figure:: ../images/CFT_hourly.png

|

Launch CFT into existing VPC
````````````````````````````

We'll using the Github CFT to launch a second BIG-IP into the existing VPC that already exists.

1. At the ``Select Template`` page, ensure you are still in the ``N. California`` region, note the template URL is already selected, and click :guilabel:`Next`.
2. Create a :guilabel:`Stack name` of ``Student#-CFT``
3. Find your ``Student#`` VPC in the drop down.
4. Select the Management, External, and Internal subnets in the drop downs.
5. Change the :guilabel:`BIG-IP Image Name` to ``Good25Mbps``
6. Change the :guilabel:`AWS Instance Size` to ``t2.medium``.
7. Utilize the Student# key in the drop down for :guilabel:`SSH Key`
8. Enter the Lab Public IP in the :guilabel:`Source Address(es) for Management Access`
9. Enter ``0.0.0.0/0`` in the :guilabel:`Source Address(es) for Web Application Access (80/443)` field.
10. Leave all other fields at default values and select :guilabel:`Next`.
11. Leave all fields in the ``Options`` page at defaults and select :guilabel:`Next`.
12. Review the settings, check the ``I acknowledge that AWS CloudFormation might create IAM resources`` box and click :guilabel:`Create`.
13. Refresh the page to see the status of the deployment.


.. |github| raw:: html

   <a href="https://github.com/F5Networks/f5-aws-cloudformation/tree/master/supported/standalone/3nic" target="_blank">F5's Github repository</a>