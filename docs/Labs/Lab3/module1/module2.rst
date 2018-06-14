Create WAF logging profile
--------------------------

#. Select **Security->Event Logs->Logging Profiles** then click **Create**
#. Enter ``waf_log`` for **Profile Name**
#. Select the **Application Security, Dos Protection**, and **Bot Defense** checkboxes

   .. image:: /_static/image301.png
     :height: 200px

#. On the **Application Security** tab, for **Request Type** select **All requests**

   .. image:: /_static/image302.png
     :height: 100px

#. On the **DoS Protection** tab select the **Local Publisher** checkbox

   .. image:: /_static/image303.png
     :height: 100px

#. On the **Bot Defense** tab select the **Local Publisher, Log Illegal Requests** and **Log Challenged Requests** checkboxes

   .. image:: /_static/image304.png
     :height: 200px

#. Click Finished and you should see a waf_log

   .. image:: /_static/image305.png
     :height: 200px
