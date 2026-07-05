# LeetCode Sync (Custom)

GitHub Action for automatically syncing LeetCode submissions to a GitHub repository, with an added feature to automatically fetch and submit the LeetCode daily question boilerplate to your account and repo.

## How to use

1. Go to REPO > settings > actions and in Workflow Permissions section give actions Read and Write permissions.

2. Add the `LEETCODE_CSRF_TOKEN` and `LEETCODE_SESSION` as GitHub secrets to your tracking repo.

3. Add a workflow file with this action under the `.github/workflows` directory, e.g. `sync_leetcode.yml`.

   Example workflow file:

   ```yaml
   name: Sync Leetcode

   on:
     workflow_dispatch:
     schedule:
       - cron: "30 23 * * *"

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
         - name: Sync
           uses: AKASH-DEV-23/leetcode-sync-action@main
           with:
             github-token: ${{ github.token }}
             leetcode-csrf-token: ${{ secrets.LEETCODE_CSRF_TOKEN }}
             leetcode-session: ${{ secrets.LEETCODE_SESSION }}
             destination-folder: DSA
             verbose: true
             commit-header: "[Commit]"
             sync-daily-question: true
             sync-daily-language: java
   ```

## Custom Inputs

- `sync-daily-question`: Syncs the daily question boilerplate code and automatically submits it to LeetCode for you! (default: false)
- `sync-daily-language`: The language to use for the daily question empty solution (default: 'python3', set to 'java' for Java).
