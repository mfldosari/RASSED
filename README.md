# RASSED
# Dynamic Scan Action

Reusable GitHub Action for validating credentials and running dynamic security scans via an orchestrator API.

## Usage

you can use it in any workflow like this:

```yaml
    inputs:
      HOST:
        description: 'Host IP and Port (e.g., 172.20.31.135:30899)'
        required: true
        default: '172.20.31.135:30899'
      ACCESS_TOKEN:
        description: 'Access Token'
        required: true
      action_type:
        description: 'Action Type (scan or scan_and_exploit)'
        required: true
        default: 'scan_only'
        type: choice
        options:
          - scan_only
        #   - scan_and_exploit
      mock_mode:
        description: 'Mock Mode (true or false)'
        required: true
        default: 'false'
        type: choice
        options:
          - 'true'
          - 'false'
      debug_mode:
        description: 'Debug Mode (true or false)'
        required: true
        default: 'false'
        type: choice   
        options:
          - 'true'
          - 'false'
      tracker_type:
        description: 'Issue Tracker Type (github or jira)'
        required: true
        default: 'github'
        type: choice
        options:
          - github
          - jira
      server_url:
        description: 'Issue Tracker Server URL. Enter https://github.com if tracker_type is github, or https://jira.com if tracker_type is jira.'
        required: true
        default: ''
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
        default: 'Security Scan - veracode'
      git_url:
        description: 'Git URL'
        required: true
        default: ''
      git_branch:
        description: 'Git Branch'
        required: true
        default: ''
      git_credentials:
        description: 'Git Credentials'
        required: true
      git_username:
        description: 'Git Username'
        required: true
        default: ''
      git_password:
        description: 'Git Password'
        required: true
jobs:
  scan:
    runs-on: ubuntu-latest #or self-hosted
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
          
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Run Dynamic Scan Action
        uses: mfldosari/RASSED@v1.0.0
        with:
        HOST: "172.20.31.135:30899"                # Example: Host IP and Port
        ACCESS_TOKEN: "exampleaccesstoken123"       # Example: Access Token
        action_type: "scan_only"                    # scan_only or scan_and_exploit
        mock_mode: "false"                          # true or false
        tracker_type: "github"                      # github or jira
        server_url: "https://github.com"            # Example: Issue Tracker Server URL
        username: "octocat"                         # Example: Issue Tracker Username
        password: "hunter2"                         # Example: Issue Tracker Password
        project_key: "octocat/hello-world"          # Example: Issue Tracker Project Key (for github use <owner>/<repo>)
        scanner_name: "veracode"                    # Example: Scanner Name
        git_url: "https://github.com/your/repo.git" # Example: Git URL
        git_branch: "main"                          # Example: Git Branch
        git_credentials: "ghp_exampletoken"         # Example: Git Credentials
        git_username: "octocat"                     # Example: Git Username
        git_password: "gitpass123"                  # Example: Git Password
    ```


