# opschain-github-action 

This GitHub action can be used to initiate an OpsChain change.

## Setup

On your GitHub Repository or Organisation, add the following secrets:

OPSCHAIN_URL - The URL with which to access OpsChain
OPSCHAIN_USERNAME - The user with which to authenticate to OpsChain
OPSCHAIN_PASSWORD - The user credential with which to authenticate to OpsChain
OPSCHAIN_GITHUB_USERNAME - The GitHub User with which OpsChain should authenticate to GitHub
OPSCHAIN_GITHUB_PAT - The GitHub PAT with which OpsChain should authenticate to GitHub

## Usage

Add a new job in your GitHub Workflow

```yaml
jobs:

  verify-opschain:
    name: Verify OpsChain GitHub Action
    if: ${{ github.ref == 'refs/heads/main' }}
    timeout-minutes: 60
    environment:
      name: dev
    concurrency:
      group: ${{ github.workflow }}-dev
      cancel-in-progress: false
    steps:
      - name: Deploy
        uses: limepoint/opschain-github-action@v3
        with:
          opschain_apiBaseUrl: "https://opschain.limepoint.dev"
          opschain_username: ${{ secrets.OPSCHAIN_USERNAME }}
          opschain_password: ${{ secrets.OPSCHAIN_PASSWORD }}
          opschain_project: "demo"
          opschain_environment: "dev"
          opschain_git_remote: "origin"
          opschain_git_username: ${{ secrets.OPSCHAIN_GITHUB_USERNAME }}
          opschain_git_password: ${{ secrets.OPSCHAIN_GITHUB_PAT }}
          opschain_action: "demo:application:deploy"
```

The following arguments are supported for this action:

- `opschain_apiBaseUrl`: OpsChain API Base URL, required: true
- `opschain_username`: OpsChain username, required: true
- `opschain_password`: OpsChain password, required: true
- `opschain_project`: Project code for the change, default: auto-generated using GITHUB_REPOSITORY and GITHUB_REPOSITORY_OWNER variables, required: true
- `opschain_environment`: Environment code for the change, required: true
- `opschain_action`: The action to perform during this change, required: true
- `opschain_requestTimeout`: opschain request timeout, default: '60000', required: false
- `opschain_action_metadata`: The metadata to store along with this change, default: '', required: true
- `opschain_git_remote`: Git Remote name to use on the OpsChain Project, default: 'origin', required: true
- `opschain_git_rev`: The Git revision (branch/tag/commit) for the change, default: ${GITHUB_SHA}, required: true
- `opschain_github_username`: The GitHub Username with which to authenticate, required: true
- `opschain_github_pat`: The GitHub Privileged Access Token with which to authenticate, required: true

# Licence & authors

- Author:: LimePoint (support@limepoint.com)

See [LICENCE](LICENCE)
