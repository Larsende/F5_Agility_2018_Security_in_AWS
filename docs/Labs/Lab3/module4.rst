Create Credentials Protection WAF Child Policy
----------------------------------------------
**Task 1 - Simulate credential attacks.**

#. Open browser on jump server and go to ``https://hackazon.f5demo.com/user/login``
#. Enter ``bigmac`` for **Username**
#. Enter random password for **Password.**  Repeat 5 consecutive times using different password to simulate brute force attack

   .. NOTE::

      This is a common ``brute force`` attack. In this case the application allowed
      repeated attempts without lockout.  Some applications will send "account locked"
      for a period of time, however user can continue to repeated attempts to
      elongate lockout period.

#. Open new incognito browser on jump server and open developer tools. (View->Developer-Developer Tools)
#. Browse to ``https://hackazon.f5demo.com/user/login`` and login as ``bigmac``
#. Once successfully logged in, review log on Developer Tool.  Highlight ``login?return_url=`` and on right panel scroll to bottom of Form Data to view **Username** and **Password**.

   .. image:: ../images/image340.png
     :height: 400px

**Task 2 - Create new waf policy to mitigate the vulnerabilities using info on table below:**

.. list-table::
    :widths: 20 40
    :header-rows: 0
    :stub-columns: 0

    * - **Policy Name**
      - waf_baseCredentials
    * - **Policy Type**
      - Security
    * - **Parent Policy**
      - waf_base
    * - **Virtual Server**
      - none
    * - **Enforcement Mode**
      - Blocking

#. Select the Security->Application Security->Security Policies->Policies List page
#. Click **Create Policy**

   .. image:: ../images/image341.png
     :height: 300px

**Task 3 - Configure Brute Force Protection**

#. Select **Security->Application Security->Sessions and Logins->Login Pages List** page
#. Click **Create**

   .. image:: ../images/image342.png
     :height: 300px

#. Open the **Application Security->Anomaly Detection->Brute Force Attack Prevention** page and click **Create**.
#. Select **Security->Application Security->Anomaly Detection->Brute Force Attack Prevention** then click **Create**
#. Change **Login Page** drop down box to ``[HTTP]/user/login``
#. Click **Apply Policy** to commit changes

   .. image:: ../images/image343.png
     :height: 50px

**Task 4 - Configure Credential Encryption**

#. Select **Security->Application Security->Data Protection->DataSafe Profiles**
#. Click **Create**

   .. image:: ../images/image344.png
     :height: 100px

#. Enter ``protect_credentials`` for **Profile Name**

   .. image:: ../images/image345.png
     :height: 300px

#. Select **URL List** and click **Add**

   .. image:: ../images/image346.png
     :height: 150px

#. Select **Parameters** then enter ``username`` in the **Parameter Name** and click Add
#. Check **Identify as Username** and **Encrypt** check boxes
#. Enter ``password`` in the **Parameter Name** and click Add
#. Check **Encrypt** check box

   .. image:: ../images/image347.png
     :height: 150px

#. Click **Login Page Properties**
#. Check **Yes** for **URL is Login Page**
#. Enter ``My Account`` for **A string should appear**
#. Enter ``Username or password are incorrect`` for **A string that should NOT appear**

   .. image:: ../images/image348.png
     :height: 300px
#. Click **Save**

**Task 5 - Assign policies to protect Hackazon App**

#. Select **Local Traffic->Virtual Servers->Virtual Servers List** and click on ``hackazon_vs``
#. Select **Security** then **Policy** tab
#. Change **Application Security Policy** to ``waf_baseCredentials``
#. Enable **Anti-Fraud Profile** and select ``protect_credentials``
#. Click **Update**

   .. image:: ../images/image349.png
     :height: 300px

**Task 6 - Repeat simulated credential attacks**

#. Open browser on jump server and go to ``https://hackazon.f5demo.com/user/login``
#. Enter ``bigmac`` for **Username**
#. Enter random password for **Password.**  Repeat multiple times using different password to simulate brute force attack.  You should receive a captcha challenge after 3 failed attempts.
#. Enter code from captcha challenge then enter correct credentials to login in successfully.

#. Open new incognito browser on jump server and open developer tools. (View->Developer-Developer Tools)
#. Browse to ``https://hackazon.f5demo.com/user/login`` and login as ``bigmac``
#. Once successfully logged in, review log on Developer Tool.  Highlight ``login?return_url=`` and on right panel scroll to bottom of Form Data to view encrypted **Username** and **Password**
