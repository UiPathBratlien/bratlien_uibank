# UiBank Field Map

## Status

This field map is intentionally split into confirmed information and unknowns. At the moment, the public sources I checked support the workflow direction, but they do not provide a trustworthy full registration form schema.

## Confirmed Or Strongly Suggested Inputs

| Field | Status | Notes |
| --- | --- | --- |
| Email address | Likely required | UiPath Marketplace descriptions for UiBank account creation say the account is created based on an email address and that login details are sent to that address. |

## Unknown Inputs To Capture From The Live Site

| Field | Why It Matters | What To Record |
| --- | --- | --- |
| First name | Common registration input | label text, required or optional, validation |
| Last name | Common registration input | label text, required or optional, validation |
| Username | May be distinct from email | allowed characters, uniqueness behavior |
| Password | Needed for robust automation if user-set | complexity rules, masking, confirm-password behavior |
| Confirm password | Common paired field | mismatch validation |
| Phone number | Possible contact field | format and validation |
| Address fields | May appear in banking-style demo forms | line breakdown and requiredness |
| Consent checkbox | Often blocks submit | exact text and default state |
| Verification code or email link | May be part of completion | inbox dependency and timeout expectations |

## Validation Messages To Capture

- required field errors
- invalid email format
- duplicate account or duplicate email behavior
- password complexity feedback
- submit blocked by missing consent
- expired or missing verification flow

## Selector And Automation Notes

- Prefer labels, placeholders, `aria` text, or stable button text over layout-based targeting.
- Record whether fields are standard HTML inputs, custom controls, or iframe-hosted elements.
- Note whether errors appear inline, in toast messages, or after submit.
- Record whether the submit button text changes across steps.

## Suggested Capture Template

Use this format as you inspect each field on the live site:

| Screen | Field label | Control type | Required | Example value | Validation | Automation notes |
| --- | --- | --- | --- | --- | --- | --- |
| Registration |  |  |  |  |  |  |

## Completion Criteria

This file is ready for automation use once it includes:

- every required field
- every step-level button
- every blocking validation rule
- the success condition for registration
- any inbox or verification dependency

## Sources

- [UiBank Gmail template on UiPath Marketplace](https://marketplace.uipath.com/listings/create-demo-application-account-on-uibank-and-share-credentials-from-gmail)
- [UiBank scan summary on urlscan.io](https://urlscan.io/result/0195ed1f-eb77-730e-9d78-afccfeefcbed/)
