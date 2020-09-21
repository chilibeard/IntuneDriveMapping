If you want to offboard the solution you can replace your `DriveMapping.ps1` script in Intune with the following content:

```powershell
# Remove scripts
$scriptSavePath = $(Join-Path -Path $env:ProgramData -ChildPath "intune-drive-mapping-generator")
Remove-Item -Path $scriptSavePath -Recurse -Force

# Remove scheduled task
$schtaskName = "IntuneDriveMapping"
Unregister-ScheduledTask -TaskName $schtaskName -Confirm:$false
```
Note that the offboarding script won't delete the mapped network drives.