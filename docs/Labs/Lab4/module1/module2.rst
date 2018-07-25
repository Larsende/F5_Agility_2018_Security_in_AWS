Deploy Hackazon App using F5 Declarative AS3 Template
-----------------------------------------------------

**Delete hackazon_vs**
#. From the BIG-IP GUI, select **Local Traffic->Virtual Servers** page
#. Select check box next to ``hackazon_vs`` then click ``delete``.
#. Select ``delete`` again to confirm deletion.
#. Open a browser and ensure hackazon app is no longer working.

**Deploy F5 Application Services**
#. On the Jump host, type ``ansible-playbook playbooks/hackazon.yaml.  Enter BIG-IP Username and Password when prompted.
This will deploy the new app services along with waf policy created in Lab3.
#. Open a browser and ensure hackazon app is working again.
