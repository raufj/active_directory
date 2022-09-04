# AD Setup 

Get-item wsman:\localhost\Client\TrustedHosts 

set-item wsman:\localhost\Client\TrustedHosts -value <IP DC>


New-PSSession -ComputerName <IP DC> -Credential (Get-Credential)

Enter-PSSession <id> 

ipconfig /all 

sconfig

Install-WindowsFeature AD-Domain-Services -IncludeManagementTools 
