# RASSED
# Dynamic Scan Action

Reusable GitHub Action for validating credentials and running dynamic security scans via an orchestrator API.

## Usage

you can use it in any workflow like this:

```yaml
        You can use this action in three ways or more:

        ### 1. Using GitHub Secrets (Recommended)

        ```yaml
        jobs:
          scan:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout code
                uses: actions/checkout@v4
              - name: Run Dynamic Scan Action
                uses: mfldosari/RASSED@v1.0.0
                with:
                  HOST: ${{ secrets.HOST }}
                  ACCESS_TOKEN: ${{ secrets.ACCESS_TOKEN }}
                  action_type: ${{ secrets.ACTION_TYPE }}
                  mock_mode: ${{ secrets.MOCK_MODE }}
                  tracker_type: ${{ secrets.TRACKER_TYPE }}
                  server_url: ${{ secrets.SERVER_URL }}
                  username: ${{ secrets.ISSUE_TRACKER_USERNAME }}
                  password: ${{ secrets.ISSUE_TRACKER_PASSWORD }}
                  project_key: ${{ secrets.PROJECT_KEY }}
                  scanner_name: ${{ secrets.SCANNER_NAME }}
                  git_url: ${{ secrets.GIT_URL }}
                  git_branch: ${{ secrets.GIT_BRANCH }}
                  git_credentials: ${{ secrets.GIT_CREDENTIALS }}
                  git_username: ${{ secrets.GIT_USERNAME }}
                  git_password: ${{ secrets.GIT_PASSWORD }}
        ```

        ### 2. Using Workflow Inputs (Recommended for reusable workflows)

        ```yaml
        on:
          workflow_dispatch:
            inputs:
              HOST:
                description: 'Host IP and Port'
                required: true
              ACCESS_TOKEN:
                description: 'Access Token'
                required: true
              action_type:
                description: 'Action Type (scan_only or scan_and_exploit)'
                required: true
              mock_mode:
                description: 'Mock Mode (true or false)'
                required: true
              tracker_type:
                description: 'Issue Tracker Type (github or jira)'
                required: true
              server_url:
                description: 'Issue Tracker Server URL'
                required: true
              username:
                description: 'Issue Tracker Username'
                required: true
              password:
                description: 'Issue Tracker Password'
                required: true
              project_key:
                description: 'Issue Tracker Project Key'
                required: true
              scanner_name:
                description: 'Scanner Name'
                required: true
              git_url:
                description: 'Git URL'
                required: true
              git_branch:
                description: 'Git Branch'
                required: true
              git_credentials:
                description: 'Git Credentials'
                required: false
              git_username:
                description: 'Git Username'
                required: true
              git_password:
                description: 'Git Password'
                required: false

        jobs:
          scan:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout code
                uses: actions/checkout@v4
              - name: Run Dynamic Scan Action
                uses: mfldosari/RASSED@v1.0.0
                with:
                  HOST: ${{ github.event.inputs.HOST }}
                  ACCESS_TOKEN: ${{ github.event.inputs.ACCESS_TOKEN }}
                  action_type: ${{ github.event.inputs.action_type }}
                  mock_mode: ${{ github.event.inputs.mock_mode }}
                  tracker_type: ${{ github.event.inputs.tracker_type }}
                  server_url: ${{ github.event.inputs.server_url }}
                  username: ${{ github.event.inputs.username }}
                  password: ${{ github.event.inputs.password }}
                  project_key: ${{ github.event.inputs.project_key }}
                  scanner_name: ${{ github.event.inputs.scanner_name }}
                  git_url: ${{ github.event.inputs.git_url }}
                  git_branch: ${{ github.event.inputs.git_branch }}
                  git_credentials: ${{ github.event.inputs.git_credentials }}
                  git_username: ${{ github.event.inputs.git_username }}
                  git_password: ${{ github.event.inputs.git_password }}
        ```

        ### 3. Hardcoding Values (Not Recommended)

        ```yaml
        jobs:
          scan:
            runs-on: ubuntu-latest
            steps:
              - name: Checkout code
                uses: actions/checkout@v4
              - name: Run Dynamic Scan Action
                uses: mfldosari/RASSED@v1.0.0
                with:
                  HOST: "HOST IP"
                  ACCESS_TOKEN: "exampleaccesstoken123"
                  action_type: "scan_only"
                  mock_mode: "false"
                  tracker_type: "github"
                  server_url: "https://github.com"
                  username: "octocat"
                  password: "hunter2"
                  project_key: "octocat/hello-world"
                  scanner_name: "veracode"
                  git_url: "https://github.com/octocat/hello-world.git"
                  git_branch: "main"
                  git_credentials: "ghp_exampletoken" #or 
                  git_password: "gitpass123"
                  git_username: "octocat"
        ```

## Required Inputs Reference

| Input          | Description                                         | Example Value                        |
|---------------|-----------------------------------------------------|--------------------------------------|
| HOST          | Host IP and Port                                    | 172.20.31.135:30899                  |
| ACCESS_TOKEN  | Access Token for orchestrator API                   | exampleaccesstoken123                |
| action_type   | Action Type (scan_only or scan_and_exploit)         | scan_only                            |
| mock_mode     | Mock Mode (true or false)                           | false                                |
| tracker_type  | Issue Tracker Type (github or jira)                 | github                               |
| server_url    | Issue Tracker Server URL                            | https://github.com                   |
| username      | Issue Tracker Username                              | octocat                              |
| password      | Issue Tracker Password                              | hunter2                              |
| project_key   | Issue Tracker Project Key (github: <owner>/<repo>)  | octocat/hello-world                  |
| scanner_name  | Scanner Name                                        | veracode                             |
| git_url       | Git repository URL                                  | https://github.com/octocat/hello-world.git |
| git_branch    | Git Branch                                          | main                                 |
| git_credentials| Git Credentials (token/password)                    | ghp_exampletoken                     |
| git_username  | Git Username                                        | octocat                              |
| git_password  | Git Password                                        | gitpass123                           |

> **Note:** For `project_key` with GitHub, use the format `<owner>/<repo>`, e.g., `octocat/hello-world`.
> All inputs are required and must be provided for the action to work correctly.
> You can pass in `password`, `git_credentials`, or both, depending on your authentication needs.
> You can combine secrets and variables to make static values