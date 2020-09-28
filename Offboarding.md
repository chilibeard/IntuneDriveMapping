If you want to offboard the solution you can replace your `DriveMapping.ps1` script in Intune with the following content:

```powershell
# Remove scripts
$scriptSavePath = $(Join-Path -Path $env:ProgramData -ChildPath "intune-drive-mapping-generator")
Remove-Item -Path $scriptSavePath -Recurse -Force

# Remove scheduled task
$schtaskName = "IntuneDriveMapping"
Unregister-ScheduledTask -TaskName $schtaskName -Confirm:$false
```

Note that the offboarding script won't delete the mapped network drives, deleting mapped network drives needs to happen under the signed-in user's context. If you want to do this, create an additional script with the following content and deploy it with the "Run this script using the logged on credentials" option:

```powershell
#Remove all locally connected network drives
$psDrives = Get-PSDrive | Where-Object { $_.Provider.Name -eq "FileSystem" -and $_.Root -notin @("$env:SystemDrive\", "D:\") }
foreach ($drive in $psDrives) {
    Remove-SmbMapping -LocalPath "$($drive.Name):" -Force -UpdateProfile
}
```



