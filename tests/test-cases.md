# Test Cases

## Test 1 — Mandatory Enforcement

**Setup:** Create a new Incident.

1. Set Impact to High.
2. Leave Assigned To empty.
3. Click Submit.

**Expected:**
- The Incident is not saved.
- An error indicates that Assigned To is mandatory.
- Assignment group is mandatory.
- Urgency is read-only.
- Urgency is automatically set to High.

## Test 2 — Successful Save

1. Set Impact to High.
2. Populate Assigned To.
3. Click Submit.

**Expected:**
- The Incident saves successfully.
- The configured UI Policy and Client Script behavior remains active.

## Test 3 — Reverse Condition

1. Open an Incident with Impact = High.
2. Change Impact to Medium.
3. Review the form.

**Expected:**
- Assignment group is no longer mandatory because the UI Policy condition is false.
- Urgency becomes editable again.
- The record can be saved successfully.

## Test 4 — List Edit Blocking

1. Open Incident → All.
2. Double-click the State field.
3. Attempt to change State.

**Expected:**
- An alert says State cannot be updated using list editing.
- The State value remains unchanged.

## Test 5 — Form-Based State Update

1. Open an Incident record.
2. Change State from the Incident form.
3. Click Update.

**Expected:**
- The State change is saved successfully.
- The list-edit restriction does not prevent normal form-based updates.
