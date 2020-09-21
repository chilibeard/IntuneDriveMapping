The API endpoint `https://intunedrivemapping.azurewebsites.net/api/pstemplate` accepts GET and POST requests.

For POST requests supply a network drive mapping configuration as JSON in the request body and set the content-type to `application/json`.

Example:

```json
[
  {
    "Path": "\\\\test\\li",
    "DriveLetter": "B",
    "Label": "Test",
    "Id": 1,
    "GroupFilter": "TestGroup"
  }
]
```

As a response you will receive the generated PowerShell script to map the network drives.

Calling the API with PowerShell could look like this:

```powershell
$requestBody = '[{"Path":"\\\\test\\li","DriveLetter":"B","Label":"Test","Id":1,"GroupFilter":"TestGroup"}]'
$requestUri = 'https://intunedrivemapping.azurewebsites.net/api/pstemplate'
Invoke-RestMethod -Uri $requestUri -Method Post -Body $requestBody -ContentType "application/json"
```