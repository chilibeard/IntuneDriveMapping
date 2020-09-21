## Web app

The web app allows configuration of the network drives you want to map. The "Download PowerShell script" button serializes your configuration to JSON format and adds the configuration to a [PowerShell template](https://github.com/nicolonsky/IntuneDriveMapping/blob/master/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1) which is returned as a file download.

## Client-side processing

If you deploy the generated PowerShell script (with SYSTEM context) e.g. via Intune or any client management solution the following footprint gets created on your device:

Files:

```
C:/ProgramData/intune-drive-mapping-generator/
┣ DriveMappping.ps1
┗ IntuneDriveMapping-VBSHelper.vbs
```
Scheduled task:

`/IntuneDriveMapping`

The scheduled task gets triggered on each logon and will invoke the `IntuneDriveMapping-VBSHelper.vbs` script (to suppress the PowerShell windows from appearing) which invokes the `DriveMappping.ps1` PowerShell script.