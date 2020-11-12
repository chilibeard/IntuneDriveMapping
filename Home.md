Welcome to the IntuneDriveMapping wiki! Browse other wiki entries from the right navigation pane or get started with this page.

## Adding network drive mapping entries

**UNC Path** - enter the network path for your file share. Examples:

* `\\ds.tech.nicolonsky.ch\dfsroot\public`

If you want to use environment variables use PowerShell environment variables:
* `\\ds.tech.nicolonsky.ch\dfsroot\homes\$env:username`

**Drive Letter** - select a drive letter where the drive becomes available.

**Display Name** - reflects the name displayed in windows explorer.

**Security Group Filter** - enter the sAMAccountName **without domain prefix** of an on-premises Active Directory group the user needs to be a member of. 

## Migrate Group Policy Preferences

To convert your existing drive mapping group policy configuration, save the GPO as XML report with the group policy management console.

<img src="https://tech.nicolonsky.ch/content/images/2019/07/Export-DriveMapping-GPP.gif">

The import is quite self-explaining. Please do not make changes in the exported XML file. Just upload the previously exported file to the generator.

<img src="https://tech.nicolonsky.ch/content/images/2019/07/Import-DriveMapping-GPP.gif">

## Download the script

If you select the `remove stale drives` option before downloading the script, network drives not specified in the configuration gets disconnected. This is useful if you want to automatically remove stale drives which are no longer required and/or maintained by your configuration.