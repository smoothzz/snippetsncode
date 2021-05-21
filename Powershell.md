### Powershell code snippets

##### GET INFOS FROM USER IN A ESPECIFIC OU
```
### GET INFOS FROM USER IN A ESPECIFIC OU ###
$OU = 'complete path of the OU goes here'
Get-ADUser -Filter * -SearchBase $OU -Properties * | select 'EmployeeId','EmployeeNumber','SamAccountName','Name', 'LastLogonDate', 'PasswordLastSet', 'Modified' | Export-Csv menoresaprendizes.csv -Delimiter ';' -NoTypeInformation -append
```