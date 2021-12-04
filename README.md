# SecureStack GitHub Actions

A GitHub Action to execute SecureStack secrets analysis on an application code repository.

```
name: Example Workflow Using SecureStack Actions
on: push
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo for running secrets analysis within workflow
        id: checkout
        uses: actions/checkout@v2.4.0
        with:
          fetch-depth: 0
      - name: Secrets Analysis Step
        id: secrets
        uses: SecureStackCo/actions/secrets@main
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY_SECRET }}
          securestack_app_id: '<Application Id>'
          severity: critical
          flags: '-d 50'
```
NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli code --help`

## Getting your SecureStack API Key

1. Log in to [SecureStack](https://app.securestack.com) and go to the Profile -> GENERATE KEY screen.
2. Generate an API key and copy the value.
3. Paste into the value of a secret called SECURESTACK_API_KEY_SECRET in the GitHub repo settings.

## Getting your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.
3. Copy the value of the application id on the View Application screen.
4. Paste into the value of the `securestack_app_id` action input for the step using the SecureStack action in your workflow.


Made with 💜 by SecureStack
