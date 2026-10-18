# Sysmon

Install (PowerShell as Administrator, from the folder with Sysmon64.exe):

```powershell
.\Sysmon64.exe -accepteula -i sysmon-lab.xml
```

Update config later:

```powershell
.\Sysmon64.exe -c sysmon-lab.xml
```

Download Sysmon from Microsoft Sysinternals.
