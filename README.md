# RASSED
# Dynamic Scan Action

Reusable GitHub Action for validating credentials and running RASSED security scan.

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
                  llm_endpoint_url: ${{ secrets.LLM_ENDPOINT_URL }}
                  llm_model_name: ${{ secrets.LLM_MODEL_NAME }}
                  llm_api_key: ${{ secrets.LLM_API_KEY }}
                  llm_max_context_tokens: ${{ secrets.LLM_MAX_CONTEXT_TOKENS }}
                  # Only use the following if scan type is scan_and_exploit
                  exploiter_llm_api_key: ${{ secrets.EXPLOITER_LLM_API_KEY }}
                  exploiter_llm_endpoint_url: ${{ secrets.EXPLOITER_LLM_ENDPOINT_URL }}
                  exploiter_llm_max_context_tokens: ${{ secrets.EXPLOITER_LLM_MAX_CONTEXT_TOKENS }}
                  exploiter_llm_model_name: ${{ secrets.EXPLOITER_LLM_MODEL_NAME }}
                  exploiter_target_url: ${{ secrets.EXPLOITER_TARGET_URL }}
                  exploiter_max_attempts: ${{ secrets.EXPLOITER_MAX_ATTEMPTS }}
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
                  llm_endpoint_url: ${{ github.event.inputs.llm_endpoint_url }}
                  llm_model_name: ${{ github.event.inputs.llm_model_name }}
                  llm_api_key: ${{ github.event.inputs.llm_api_key }}
                  llm_max_context_tokens: ${{ github.event.inputs.llm_max_context_tokens }}
                  # Only use the following if scan type is scan_and_exploit
                  exploiter_llm_api_key: ${{ github.event.inputs.exploiter_llm_api_key }}
                  exploiter_llm_endpoint_url: ${{ github.event.inputs.exploiter_llm_endpoint_url }}
                  exploiter_llm_max_context_tokens: ${{ github.event.inputs.exploiter_llm_max_context_tokens }}
                  exploiter_llm_model_name: ${{ github.event.inputs.exploiter_llm_model_name }}
                  exploiter_target_url: ${{ github.event.inputs.exploiter_target_url }}
                  exploiter_max_attempts: ${{ github.event.inputs.exploiter_max_attempts }}
    
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
                  llm_endpoint_url: "http://localhost:11434/v1"
                  llm_model_name: "SimonPu/qwen3-coder:30B-Instruct_Q4_K_XL"
                  llm_api_key: "ollama"
                  llm_max_context_tokens: 262144
                  # Only use the following if scan type is scan_and_exploit
                  exploiter_llm_api_key: "ollama"
                  exploiter_llm_endpoint_url: "http://localhost:33821"
                  exploiter_llm_max_context_tokens: 4096
                  exploiter_llm_model_name: "qwen3:30b-a3b-thinking-2507-fp16"
                  exploiter_target_url: "http://localhost:8080"
                  exploiter_max_attempts: 3
                  
        ```



## Required Inputs Reference


| Input                          | Description                                         | Example Value                        | Required for scan_only | Required for scan_and_exploit |
|---------------------------------|-----------------------------------------------------|--------------------------------------|------------------------|------------------------------|
| HOST                           | Host IP and Port                                    | 172.20.31.135:30899                  | Yes                   | Yes                         |
| ACCESS_TOKEN                   | Access Token for orchestrator API                   | exampleaccesstoken123                | Yes                   | Yes                         |
| action_type                    | Action Type (scan_only or scan_and_exploit)         | scan_only                            | Yes                   | Yes                         |
| mock_mode                      | Mock Mode (true or false)                           | false                                | Yes                   | Yes                         |
| tracker_type                   | Issue Tracker Type (github or jira)                 | github                               | Yes                   | Yes                         |
| server_url                     | Issue Tracker Server URL                            | https://github.com                   | Yes                   | Yes                         |
| username                       | Issue Tracker Username                              | octocat                              | Yes                   | Yes                         |
| password                       | Issue Tracker Password                              | hunter2                              | Yes                   | Yes                         |
| project_key                    | Issue Tracker Project Key (github: <owner>/<repo>)  | octocat/hello-world                  | Yes                   | Yes                         |
| scanner_name                   | Scanner Name                                        | veracode                             | Yes                   | Yes                         |
| git_url                        | Git repository URL                                  | https://github.com/octocat/hello-world.git | Yes              | Yes                         |
| git_branch                     | Git Branch                                          | main                                 | Yes                   | Yes                         |
| git_credentials                | Git Credentials (token/password)                    | ghp_exampletoken                     | Optional (one required) | Optional (one required)   |
| git_username                   | Git Username                                        | octocat                              | Yes                   | Yes                         |
| git_password                   | Git Password                                        | gitpass123                           | Optional (one required) | Optional (one required)   |
| llm_endpoint_url               | LLM Endpoint URL                                    | http://localhost:11434/v1            | Yes                   | Yes                         |
| llm_model_name                 | LLM Model Name                                      | SimonPu/qwen3-coder:30B-Instruct_Q4_K_XL | Yes               | Yes                         |
| llm_api_key                    | LLM API Key                                         | ollama                               | Yes                   | Yes                         |
| llm_max_context_tokens         | LLM Max Context Tokens                              | 262144                               | Yes                   | Yes                         |
| exploiter_llm_api_key          | Exploiter LLM API Key                               | ollama                               | No                    | Yes                         |
| exploiter_llm_endpoint_url     | Exploiter LLM Endpoint URL                          | http://localhost:33821               | No                    | Yes                         |
| exploiter_llm_max_context_tokens| Exploiter LLM Max Context Tokens                    | 4096                                 | No                    | Yes                         |
| exploiter_llm_model_name       | Exploiter LLM Model Name                            | qwen3:30b-a3b-thinking-2507-fp16      | No                    | Yes                         |
| exploiter_target_url           | Target URL for Exploitation                         | http://localhost:8080                | No                    | Yes                         |
| exploiter_max_attempts         | Max Attempts for Exploitation                       | 3                                    | No                    | Yes                         |

> **Note:**
> - If `action_type` is `scan_only`, only the columns marked "Yes" under scan_only are required.
> - If `action_type` is `scan_and_exploit`, you must also provide all columns marked "Yes" under scan_and_exploit.
> - For `git_password` and `git_credentials`, at least one must be provided (either is sufficient, or both).
> - For `project_key` with GitHub, use the format `<owner>/<repo>`, e.g., `octocat/hello-world`.
> - You can combine secrets and variables to make static values.

> **Note:** For `project_key` with GitHub, use the format `<owner>/<repo>`, e.g., `octocat/hello-world`.
> All inputs are required and must be provided for the action to work correctly.
> You can pass in `git_password`, `git_credentials`, or both.
> You can combine secrets and variables to make static values
