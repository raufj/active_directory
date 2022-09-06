# AD Setup 

This walkthrough is the steps followed on John Hammond Youtube Active Directory Series and the personal notes on the steps are detailed as below. 

Machine setups : 
1. Windows Server 2022 as Domain Controller 
2. Windows 11 as workstation node 

All machine setups performed in VMWare Workstation. First part of the video are basically configuring the machine. Windows 11 iso having issues on installation due due to Trusted Platform Module (TPM) settings. The bypass techniques by setting registry keys are listed here : https://www.tomshardware.com/how-to/bypass-windows-11-tpm-requirement

Next steps in configuring the remote session in between the machine. Steps as below : 
    - Enable the PS remote onm DC server using this command : Enable-PSRemoting
    - Add the DC IP in the Workstation Trusted Host : set-item wsman:\localhost\Client\TrustedHosts -value <IP DC>
    - Test the connection in Workstation : New-PSSession -ComputerName <IP DC> -Credential (Get-Credential), you will be prompted GUI to enter credentials of DC server. Then run Enter-PSSession <id prompted on the previous commands> 

Step #1 : Domain Controller installation 

1. Use 'sconfig' to: 
    - Config hostname 
    - Config static IP Address 
    - Config DNS server pointed to our IP address

2. Active Directory Windows Feature Installation 

 ```shell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools 
```

3. Setting the DNS on DC and Workstation 

Check the IP setup
```shell 
Get-NetIPAddress
```

Set the DNS 
```shell 
Set-DNSClientServerAddress -InterfaceIndex <index interface of your IP> -ServerAddress <DC IP>
```


Command to join Workstation to DC (run in Workstation)
```shell 
Add-Computer -Domainname rjz.com -Credential rjz\Administrator -Force Restart
```