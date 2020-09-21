Welcome to the IntuneDriveMapping wiki!

## Adding network drive mapping entries

**UNC Path** - enter the network path for your file share. Examples:

* `\\ds.tech.nicolonsky.ch\dfsroot\public`

If you want to use environment variables use PowerShell environment variables:
* `\\ds.tech.nicolonsky.ch\dfsroot\homes\$env:username`

**Drive Letter** - select a drive letter where the drive becomes available.

**Display Name** - reflects the name displayed in windows explorer.

**Security Group Filter** - enter the sAMAccountName **without domain prefix** of an on-premises Active Directory group the user needs to be a member of. 

## Download the script

If you select the `remove stale drives` option before downloading the script, network drives not specified in the configuration gets disconnected. This is useful if you want to automatically remove stale drives which are no longer required and/or maintained by your configuration.