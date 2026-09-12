# Security Monitoring Roadmap

The identity environment is complete. The next phase will turn it into a controlled SOC-oriented Windows monitoring lab.

## Planned phases

| Phase | Capability | Evidence required before claiming completion |
|---|---|---|
| 1 | Advanced Audit Policy on DC01 | Policy settings plus generated security-event evidence |
| 2 | Centralized collection from DC01 and WIN11-CLIENT | Agent/forwarder configuration and successful log ingestion |
| 3 | Repeatable test cases | Documented tests for failed logons, lockouts, new users, and admin-group changes |
| 4 | Detection and triage | Detection logic, alert evidence, analyst workflow, and tuning notes |
| 5 | Recovery documentation | Snapshot strategy, restore steps, and secure credential handling |

## Candidate telemetry

- Failed and successful logons
- Account creation and account lockouts
- Security-group membership changes
- Privileged-group changes
- Group Policy changes

## Candidate SIEM platforms

Wazuh or Splunk Free are candidates for the monitoring phase. Neither is currently represented as implemented in this repository.

## Portfolio standard

Each completed phase will include:

1. The configuration or detection logic.
2. A controlled test.
3. Evidence of the expected telemetry or alert.
4. A short analyst-facing explanation of how to investigate it.
5. A limitation or tuning note.

This keeps the project accurate and prevents roadmap items from being presented as completed work.
