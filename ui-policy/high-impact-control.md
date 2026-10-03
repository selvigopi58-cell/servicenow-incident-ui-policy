# UI Policy: High Impact Control

## Basic Configuration

- **Name:** High Impact Control
- **Table:** Incident
- **Active:** true
- **Condition:** Impact | is | 1 - High
- **Reverse if false:** true

## UI Policy Action 1 — Assignment group

- **Field:** Assignment group
- **Mandatory:** true
- **Read-only:** Leave unchanged
- **Visible:** Leave unchanged

This makes Assignment group mandatory when Impact is High.

## UI Policy Action 2 — Urgency

- **Field:** Urgency
- **Read-only:** true
- **Visible:** Leave unchanged
- **Mandatory:** Leave unchanged

This makes Urgency read-only while Impact is High.

## Expected Behavior

When Impact is changed away from High, the policy reverses its conditional changes because **Reverse if false** is enabled.
