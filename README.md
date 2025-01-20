# Analyze Pull Request with OpenAI

This action automates the process of reviewing code from GitHub pull requests using OpenAI's API.

## Features

- Extracts code diffs from pull requests
- Generates a summary of the code changes using OpenAI's API
- Posts the summary as a comment on the pull request

## Prerequisites

- OpenAI API key
- GitHub repository
- GitHub token

## Usage
To use this action in your repository, include it in your GitHub workflow YAML file. Below is an example configuration:
```
name: "Analyze Pull Request"

on:
  pull_request:
    types:
      - opened
      - reopened
      - synchronize

permissions:
  contents: write
  pull-requests: write

jobs:
  analyze:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Analyze Pull Request with OpenAI
        uses: ProductDock/openai-pr-review-action@v1
        with:
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          REPOSITORY: ${{ github.repository }}
          PR_NUMBER: ${{ github.event.pull_request.number }}
          GPT_MODEL: 'gpt-4o-mini' # Optional
          MAX_TOKENS: '500' # Optional
```
## Inputs

| Input Name  | Required | Description                                                                                                                           |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------------------------|
| `OPENAI_API_KEY` | `true` | Your OpenAI API key used to authenticate and interact with the OpenAI API for generating insights or responses.                       |
| `GITHUB_TOKEN` | `true` | GitHub token provided by GitHub Actions for authenticating and interacting with the GitHub API (e.g., fetching pull request details). |
| `REPOSITORY` | `true` | The full name of the GitHub repository (e.g., owner/repo) where the pull request exists.                                              |
| `PR_NUMBER` | `true` | The pull request number in the specified repository to analyze.                                                                       |
| `GPT_MODEL` | `false` | The OpenAI GPT model to use for analysis. Specify the model name for customization (default: `gpt-4o-mini`).                          |
| `MAX_TOKENS` | `false` | The maximum number of tokens the model can generate in its response (default: `500`).                                                   |

## Required Permissions

This action requires the following permissions to function properly:

- **Contents**: `write`
- **Pull Requests**: `write`

## Licence
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
