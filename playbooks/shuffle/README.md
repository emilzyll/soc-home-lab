# SOAR playbook: alert enrichment

## Flow

1. **Trigger:** Wazuh sends alerts (level >= 10) to a Shuffle webhook (see `configs/wazuh/manager-shuffle-integration.xml`)
2. **Extract:** pull the source IP and rule description from the alert JSON
3. **Enrich:** query AbuseIPDB / VirusTotal for the source IP
4. **Decide:** if the reputation score is above the threshold, mark as high priority
5. **Notify / ticket:** send an email or create a ticket with alert details and enrichment result

## Setup notes

- Shuffle runs in Docker on the SOAR VM (see the Shuffle docs for the install steps)
- API keys go into Shuffle's secret storage, never into the repo
- Export the finished workflow as JSON and save it here as `enrich-and-notify.json` (remove secrets first)

Screenshots to add: workflow canvas, webhook execution, enrichment result.
