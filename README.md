# ServiceNow Incident – Client Scripts & UI Policy

A ServiceNow micro-project demonstrating client-side controls for the **Incident** table.

## Project Overview

This project implements UI Policy and Client Script controls to improve Incident data quality and enforce conditional business rules.

### Objectives

- Make **Assignment group** mandatory when Impact is High.
- Make **Urgency** read-only when Impact is High.
- Automatically set Urgency to High when Impact changes to High.
- Prevent saving a High Impact Incident when **Assigned To** is empty.
- Prevent direct **State** changes through list editing.
- Verify that the configured behavior reverses correctly when Impact changes from High to Medium.

## Technologies

- ServiceNow
- Incident Management
- UI Policies
- UI Policy Actions
- Client Scripts
- JavaScript
- Form Validation

## Project Structure

```text
servicenow-incident-client-script-ui-policy/
├── README.md
├── ui-policy/
│   └── high-impact-control.md
├── client-scripts/
│   ├── onChange-auto-set-urgency.js
│   ├── onSubmit-prevent-save-if-assigned-to-missing.js
│   └── onCellEdit-prevent-state-list-edit.js
└── tests/
    └── test-cases.md
```

## Configuration

### 1. UI Policy — High Impact Control

**Table:** Incident  
**Active:** true  
**Condition:** Impact is `1 - High`  
**Reverse if false:** true

UI Policy Action:

| Field | Mandatory | Read-only | Visible |
|---|---|---|---|
| Assignment group | Yes | No | Leave as configured |
| Urgency | No | Yes | Leave as configured |

The UI Policy ensures the Assignment group is mandatory for High Impact incidents and reverses the behavior when the condition becomes false.

See [`ui-policy/high-impact-control.md`](ui-policy/high-impact-control.md).

### 2. onChange Client Script — Auto Set Urgency

**Name:** Auto set urgency for high impact  
**Table:** Incident  
**Type:** onChange  
**Field:** Impact  
**Active:** true

When Impact changes to High, the script sets Urgency to High and displays an information message.

Source: [`client-scripts/onChange-auto-set-urgency.js`](client-scripts/onChange-auto-set-urgency.js)

### 3. onSubmit Client Script — Assigned To Validation

**Name:** Prevent save if Assigned To missing  
**Table:** Incident  
**Type:** onSubmit  
**Active:** true

For High Impact incidents, the script prevents submission when Assigned To is empty.

Source: [`client-scripts/onSubmit-prevent-save-if-assigned-to-missing.js`](client-scripts/onSubmit-prevent-save-if-assigned-to-missing.js)

### 4. onCellEdit Client Script — Block State List Editing

**Name:** Prevent state change via list edit  
**Table:** Incident  
**Type:** onCellEdit  
**Field:** State  
**Active:** true

The script blocks direct State changes from the Incident list and asks the user to open the Incident record.

Source: [`client-scripts/onCellEdit-prevent-state-list-edit.js`](client-scripts/onCellEdit-prevent-state-list-edit.js)

## Testing

The test plan covers:

1. High Impact mandatory enforcement.
2. Successful save after Assigned To is populated.
3. Reverse condition when Impact changes from High to Medium.
4. Blocking State changes through list editing.
5. Allowing State changes through the Incident form.

See [`tests/test-cases.md`](tests/test-cases.md).

## How to Use

1. Open a ServiceNow developer/admin instance.
2. Navigate to **System UI → UI Policies**.
3. Create the `High Impact Control` UI Policy on the Incident table.
4. Add the documented UI Policy Actions.
5. Navigate to **System UI → Client Scripts**.
6. Create the three Client Scripts using the JavaScript files in this repository.
7. Execute the test cases in `tests/test-cases.md`.

> These files document the configuration and scripts. They are not a native ServiceNow Update Set export. For deployment between instances, recreate/import the configuration through the appropriate ServiceNow application/update-set workflow.

## Expected Result

The Incident form dynamically responds to Impact changes, required information is validated before submission, and direct list editing of State is blocked.

## Portfolio Note

This project demonstrates practical ServiceNow skills in **Incident Management, UI Policy configuration, Client Scripts, dynamic form behavior, and client-side validation**.
