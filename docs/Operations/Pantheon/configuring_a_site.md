# Configuring a Site

In order for a D7-WebExpress site to work properly on Pantheon there are a number of variables to set and modules enable and disable. Use the following lists to make the correct settings.

Make sure you have [terminus](Pantheon-index#user-content-terminus) installed. 

## **setting site variables**

You can use `terminus remote:drush SITE_NAME.live -- vset VARIABLE_NAME VARIABLE_VALUE` in the terminal to set each of these variables:

### **variable names and values**
*name*|*value*
---|---
'simplesamlphp_auth_installdir|/code/vendor/simplesamlphp/simplesamlphp
'simplesamlphp_auth_registerusers|1
'honeypot_file_default_scheme|public
'smtp_allowhtml|0
'smtp_from|webexpress_noreply@colorado.edu
'smtp_fromname|"Web Express"
'smtp_host|smtp.office365.com
'smtp_on|1
'smtp_port|587
'smtp_password|YOU_WILL_NEED_TO_ASK_FOR_THIS
'smtp_protocol|tls
'smtp_queue|0
'smtp_queue_fail|0
'smtp_username|webexpress_noreply@colorado.edu
'smtp_debugging|2
'smtp_deliver|1
'smtp_default_timezone|"America/Denver"

## **configuring modules**

be sure to follow the order of modules as listed below. You can use `terminus remote:drush SITE_NAME.live -- en MODULE_NAME` to enable or `terminus remote:drush SITE_NAME.live -- dis MODULE_NAME` to disable modules

*en/dis*|*module name*
---|---
en|cu_users
en|dblog
en|pantheon_api
en|pantheon_advanced_page_cache
en|smtp
en|cu_core
en|noreqnewpass
en|cu_saml
en|simplesamlphp_auth
dis|ucb_on_prem_hosting
dis|pantheon_hosting
dis|memcache
dis|varnish
dis|ldap_authentication
dis|syslog
dis|cu_atlas
dis|atlas
dis|express_site_metrics
dis|cu_logout_users
en|cu_ldap
en|ldap_user
en|ldap_servers
dis|cu_ldap
dis|ldap_user
dis|ldap_servers