# Detection rules

| Rule | Technique | Source |
|---|---|---|
| 100100 Mimikatz execution | T1003 | wazuh/local_rules.xml |
| 100101 PowerShell encoded command | T1059.001 | wazuh/local_rules.xml, sigma/powershell_encoded_command.yml |

Every rule is tested by running the matching attack from Kali / Atomic Red Team and checking that the alert appears in Wazuh. Add a screenshot of the alert to the matching incident report.
