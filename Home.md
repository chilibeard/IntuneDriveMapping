Welcome to the IntuneDriveMapping wiki!



`UNC Path` enter the network path for your file share. Examples:

* `\\ds.tech.nicolonsky.ch\dfsroot\public`

If you want to use environment variables use PowerShell environment variables:
* `\\ds.tech.nicolonsky.ch\dfsroot\homes\$env:username`

Drive Letter - enter a character in the range of A-Z without the colon.

Display Name - reflects the name displayed in windows explorer.

Security Group Filter - enter a sam account name of an on-premises Active Directory group the user needs to be a member of. Verify on a test machine the functionality of the `Get-ADGroupMembership` [function](https://github.com/nicolonsky/IntuneDriveMapping/blob/master/IntuneDriveMapping/wwwroot/bin/IntuneDriveMappingTemplate.ps1#L35). If you experience issues override the `$searchRoot` variable with your Active Directory Domain name.

![image](https://user-images.githubusercontent.com/32899754/88683436-1750f280-d0f4-11ea-8397-6ac41b894b33.png)