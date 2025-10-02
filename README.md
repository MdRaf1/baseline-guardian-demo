# Baseline Guardian Demo

This repository serves as a live demonstration for the **[Baseline Guardian GitHub Action](https://github.com/MdRaf1/baseline-guardian)**. Its purpose is to showcase how the action automatically scans pull requests, checks CSS properties against the Baseline dataset, and posts a clear, actionable report.

## Live Demo in Action

The pull request in this repository was intentionally created with a CSS feature that has "newly available" to trigger the action's `fail` policy.

**➡️ [View the Live Pull Request Here](https://github.com/MdRaf1/baseline-guardian-demo/pull/1)**

### Example Report

Below is a gif of the comment automatically posted by Baseline Guardian on the pull request. Notice how it identifies the feature, states its status, and provides a direct link to the MDN documentation.

![Baseline Guardian Report gif](https://raw.githubusercontent.com/MdRaf1/baseline-guardian/main/docs/pr-comment.gif)

## How This Demo is Configured

This demonstration is powered by two simple configuration files in the `main` branch:

**1. The Workflow File (`.github/workflows/baseline-guardian.yml`)**

This file tells GitHub Actions to run the public version of Baseline Guardian on every pull request.

```yaml
name: 'Baseline Guardian'

on:
  pull_request:
    types: [opened, synchronize]

permissions:
  contents: read
  pull-requests: write
  checks: write

jobs:
  run-guardian:
    name: Run Baseline Guardian
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run Baseline Guardian
        uses: MdRaf1/baseline-guardian@v1.0.0
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
```

**2. The Policy File (`.baseline-guardian.yml`)**

This file defines our team's compatibility rules. For this demo, we set it to warn about features with "newly available."

```yaml
policy:
  newly_available: fail
  limited_availability: warn
```

## About the Project

This demo repository is just a showcase. To learn more about the Baseline Guardian action itself or to use it in your own projects, please visit the links below.

- **[View the Source Code on GitHub](https://github.com/MdRaf1/baseline-guardian)**
- **[Install the Action from the GitHub Marketplace](https://github.com/marketplace/actions/baseline-guardian)**
