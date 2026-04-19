# UiBank Registration Workflow

This folder is a UiPath process scaffold for the live UiBank registration flow documented in `research/uibank-registration-flow.md` and `research/field-map.md`.

Use `MAIN-WIRING.md` for the recommended argument schema and orchestration pattern for `Main.xaml`.

## Intended Workflow Breakdown

- `Main.xaml` orchestrates the end-to-end path
- `Workflows/OpenWelcomePage.xaml` opens UiBank and navigates to registration
- `Workflows/RegisterNewUser.xaml` fills and submits the register form
- `Workflows/VerifyRegistrationSuccess.xaml` confirms the success page and route
- `Workflows/VerifyRegistrationEmail.xaml` verifies the inbox follow-up step

## Live Registration Facts This Scaffold Assumes

- registration route: `/register-account`
- success route: `/register-account/success/:username`
- register button disabled until privacy checkbox is checked
- email should be real; other profile data can be dummy data

## Confirmed Required Inputs

- `email`
- `password`
- `gender`
- `title`
- `employmentStatus`
- `maritalStatus`
- `username`
- privacy consent checkbox

## Suggested First Implementation Order

1. Build browser open and navigation in `OpenWelcomePage.xaml`
2. Build field entry and checkbox handling in `RegisterNewUser.xaml`
3. Verify redirect and visible success copy in `VerifyRegistrationSuccess.xaml`
4. Add email-inbox verification in `VerifyRegistrationEmail.xaml`

## Test Data

Use `Data/registration-sample.json` as a starter shape only. Replace the email and password with safe test values before execution.
