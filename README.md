# powershell_cmds

## Change all file names to lower case in the current directory
Get-ChildItem | Rename-Item -NewName {$_.Name -replace $_.Name, $_.Name.ToLower()}
