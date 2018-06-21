Create Base WAF Child Policy
----------------------------
**Task 1 - Simulate attacks to demonstrate common web app vulnerabilities.**

#. Open browser on jump server and go to ``https://hackazon.f5demo.com``
#. Enter ``%' or 1='1`` in Search field and press Enter

   .. NOTE::

      This is a common ``sql injection`` attack and although this did not return
      anything exciting the search request was accepted and processed with response.

#. Enter ``<script>alert("Your system is infected! Call 999-888-7777 for help.")</script>`` in Search field and press Enter

   .. NOTE::

      This is a common ``Cross-site scripting (XSS)`` attack and although this did not return
      anything exciting the search request was accepted and processed with response.

**Task 2 - Create new waf policy to mitigate the vulnerabilities using info on table below:**

.. list-table::
    :widths: 20 40
    :header-rows: 0
    :stub-columns: 0

    * - **Policy Name**
      - waf_baseOnly
    * - **Policy Type**
      - Security
    * - **Parent Policy**
      - waf_base
    * - **Virtual Server**
      - hackazon_vs
    * - **Enforcement Mode**
      - Blocking

#. Select the **Security->Application Security->Security Policies->Policies List** page
#. Click **Create New Policy**
#. Select **Advanced** options
#. Enter ``waf_baseOnly`` for **Policy Name**
#. Select **Security** for **Policy Type**
#. Enter ``waf_base`` for **Parent Policy**
#. Select ``hackazon_vs`` for **Virtual Server**
#. Change **Enforcement Mode** to **Blocking**

   .. image:: ../images/image311.png
     :height: 400px

#. Click **Create Policy**

   .. image:: ../images/image312.png
     :height: 400px

   .. NOTE::

      This creates a child security policy which inherits the settings from the
      waf_base Parent Policy.  The parent policy settings was created using Rapid
      Deployment Template which includes several common security measures and
      thousands of attack signatures. Signature Staging is Disabled for this lab
      demo but most likely will be enabled for production environments.

**Task 3 - Test WAF policy.**

#. Select the **Virtual Servers->Virtual Servers List** page
#. Click the **hackazon_vs** to display virtual server properties
#. Click the **Security->Policies** tab to display Policy Settings
#. Ensure **waf_log** profile is selected in the Log Profile
#. Select **update**

   .. image:: ../images/image313.png
     :height: 300px

#. Open browser on jump server and go to ``https://hackazon.f5demo.com``
#. Enter ``%' or 1='1`` in Search field and press Enter.  You should receive a block message similar to below. Take note of the Support ID number.

   .. image:: ../images/image314.png
     :height: 70px

#. Return to hackazon main page
#. Enter ``<script>alert("Your system is infected! Call 999-888-7777 for help.")</script>`` in Search field and press Enter.  You should see a similar block message. Take note of the Support ID number.

**Task 4 - Review WAF event logs on BIG-IP GUI.**

#. Select the **Security->Event Logs->Application->Requests** page
#. Select the ``Event`` with the matching ``Support ID`` noted on the block pages

   .. image:: ../images/image315.png
     :height: 300px


   .. NOTE::

      You can view the "Decoded Requests" and the "Original Request" however the ``Response`` is not captured by default.

#. Select ``Attack Signatures Detected`` to view details of the request that triggered the violation.

   .. image:: ../images/image316.png
     :height: 200px
