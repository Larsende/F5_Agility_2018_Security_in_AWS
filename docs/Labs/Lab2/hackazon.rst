Setting up Hackazon Virtual Server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**We will now setup an SSL Offload Virtual Server using the Cipher Group previously configured.**

#. Go to the F5 Admin page and select **Local Traffic -> Profiles -> SSL -> Client.**

#. Click on **Create.**

#. Enter a name for your SSL profile **hackazon-clientssl.prf.**

#. Select **Advanced** configuration.

#. Select the checkbox to **modify Ciphers** and select **Cipher Group** and in the dropdown select your Cipher Group that you created.

   .. image:: ./images/image203a.png

#. Leave other options as default and click on **Finished.**

#. Go to **Local Traffic -> Pools**

#. Click on **Create**

#. Enter a pool name **hackazon.p**

#. Select the **HTTP health monitor** and move it to Active.

#. Put in the following two IP addresses into the list of pool members both on port 80:  **18.205.1.169**, and **34.239.240.82**

   .. image:: ./images/image204.png

#. Click on **Finished.**

#. Go to the AWS console, Select Services and then EC2. Select **Instances.**  Filter for your student# instance of the BIG-IP.

#. In the description for the instance there is a list of **Elastic IPs.**  Click on the last one in the list.  It will also not have a * at the end of the IP address.

#. In the definition of the Elastic IP there will be a **private IP address.**  This IP will become your Virtual Server Destination address.

   .. image:: ./images/image202.png

   This screenshot illustrates one example. The presented IP addresses will not be the ones you see

#. Go to **Local Traffic -> Virtual Servers.**

#. Click on **Create.**

#. Give the virtual server a name such as hackazon_vs.

#. Enter as **destination address** the *Private IP address* that you determined earlier from the Elastic IP information in Step 3.

#. Enter the service port of **443.**

#. Select the **HTTP Profile** of HTTP.

#. Select the **hackazon_clientssl.prf** SSL Profile (client) and put it into Selected.

#. Select **Automap** in the Source Address Translation option.

#. Select the **Default Pool** of **hackazon.p** from the pool dropdown list.

   .. image:: ./images/image205.png

#. Click on Finished.


#. Now take the Elastic IP you found in Step 3 and open a web browser and go to 'https://<Elastic IP>'.  You will get a certificate error for mismatch but after ignoring the certificate error you should start seeing the hackazon web page.
