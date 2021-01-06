If you want to add additional triggers replace the logon only trigger from this [line](https://github.com/nicolonsky/IntuneDriveMapping/blob/c6c33436eedf590da0643253f496e04e6452eaf7/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1#L260) with the following content:

```powershell
$trigger = New-ScheduledTaskTrigger -AtLogOn

$class = cimclass MSFT_TaskEventTrigger root/Microsoft/Windows/TaskScheduler
$trigger2 = $class | New-CimInstance -ClientOnly
$trigger2.Enabled = $True
$trigger2.Subscription = '<QueryList><Query Id="0" Path="Microsoft-Windows-NetworkProfile/Operational"><Select Path="Microsoft-Windows-NetworkProfile/Operational">*[System[Provider[@Name=''Microsoft-Windows-NetworkProfile''] and EventID=10002]]</Select></Query></QueryList>'

$trigger3 = $class | New-CimInstance -ClientOnly
$trigger3.Enabled = $True
$trigger3.Subscription = '<QueryList><Query Id="0" Path="Microsoft-Windows-NetworkProfile/Operational"><Select Path="Microsoft-Windows-NetworkProfile/Operational">*[System[Provider[@Name=''Microsoft-Windows-NetworkProfile''] and EventID=4004]]</Select></Query></QueryList>'
```

And adjust the [registration](https://github.com/nicolonsky/IntuneDriveMapping/blob/c6c33436eedf590da0643253f496e04e6452eaf7/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1#L267) of the scheduled task with the newly definded triggers:

```powershell
$null=Register-ScheduledTask -TaskName $schtaskName -Trigger $trigger,$trigger2,$trigger3 -Action $action  -Principal $principal -Settings $settings -Description $schtaskDescription -Force
```