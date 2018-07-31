Deploy Jump host
----------------
**Launch new EC2 resource.**

#. In the AWS Management Console, navigate to EC2 and click ``Launch Instance``.
#. Select ``Amazon Linux AMI 2018.03.0 (HVM), SSD Volume Type - ami-cfe4b2b0``.

   .. image:: ./images/image410.png
      :height: 200px

#. Select ``t2.micro`` then click ``Next: Configure Instance Details``
#. Find your ``Student#-VPC-CFT`` Network in the drop down.
#. Find your ``Student#-VPC-CFT-MgmtSubnet`` Subnet in the drop down.
#. Select ``Enable`` to Auto-assign Public IP in the drop down.
#. Expand ``Advanced Details`` on bottom of page and paste the following code into ``User Data`` box.

   .. code::

     #!/bin/bash
     yum update -y
     yum install -y docker
     yum install -y telnet
     yum install -y curl
     yum install -y ab
     /sbin/chkconfig --add docker
     service docker start

#. Click ``Next: Add Storage``
#. Click ``Next: Add Tags``
#. Click ``Next: Configure Security Group``
#. Select ``Existing Security`` and find your ``Student#-VPC-CFT-bigipManagement`` in the drop down.
#. Click ``Review and Launch``
#. Click ``Launch``
#. Utilize the Student#-BIG-IP key in the drop down for SSH Key
#. Check the I acknowledge that AWS CloudFormation might create IAM resources box and click Launch Instances.

**Prepare BIG-IP to utilize iAppLX Application Services (AS3)**

#. Follow instructions for Downloading and Installing the AS3 Package then return after install.  Instructions at `this link`_.

   .. _this link: https://clouddocs.f5.com/products/extensions/f5-appsvcs-extension/3/userguide/installation.html

**Launch F5 Super-NetOps docker instance**

#. View Instances and and filter for your Student# to see your unamed instance.
#. Connect to Jump Host using ssh utility. For example; ssh -i "Student#-BIG-IP.pem" ec2-user@<jump_host>
#. Type ``sudo docker run -it f5usecases/f5-rs-container:latest``
#. Type ``git clone https://github.com/gotspam/as3-examples.git``
#. Type ``cd as3-examples``

**Modify ansible files for your environment**

#. Type ``vim inventory/hosts`` and change address to your **BIG-IP Private IP Address (eth0)**.  This is the BIG-IP Management IP and is typically the first **Private IP** listed or by clicking on eth0.

   .. image:: ./images/image415.png
      :height: 50px

#. Type ``vim roles/hackazon/files/hackazon.json`` and change address to your **BIG-IP Private IP Address** of the Elastic IP found in Lab2.

   .. image:: ./images/image416.png
      :height: 400px

**Test Ansible communication with BIG-IP**

You will now need to setup security permissions on AWS EC2 console so that Ansible can communicate with the BIG-IP.
#. In the AWS EC2 console go to Network Interfaces and Filter by your studentID.
#. Select the Interface labeled "Primary network interface".
#. In the bottom area look for the "Primary private IPv4 IP:"
#. Now select Security Groups on the left hand side.
#. Filter by your Student# and then select the Bigip Management instance.
#. Click the Inbound tab at the bottom and then select Edit.
#. Click on Add Rule.
#. Select SSH and then put the IP you found earlier in the source with a /32.
#. Click on Add Rule again.
#. Select HTTPS and then put the IP you found earlier in the source with a /32.
#. Click on Save.
#. Go back to your SSH into the Ansible host.
#. Type ``ssh admin@<BIG-IP Private IP Address (eth0)>``.  After successfully logging in, type ``quit`` to disconnect ssh session.
#. Type ``ansible-playbook playbooks/cmd.yaml``.  Enter BIG-IP Username and Password when prompted.

   .. image:: ./images/image417.png
      :height: 400px
