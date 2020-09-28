If you want to offboard the solution you can replace your `DriveMapping.ps1` script in Intune with the following content:

![image](https://user-images.githubusercontent.com/32899754/94411711-2c401580-0179-11eb-9e26-49501af32b7d.png)


```powershell
# Remove scripts
$scriptSavePath = $(Join-Path -Path $env:ProgramData -ChildPath "intune-drive-mapping-generator")
Remove-Item -Path $scriptSavePath -Recurse -Force

# Remove scheduled task
$schtaskName = "IntuneDriveMapping"
Unregister-ScheduledTask -TaskName $schtaskName -Confirm:$false
```

Note that the offboarding script won't delete the mapped network drives, deleting mapped network drives needs to happen under the signed-in user's context. If you want to do this, create an additional script with the following content and deploy it with the "Run this script using the logged on credentials" option:

![image](https://user-images.githubusercontent.com/32899754/94411583-09156600-0179-11eb-8787-70cab8825a99.png)

```powershell
#Remove all locally connected network drives
$psDrives = Get-PSDrive | Where-Object { $_.Provider.Name -eq "FileSystem" -and $_.Root -notin @("$env:SystemDrive\", "D:\") }
foreach ($drive in $psDrives) {
    Remove-SmbMapping -LocalPath "$($drive.Name):" -Force -UpdateProfile
}
```



