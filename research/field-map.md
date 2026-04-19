# UiBank Field Map

## Status

This field map is intentionally split into confirmed information and unknowns. At the moment, the public sources I checked support the workflow direction, but they do not provide a trustworthy full registration form schema.

## Confirmed Or Strongly Suggested Inputs

| Field | Status | Notes |
| --- | --- | --- |
| Email address | Likely required | UiPath Marketplace descriptions for UiBank account creation say the account is created based on an email address and that login details are sent to that address. |
| Username | Confirmed on welcome/login page | The live welcome-page bundle exposes a `Username` field for sign-in. This confirms login uses a username field, but not yet whether registration also asks for a separate username. |
| Password | Confirmed on welcome/login page | The live welcome-page bundle exposes a `Password` field for sign-in. This does not yet confirm whether new-user registration sets a password directly or relies on an emailed credential flow. |

## Confirmed Navigation And Action Controls

| Screen | Control | Observed target or behavior |
| --- | --- | --- |
| Welcome | `Sign In` | submits the login form |
| Welcome | `Forgot Your Password?` | routes to `/password-request` |
| Welcome | `Register For Account` | routes to `/register-account` |
| Welcome | `Get Started` | routes to `/register-account` |
| Welcome | `Apply Now` | routes to `/accounts/account-apply` |

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

## Confirmed Policy And Consent Clue

The live welcome-page bundle includes a privacy dialog stating that UiBank is for demo purposes and that email is used for official communications and password recovery. That strongly suggests:

- email remains part of the workflow even if username is used for login
- a consent or acknowledgement step may appear before login or registration completes
- password recovery is a supported path in the app

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
