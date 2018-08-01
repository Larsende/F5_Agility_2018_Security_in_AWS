Securing the SSL for the Application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Starting in v13.0 the allowed SSL Ciphers can be managed with a combination of SSL Cipher Rules and Cipher Groups.  Using a combination of these rules you can create a secure ClientSSL profile that will protect your app and allow the clients necessary.  

SSL Cipher Rules can be combined in the groups as follows:

.. image:: ./images/image201.png

#. We will start by creating a SSL Cipher Rule.  Click on **Local Traffic, Ciphers, Rules,** then **Create.**

#. Enter a name for the rule such as **hackazon-cipherrule.**

#. Enter the following Cipher String

     !SSLv2:!EXPORT:!DHE+AES-GCM:!DHE+AES:!DHE+3DES:ECDHE+AES-GCM:ECDHE+AES:RSA+AES-GCM:RSA+AES:ECDHE+3DES:RSA+3DES:-MD5:-SSLv3:-RC4

#. Click on **Finished.**

#. Now click on the **Groups** Tab.

#. Click on **Create.**

#. Enter a name for the Cipher Group such as **hackazon-ciphergroup.**

#. Select the **StudentX-cipherrule** previously created and add it to the **"Allow the Following" category.** 

#. Down at the bottom of the Cipher Group configuration will be the allowed Ciphers.  With the above string you will get a security configuration that will still allow some older clients like WindowsXP and IE8.  You can further secure it by removing TLSv1 or making it so the default f5-ecc cipher rule is in the "Restrict the Allowed List to the Following."

#. Click on **Finished.**