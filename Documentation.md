Welcome to the IntuneDriveMapping wiki!

## Architecture

If you deploy the generated PowerShell script (with SYSTEM context) e.g. via Intune or any client management solution the following footprint gets created on your device:

Files:

```
C:/ProgramData/intune-drive-mapping-generator/
┣ DriveMappping.ps1
┗ IntuneDriveMapping-VBSHelper.vbs
```
Scheduled Task:
/IntuneDriveMapping

## Adding network drive mapping entries

`UNC Path` enter the network path for your file share. Examples:

* `\\ds.tech.nicolonsky.ch\dfsroot\public`

If you want to use environment variables use PowerShell environment variables:
* `\\ds.tech.nicolonsky.ch\dfsroot\homes\$env:username`

Drive Letter - enter a character in the range of A-Z without the colon.

Display Name - reflects the name displayed in windows explorer.

Security Group Filter - enter a sam account name of an on-premises Active Directory group the user needs to be a member of.

## Troubleshooting

For troubleshooting get back to the log file which gets stored within the path: `%TEMP%\DriveMapping.log`.

### Security group filtering

Verify on a test machine the functionality of the `Get-ADGroupMembership` [function](https://github.com/nicolonsky/IntuneDriveMapping/blob/master/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1#L35). If you experience issues override the `$searchRoot` variable with your Active Directory Domain name.