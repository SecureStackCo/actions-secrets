# SecureStack GitHub Actions

A GitHub Action that analyses your source code for secrets, credentials, API keys, server and database hostnames/URLS, and a lot more!  When you add this to GitHub Actions we will analyze your source code to make sure there is no sensitive data in your commit. See below for the specific types of credentials and files we scan for.

```
name: Example Workflow Using SecureStack Secrets Scan Action
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
        uses: SecureStackCo/actions-secrets@v0.1.0
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY_SECRET }}
          securestack_app_id: '<Application Id>'
          severity: critical
          flags: '-d 50'
```
NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli code --help`

## Create your SecureStack API Key and save as GitHub Secret

1. Log in to [SecureStack](https://app.securestack.com) and go to the Profile -> GENERATE KEY screen.
2. Generate an API key and copy the value.
3. Go to Settings for your GitHub repository and click on Secrets at the bottom left.
4. Create a new secret named SECURESTACK_API_KEY_SECRET and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.
3. Copy the value of the application id on the View Application screen.
4. Paste into the value of the `securestack_app_id` action input for the step using the SecureStack action in your workflow.

## What types of credentials does this GitHub Action find?
1. API keys like Stripe, AWS, Amplitude and a bazillion more
2. Server and database hostnames or URLS
3. Passwords and Usernames
4. .env files and git indexes

Made with 💜  by [SecureStack](https://securestack.com)
