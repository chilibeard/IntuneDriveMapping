Welcome to the IntuneDriveMapping wiki!

## Adding network drive mapping entries

**UNC Path** - enter the network path for your file share. Examples:

* `\\ds.tech.nicolonsky.ch\dfsroot\public`

If you want to use environment variables use PowerShell environment variables:
* `\\ds.tech.nicolonsky.ch\dfsroot\homes\$env:username`

**Drive Letter** - enter a character in the range of A-Z without the colon.

**Display Name** - reflects the name displayed in windows explorer.

**Security Group Filter** - enter the sAMAccountName **without domain prefix** of an on-premises Active Directory group the user needs to be a member of. 

## Download the script

If you select the `remove stale drives` option before downloading the script, network drives not specified in the configuration gets disconnected. This is useful if you want to automatically remove stale drives which are no longer required and/or maintained by your configuration.

## Troubleshooting

For troubleshooting get back to the log file which gets stored within the path: `%TEMP%\DriveMapping.log`.

### Access to the network drives

Verify access to the UNC path from a test machine. Also, have an eye on VPN connections and DNS resolution.

### Authentication

Ensure that authentication works and that you don't receive sign-in prompts. If you have Windows Hello for Business enabled that SSO is [properly configured](https://docs.microsoft.com/en-us/windows/security/identity-protection/hello-for-business/hello-hybrid-aadj-sso-base). 

### Security group filtering

Verify on a test machine the functionality of the `Get-ADGroupMembership` [function](https://github.com/nicolonsky/IntuneDriveMapping/blob/master/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1#L35). If you experience issues override the `$searchRoot` variable with your Active Directory Domain name.

* Ensure that you specified the sAMAccountName without domain name prefix

**If your test machines don't have a value for the PowerShell environment variable `$env:USERDNSDOMAIN` you need to populate the `$searchRoot` variable in the script.**