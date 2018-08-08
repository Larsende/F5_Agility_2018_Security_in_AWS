Setting up Hackazon Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**We will now setup an SSL Offload Virtual Server using the Cipher Group previously configured.**

#. Go to the F5 Admin page and select :guilabel:`Local Traffic -> Profiles -> SSL -> Client`

#. Click on :guilabel:`Create`

#. For the :guilabel:`SSL profile name` Enter ``hackazon-clientssl.prf``

#. Select :guilabel:`Advanced` configuration.

#. Select the checkbox to :guilabel:`modify Ciphers` and select :guilabel:`Cipher Group` and in the dropdown select your Cipher Group that you created.

   .. image:: ./images/image203a.png

#. Leave other options as default and click on :guilabel:`Finished`

#. Go to :guilabel:`Local Traffic -> Pools`

#. Click on :guilabel:`Create`

#. In the :guilabel:`Pool Name` field enter ``hackazon.p``

#. Select the :guilabel:`HTTP health monitor` and move it to :guilabel:`Active`

#. Put in the following two IP addresses into the list of pool members both on port 80:  ``18.205.1.169``, and ``34.239.240.82``

   .. image:: ./images/image204.png
      :height: 400px

#. Click on :guilabel:`Finished`

#. Go to the AWS console, Select :guilabel:`Services` and then :guilabel:`EC2`. Select :guilabel:`Instances`  Filter for your ``student#`` and select the checkbox for the one labeled :guilabel:`BIG-IP:Student#-CFT`.

#. In the description for the instance there is a list of :guilabel:`Elastic IPs`.  Click on the last one in the list.  It will also not have a * at the end of the IP address.

#. In the definition of the Elastic IP there will be a :guilabel:`Private IP address`.  This IP will become your Virtual Server Destination address.  The :guilabel:`Elastic IP` will be the IP for accessing the application.

   .. image:: ./images/image202.png

   This screenshot illustrates one example. The presented IP addresses will not be the ones you see

#. Go to :guilabel:`F5 Admin page` and then :guilabel:`Local Traffic -> Virtual Servers`

#. Click on :guilabel:`Create`

#. Enter a :guilabel:`Virtual Server Name` of ``hackazon_vs``

#. In the :guilabel:`Destination Address` field enter ``Private IP address`` that you determined earlier as part of the ``Elastic IP`` information.

#. For :guilabel:`Service Port` enter ``443``

#. For :guilabel:`HTTP Profile` select ``HTTP`` from the dropdown menu.

#. In the :guilabel:`SSL Profile (client)` field move ``hackazon_clientssl.prf`` from :guilabel:`Available` into :guilabel:`Selected`

#. In the :guilabel:`Source Adress Translation` select ``Automap``

#. In the :guilabel:`Resources` section under :guilabel:`Default Pool` select ``hackazon.p`` from the dropdown list.

   .. image:: ./images/image205.png
      :height: 500px

#. Click on :guilabel:`Finished`

#. Now take the :guilabel:`Elastic IP` you found earlier in the AWS Console, open a web browser and go to ``https://<Elastic IP>``.  You will get a certificate error because we are not using a domain specific SSL Certificate.  Once ignoring the certificate error you should start seeing the hackazon web page.