# UiBank Registration Flow

## Purpose

This note captures the current understanding of the UiBank registration workflow so the automation can be built against observed behavior instead of assumptions.

## Confirmed Facts

- UiBank is available at `https://uibank.uipath.com/`.
- A scanned entry point for the site is `https://uibank.uipath.com/welcome`.
- The scanned page title for that entry point was `UiBank-Welcome`.
- The live welcome page bundle currently exposes a login form with `Username` and `Password` fields and a `Sign In` button.
- The live welcome page bundle links `Forgot Your Password?` to `/password-request`.
- The live welcome page bundle links `Register For Account` to `/register-account`.
- The live welcome page bundle also exposes a `Get Started` call to action that routes to `/register-account`.
- The live welcome page bundle exposes an `Apply Now` path to `/accounts/account-apply`.
- The live welcome page bundle includes a privacy-policy dialog that says UiBank is for demo purposes and that email is used for official communications and password recovery.
- The live registration route is `/register-account`.
- The live registration route submits new users to `https://uibank-api.azurewebsites.net/api/users/`.
- After successful registration, the app attempts an automatic login with the new `username` and `password`.
- After successful registration, the app navigates to `/register-account/success/:username`.
- The live success screen says `Welcome To The UiBank Family!`.
- The live success screen instructs the user to verify email before applying for an account.
- The live success screen says `Check your inbox for a verification link.`
- UiPath Marketplace includes automation templates described as creating a UiBank account based on an email address and then sending login details to the provided email address.
- A UiPath employee described UiBank in the community forum as a free environment for learners to experiment with UiPath Test Suite.

## Working Assumption For This Project

The first automation target should be the happy-path user registration flow for a new UiBank account, with a likely focus on supplying an email address, completing the registration, and validating that account credentials or next-step instructions are delivered successfully.

This is an inference from public UiPath Marketplace descriptions and should be validated directly against the live site before implementation is treated as final.

## Proposed Happy-Path Flow

1. Open the UiBank welcome page.
2. Navigate to `/register-account` using `Register For Account` or `Get Started`.
3. Enter registration details, including the required profile fields.
4. Check the privacy-policy confirmation checkbox.
5. Click `Register`.
6. On success, let the app create the user and attempt its automatic login.
7. Confirm redirect to `/register-account/success/:username`.
8. Confirm the success message and the instruction to verify email from the inbox before applying for an account.

## Known Risks And Caveats

- Historical forum posts suggest account cleanup and reset options may be limited.
- Historical forum posts also suggest the site has had maintenance issues before, including verification-related problems.
- Because UiBank is a demo environment, behavior may be inconsistent over time.
- If the registration creates persistent accounts, test data should be planned carefully to avoid cluttering the environment.
- The live registration screen explicitly says only the email should be real and all other registration data should be dummy data.

## What To Verify Manually

- exact registration entry point
- required fields
- optional fields
- validation rules
- whether email verification is mandatory
- what success looks like on-screen
- whether the system emails credentials, a verification link, or both
- whether policy consent or popups block submission

## Automation Notes

- Prefer stable text anchors over brittle visual positions.
- Capture success criteria explicitly, such as a success banner, redirect, inbox email, or visible account identifier.
- Add guardrails for duplicate-account attempts and validation errors.
- If email verification is part of the flow, separate the web registration step from inbox verification so the workflow can be tested in parts.
- Treat the privacy checkbox as mandatory because the `Register` button is disabled until it is checked.

## Suggested Next Evidence To Capture

1. A direct manual walkthrough of registration.
2. Screenshots or notes for each step.
3. Validation messages from at least one invalid submission.
4. A sample successful outcome and one intentional failure case.
5. Confirmation of what arrives in email after registration.

## Sources

- [UiBank Gmail template on UiPath Marketplace](https://marketplace.uipath.com/listings/create-demo-application-account-on-uibank-and-share-credentials-from-gmail)
- [UiBank scan summary on urlscan.io](https://urlscan.io/result/0195ed1f-eb77-730e-9d78-afccfeefcbed/)
- [UiPath Community Forum discussion about UiBank](https://forum.uipath.com/t/uipath-breaking-gdpr-uibank/496021)
