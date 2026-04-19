# UiBank Field Map

## Status

This field map is intentionally split into confirmed information and unknowns. At the moment, the public sources I checked support the workflow direction, but they do not provide a trustworthy full registration form schema.

## Confirmed Or Strongly Suggested Inputs

| Field | Status | Notes |
| --- | --- | --- |
| Email address | Confirmed and required | Label is `Email Address*`; placeholder is `Enter Email Address`. |
| Password | Confirmed and required | Label is `Password*`; placeholder is `Password`. |
| First name | Confirmed | Label is `First Name`; placeholder is `Enter your first name`. |
| Last name | Confirmed | Label is `Last Name`; placeholder is `Enter your last name`. |
| Middle name | Confirmed | Label is `Middle Name Or Initial`; placeholder is `Enter your middle name or initial`. |
| Sex | Confirmed and required | Label is `Sex*`; options are `male`, `female`. |
| Title | Confirmed and required | Label is `Title*`; options are `ms`, `mrs`, `mr`. |
| Employment status | Confirmed and required | Label is `Employment Status*`; options are `Full-time`, `Part-time`, `Unemployed`. |
| Date of birth | Confirmed | Label is `Date of birth (MM/DD/YY)`; placeholder is `Enter date in MM/DD/YY format`. |
| Marital status | Confirmed and required | Label is `Marital Status*`; options are `Single`, `Married`, `Divorced`, `Widowed`. |
| Number of dependents | Confirmed | Label is `Number of Dependents`; placeholder is `How many dependents do you claim?`. |
| Username | Confirmed and required | Label is `Username*`; placeholder is `Enter your username`. |
| Privacy confirmation checkbox | Confirmed and required for submit | Text begins `I confirm that I agree to the Privacy Policy`; the `Register` button stays disabled until checked. |

## Confirmed Navigation And Action Controls

| Screen | Control | Observed target or behavior |
| --- | --- | --- |
| Welcome | `Sign In` | submits the login form |
| Welcome | `Forgot Your Password?` | routes to `/password-request` |
| Welcome | `Register For Account` | routes to `/register-account` |
| Welcome | `Get Started` | routes to `/register-account` |
| Welcome | `Apply Now` | routes to `/accounts/account-apply` |
| Register | `Register` | submits the registration form |
| Register success | success route | `/register-account/success/:username` |

## Fields Not Observed In The Current Register Chunk

These fields were not visible in the current live registration chunk and should not be assumed without a direct browser walkthrough:

- phone number
- street address
- city
- state
- zip code
- confirm password
- SSN
- verification code entry field

## Confirmed Policy And Consent Clue

The live welcome-page bundle includes a privacy dialog stating that UiBank is for demo purposes and that email is used for official communications and password recovery. That strongly suggests:

- email remains part of the workflow even if username is used for login
- a consent or acknowledgement step may appear before login or registration completes
- password recovery is a supported path in the app

The live registration page reinforces this with a visible notice saying only the email should be real and all other registration data should be dummy data.

## Validation Messages To Capture

- required field errors
- invalid email format
- duplicate account or duplicate email behavior
- password complexity feedback
- submit blocked by missing consent
- expired or missing verification flow
- server-side registration error message shown in an alert dialog

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
- any mismatch between the live rendered UI and the bundle-derived findings

## Sources

- [UiBank Gmail template on UiPath Marketplace](https://marketplace.uipath.com/listings/create-demo-application-account-on-uibank-and-share-credentials-from-gmail)
- [UiBank scan summary on urlscan.io](https://urlscan.io/result/0195ed1f-eb77-730e-9d78-afccfeefcbed/)
