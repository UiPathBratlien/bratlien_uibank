# Project Checklist

## Setup

- [x] Create public GitHub repository
- [x] Clone repository locally
- [ ] Add any project-specific tooling notes as they emerge

## UiBank Automation

- [ ] Define the exact registration scenario to automate
- [ ] Identify required inputs and expected outputs
- [ ] Create the initial UiPath workflow project in `workflows/`
- [ ] Implement the happy-path registration flow
- [ ] Add basic error handling and retries
- [ ] Test the workflow end to end

## Site Understanding

- [ ] Document the registration page flow in `research/`
- [ ] Capture important field names, labels, and validation rules
- [ ] Note timing issues, popups, redirects, or dynamic behavior
- [ ] Record assumptions the automation depends on

## Codex And Agent Support

- [ ] Decide whether `agent.md` or other reference files belong in this repo
- [ ] Add prompt/reference material under `references/` if needed
- [ ] Refactor supporting docs when they become too large or repetitive

## Validation

- [x] Confirm GitHub push, pull, and PR flow works
- [ ] Add a short implementation log or demo notes before final submission
