# SecureStack Secrets Analysis GitHub Action

A GitHub Action that analyses your source code for secrets, credentials, API keys, server and database hostnames/URLS, and a lot more!  When you add this to GitHub Actions we will analyze your source code to make sure there is no sensitive data in your commit. See below for the specific types of credentials and files we scan for.

```
name: Example SecureStack Secrets Analysis GitHub Action
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
        uses: SecureStackCo/actions-secrets@v0.1.3
        with:
          securestack_api_key: ${{ secrets.SECURESTACK_API_KEY }}
          securestack_app_id: ${{ secrets.SECURESTACK_APP_ID }}
          severity: critical
          flags: '-d 1'

```
NOTE - to understand possible values for the action input `flags`, run the SecureStack cli locally:

`$ bloodhound-cli code --help`

## Create your SecureStack API Key as GitHub Secret

1. Create a [SecureStack](https://app.securestack.com) account using your GitHub credentials.  You get 20 scans for free and you don't need to add a credit card.
2. Once you are logged in go to "Settings" in the black drawer on the left, and then -> API tab.
4. Generate an API key and copy the value.
5. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
6. Create a new secret named SECURESTACK_API_KEY and paste the value from step 2 into the field.

## Retreiving your SecureStack Application ID

1. Log in to [SecureStack](https://app.securestack.com).
2. Open the application you wish to analyse.  If you haven't created a managed application you can follow the directions in this [VIDEO](https://youtu.be/mapgawLMVKg) to create one.  
3. Copy the value of the application id on the View Application screen.
4. Go to Settings for your GitHub repository and click on Secrets -> Actions at the bottom left.
5. Create a new secret named SECURESTACK_APP_ID and paste the value from step 3 into the field.

## What types of credentials does this GitHub Action find?
1. API keys like Stripe, AWS, Amplitude and a bazillion more
2. Server and database hostnames or URLS
3. Passwords and Usernames
4. .env files and git indexes

## Watch this video to learn how to setup your first GitHub Action with SecureStack
[![IMAGE ALT TEXT](http://img.youtube.com/vi/0sYXsCmY2es/0.jpg)](http://www.youtube.com/watch?v=0sYXsCmY2es "Video Title")

## Check out our other GitHub Actions:
1. [SecureStack Software Composition Analysis (SCA)](https://github.com/marketplace/actions/securestack-application-composition-analysis) - Scan your application for vulnerable third-party and open source libraries.
2. [SecureStack Web Vulnerability & Cloud Misconfiguration Analysis](https://github.com/marketplace/actions/securestack-web-vulnerability-analysis) - Scan your running application url for cloud misconfigurations and web vulnerabilities.
3. [SecureStack Log4j Analysis](https://github.com/marketplace/actions/securestack-log4j-vulnerability-analysis) - Scan your application for Log4j/Log4Shell vulnerabilities.

## Learn more about SecureStack with our YouTube Channel:
https://www.youtube.com/watch?v=YrPITQNy9UM&list=PL_8Xjyi5rInxzhpQkDRipipmaj0lT6pJ8 

Made with 💜  by [SecureStack](https://securestack.com)
