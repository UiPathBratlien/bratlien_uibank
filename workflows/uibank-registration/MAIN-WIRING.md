# Main.xaml Wiring Spec

This file defines the input schema, variable names, and invocation pattern for `Main.xaml` so the UiBank registration workflows connect cleanly.

## Design Goal

`Main.xaml` should act as the orchestrator for the end-to-end registration path:

1. open UiBank and navigate to registration
2. register a new user
3. verify the success page
4. verify the follow-up email

## Naming Standard

Use these prefixes consistently:

- `in_` for input arguments
- `out_` for output arguments
- `io_` only if a workflow truly needs in/out behavior
- `var_` for local variables
- `const_` for local constants

Prefer PascalCase after the prefix.

Examples:

- `in_Email`
- `in_BaseUrl`
- `var_RegistrationSucceeded`
- `const_RegisterRoute`

## Main.xaml Arguments

Create these `In` arguments on `Main.xaml`:

| Argument | Type | Purpose |
| --- | --- | --- |
| `in_BaseUrl` | `String` | UiBank entry page, default `https://uibank.uipath.com/welcome` |
| `in_Email` | `String` | Real email used for verification |
| `in_Password` | `String` | Password for UiBank registration |
| `in_FirstName` | `String` | Dummy profile data |
| `in_LastName` | `String` | Dummy profile data |
| `in_MiddleName` | `String` | Dummy profile data |
| `in_Gender` | `String` | `male` or `female` |
| `in_Title` | `String` | `ms`, `mrs`, or `mr` |
| `in_EmploymentStatus` | `String` | `Full-time`, `Part-time`, or `Unemployed` |
| `in_DateOfBirth` | `String` | Format `MM/DD/YY` |
| `in_MaritalStatus` | `String` | `Single`, `Married`, `Divorced`, or `Widowed` |
| `in_NumberOfDependents` | `Int32` | Number of dependents |
| `in_Username` | `String` | UiBank username |
| `in_ExpectedSuccessRouteFragment` | `String` | Default `/register-account/success` |
| `in_ExpectedSuccessHeader` | `String` | Default `Welcome To The UiBank Family!` |
| `in_EmailSubjectHint` | `String` | Optional hint for the verification email search |

## Suggested Defaults

- `in_BaseUrl` = `https://uibank.uipath.com/welcome`
- `in_ExpectedSuccessRouteFragment` = `/register-account/success`
- `in_ExpectedSuccessHeader` = `Welcome To The UiBank Family!`
- `in_EmailSubjectHint` = `UiBank`

## Main.xaml Local Variables

Create these local variables:

| Variable | Type | Purpose |
| --- | --- | --- |
| `const_RegisterRoute` | `String` | `/register-account` |
| `var_RegistrationSucceeded` | `Boolean` | Tracks whether registration reached success |
| `var_SuccessPageVerified` | `Boolean` | Tracks success-page verification |
| `var_EmailVerified` | `Boolean` | Tracks inbox verification result |
| `var_RunNotes` | `String` | Optional log or summary text |

## Invocation Order

Invoke workflows in this order:

1. `Workflows/OpenWelcomePage.xaml`
2. `Workflows/RegisterNewUser.xaml`
3. `Workflows/VerifyRegistrationSuccess.xaml`
4. `Workflows/VerifyRegistrationEmail.xaml`

## Argument Mapping

### 1. OpenWelcomePage.xaml

Pass:

- `in_BaseUrl` -> `in_BaseUrl`

### 2. RegisterNewUser.xaml

Pass:

- `in_Email` -> `in_Email`
- `in_Password` -> `in_Password`
- `in_FirstName` -> `in_FirstName`
- `in_LastName` -> `in_LastName`
- `in_MiddleName` -> `in_MiddleName`
- `in_Gender` -> `in_Gender`
- `in_Title` -> `in_Title`
- `in_EmploymentStatus` -> `in_EmploymentStatus`
- `in_DateOfBirth` -> `in_DateOfBirth`
- `in_MaritalStatus` -> `in_MaritalStatus`
- `in_NumberOfDependents` -> `in_NumberOfDependents`
- `in_Username` -> `in_Username`

### 3. VerifyRegistrationSuccess.xaml

Pass:

- `in_ExpectedRouteFragment` -> `in_ExpectedSuccessRouteFragment`
- `in_ExpectedHeader` -> `in_ExpectedSuccessHeader`

### 4. VerifyRegistrationEmail.xaml

Suggested pass-through arguments when you implement that workflow:

- `in_Email` -> `in_Email`
- `in_EmailSubjectHint` -> `in_EmailSubjectHint`
- `in_Username` -> `in_Username`

## Recommended Main.xaml Flow

Use a top-level `Sequence` with this shape:

1. `Assign`
   Set `const_RegisterRoute = "/register-account"`
2. `Invoke Workflow File`
   `OpenWelcomePage.xaml`
3. `Invoke Workflow File`
   `RegisterNewUser.xaml`
4. `Invoke Workflow File`
   `VerifyRegistrationSuccess.xaml`
5. `Assign`
   Set `var_RegistrationSucceeded = True`
6. `Invoke Workflow File`
   `VerifyRegistrationEmail.xaml`
7. `Assign`
   Set `var_EmailVerified = True`

Wrap the core path in `Try Catch` if you want one place to handle screenshots, logging, and fail-fast behavior.

## Validation Rules

Before invoking the registration workflow, validate:

- `in_Email` is not empty
- `in_Password` is not empty
- `in_Username` is not empty
- `in_Gender` is one of the allowed values
- `in_Title` is one of the allowed values
- `in_EmploymentStatus` is one of the allowed values
- `in_MaritalStatus` is one of the allowed values

If any required input is invalid, fail early with a clear message.

## Logging Guidance

Log only safe values. Avoid logging:

- passwords
- full private credentials
- anything marked private in Studio

Safe examples:

- base URL
- target route
- username
- success-route confirmation
- email verification status

## Best Next Implementation Step

After wiring `Main.xaml`, implement the workflows in this order:

1. `OpenWelcomePage.xaml`
2. `RegisterNewUser.xaml`
3. `VerifyRegistrationSuccess.xaml`
4. `VerifyRegistrationEmail.xaml`
