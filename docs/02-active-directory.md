# 02. Active Directory (DC01 + WS01)

## 1. Prepare the server (PowerShell as Administrator)

```powershell
Rename-Computer -NewName DC01 -Restart
```

After reboot (adjust the interface name with `Get-NetAdapter`):

```powershell
New-NetIPAddress -InterfaceAlias "Ethernet0" -IPAddress 192.168.1.110 -PrefixLength 24 -DefaultGateway 192.168.1.1
Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ServerAddresses 127.0.0.1
```

## 2. Install AD DS and create the domain

```powershell
Install-WindowsFeature AD-Domain-Services -IncludeManagementTools
Install-ADDSForest -DomainName "soclab.local" -DomainNetbiosName "SOCLAB" -InstallDns
```

The server reboots automatically. Log in as `SOCLAB\Administrator`.

## 3. Let the domain resolve internet names

```powershell
Add-DnsServerForwarder -IPAddress 192.168.1.1
```

## 4. Create lab users

```powershell
$pw = Read-Host -AsSecureString "Password"
New-ADUser -Name "John Smith" -SamAccountName jsmith -UserPrincipalName jsmith@soclab.local -AccountPassword $pw -Enabled $true
New-ADUser -Name "Anna Lee" -SamAccountName alee -UserPrincipalName alee@soclab.local -AccountPassword $pw -Enabled $true
```

Use lab-only passwords and never commit them to the repo.

## 5. Join WS01 to the domain

On the Windows 10 VM, set DNS to the DC first:

```powershell
Set-DnsClientServerAddress -InterfaceAlias "Ethernet0" -ServerAddresses 192.168.1.110
Add-Computer -DomainName soclab.local -Credential SOCLAB\Administrator -Restart
```

## 6. Enable useful auditing (GPO)

Group Policy Management -> new GPO linked to the domain -> Computer Configuration -> Windows Settings -> Security Settings -> Advanced Audit Policy Configuration:

- Logon/Logoff: Audit Logon, Audit Logoff (Success, Failure)
- Account Logon: Audit Credential Validation (Success, Failure)
- Detailed Tracking: Audit Process Creation (Success)

Also enable *Include command line in process creation events* under Administrative Templates -> System -> Audit Process Creation.

Screenshots to add: domain created, users list, WS01 joined, GPO settings.
