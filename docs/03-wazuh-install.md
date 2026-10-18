# 03. Wazuh (SIEM) installation

> Always check the official quickstart for the current version and URL: https://documentation.wazuh.com

## Requirements (all-in-one, small lab)

- Ubuntu Server 24.04, static IP 192.168.1.150
- 4 vCPU, 8 GB RAM, 50 GB disk recommended
- Ports: 443 (dashboard), 1514/1515 (agents)

## Install

```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-install.sh
sudo bash ./wazuh-install.sh -a
```

At the end the installer prints the `admin` password. Save it in a password manager, not in the repo.

Dashboard: `https://192.168.1.150`

## Install the agent on Windows (WS01, DC01)

PowerShell as Administrator (use the MSI URL from the Wazuh docs for your version):

```powershell
msiexec.exe /i wazuh-agent.msi /q WAZUH_MANAGER="192.168.1.150" WAZUH_AGENT_NAME="WS01"
NET START WazuhSvc
```

## Install the agent on Linux (LNX01)

Follow "Wazuh agent -> Linux -> DEB amd64" in the docs, set `WAZUH_MANAGER="192.168.1.150"`, then:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now wazuh-agent
```

## Verify

Dashboard -> Agents: all agents should show as *Active*.

## Next

- Sysmon logs: see `configs/sysmon/` and `configs/wazuh/`
- Linux auditing: see `configs/auditd/`

Screenshots to add: dashboard login, agents list, first events in Threat Hunting.
