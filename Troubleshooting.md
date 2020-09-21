For troubleshooting get back to the log file which gets stored within the path: %TEMP%\DriveMapping.log.

* Access to the network drives
    * Verify access to the UNC path from a test machine. Also, have an eye on VPN connections and DNS resolution.

* Authentication
    * Ensure that authentication works and that you don't receive sign-in prompts. 
    * If you have Windows Hello for Business enabled, verify, SSO is properly configured and working.

* Security group filtering
    * Verify on a test machine the functionality of the Get-ADGroupMembership function. If you experience issues override the $searchRoot variable with your Active Directory Domain name.
    * Ensure that you specified the sAMAccountName without domain name prefix
    * If your test machines don't have a value for the PowerShell environment variable $env:USERDNSDOMAIN you need to populate the $searchRoot variable in the script.

