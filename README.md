# Detect Changes in Mono-Repo

A GitHub Action that detects changes in multiple modules within a mono-repo by comparing folder hashes between commits.

## Inputs

- `modules` (required): Space-separated list of modules to check for changes

## Outputs

- `changes`: JSON object containing change status for each module

## How it works

This action:
1. Checks out the repository with full history (`fetch-depth: 0`)
2. Sets up Python 3.11
3. Runs a Python script that compares folder hashes between commits to detect changes
4. Outputs change status for each specified module

## Example Usage

```yaml
jobs:
  detect-changes:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      # use if it's not on your runner
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: "3.11"
        
      - name: Detect Changes
        id: detect
        uses: cham207388/detect-changes@v5
        with:
          modules: "frontend backend api"

      - name: Use change detection results
        run: |
          echo "Changes detected: ${{ steps.detect.outputs.changes }}"
```

## Author

Alhagie Bai Cham