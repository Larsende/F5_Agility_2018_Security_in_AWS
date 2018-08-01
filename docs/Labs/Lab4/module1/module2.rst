Deploy Hackazon App using F5 Declarative AS3 Template
-----------------------------------------------------

**Delete hackazon_vs**

#. From the BIG-IP GUI, select **Local Traffic->Virtual Servers** page
#. Select check box next to ``hackazon_vs`` then click ``delete``.
#. Select ``delete`` again to confirm deletion.
#. Open a browser and ensure hackazon app is no longer working.

**Deploy F5 Application Services**

#. On the Jump host, type ``ansible-playbook playbooks/hackazon.yaml.  Enter BIG-IP Username and Password when prompted.  This will deploy the new app services along with waf policy created in Lab3.

   .. image:: ./images/image418.png
      :height: 400px

#. From the BIG-IP GUI, select **Local Traffic->Virtual Servers** page and note no virtual server is listed.
#. Select ``Hackazon`` on the Partition drop down menu to reveal ``serviceMain`` virtual server.

   .. image:: ./images/image420.png
      :height: 400px

#. Open a browser and ensure hackazon app is working again.
