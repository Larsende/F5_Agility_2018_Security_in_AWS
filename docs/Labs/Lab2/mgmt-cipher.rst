SSL Security of F5 Management
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

There are some vulnerabilities in the default HTTPS access of the management on the F5 documented here: https://support.f5.com/csp/article/K13400.  To midicate this we will disable all non-TLSv1.2 connections to the management by doing the following via SSH:

1. Log in to tmsh by typing the following command:

    tmsh

2. Before you change the SSL cipher string, you should review the existing string for your specific BIG-IP version. To list the currently configured cipher string, type the following command:
    
    list /sys httpd ssl-ciphersuite

For example, the BIG-IP 11.5.1 system displays the following cipher string:

ALL:!ADH:!EXPORT:!eNULL:!MD5:!DES:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2

3. To restrict Configuration utility access to clients using TLS 1.2 or RC4-SHA ciphers, type the following command:

    modify /sys httpd ssl-ciphersuite 'ALL:!ADH:!EXPORT:!eNULL:!MD5:!DES:!SSLv2:-TLSv1:-SSLv3:RC4-SHA'

Alternatively, if you can restrict to only TLS 1.1 and TLS 1.2 ciphers, then type the following command instead:

    modify /sys httpd ssl-ciphersuite 'ALL:!ADH:!EXPORT:!eNULL:!MD5:!DES:!SSLv2:!SSLv3:!TLSv1'

4. Save the configuration change by typing the following command:

    save /sys config
