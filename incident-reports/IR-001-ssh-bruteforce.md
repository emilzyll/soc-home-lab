# IR-001: SSH brute force against LNX01

> Draft skeleton. Fill in after running the exercise.

## Plan

1. From KALI run a brute force against LNX01 (e.g. with Hydra and a small lab wordlist, lab VMs only)
2. Confirm failed-login events reach Wazuh from `/var/log/auth.log`
3. Check which built-in Wazuh rule fires (SSH brute force rules, MITRE T1110)
4. Document the alert, timeline and response using `TEMPLATE.md`
