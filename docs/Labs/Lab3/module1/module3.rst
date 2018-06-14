Create WAF Policy - Low
-----------------------
Create new waf policy using info on table below:

.. list-table::
    :widths: 20 40
    :header-rows: 0
    :stub-columns: 0

    * - **Policy Template**
      - Rapid Deployment Policy
    * - **Virtual Server**
      - hackazon_vs
    * - **Learning Mode**
      - manual
    * - **Enforcement Mode**
      - Blocking
    * - **Signature Staging**
      - Disabled


#. Select the **Security->Application Security->Security Policies->Policies List** page
#. Click **Create New Policy**
#. Select **Advanced** options

   .. image:: /_static/image308.png
     :height: 30px

#. Enter ``waf_policy_low`` for **Policy Name**
#. Select **Rapid Deployment Policy** for **Policy Template**
#. Select ``hackazon_vs`` for **Virtual Server**
#. Select **Manual** for **Learning Mode**
#. Change **Enforcement Mode** to **Blocking**
#. Change **Signature Staging** to **Disabled**

   .. image:: /_static/image309.png
     :height: 400px

#. Click **Create Policy**

.. NOTE::

   This creates a basic security policy with ASM. Using Rapid Deployment
   includes several common security measures and thousands of attack signatures.
   Signature Staging is Disabled for this lab demo but most likely enabled for
   production environments.
