# PR Status Github Action
Github Action to set a PR with a Context and a Status. It is useful for developers to dynamically create a Context in a PR that can act as a bridge between two different actions. Like, one action can set the Context to "pending" state and lock the PR and a different action can set the same Context to "success" or "failure" state that can further dictate if the PR can be merged.

## Inputs

Name | Description | Required
--- | --- | ---
`repository` | Git Repository name | `true`
`pr-number` | PR number in the Git Repository | `true`
`context` | Name to use as a Context in PR | `true`
`state` | State to set in the PR context | `true`
`description` | A short description to define the status of the Context | `true`
`target-url` | The target URL to associate with the Context | `false`

## Example Usage

```
jobs:
  set-pr-status:
    runs-on: ubuntu-latest
    steps:
    - name: Set PR Context Status to Pending
        uses: gpuliyar/pr-status-action@v1.0.0
        with:
          # Repository name (Mandatory)
          repository: gpuliyar/awesome-project

          # PR Number  (Mandatory)
          pr-number: 101

          # Name the context to use in the PR  (Mandatory)
          context: cool-context

          # State to apply (Mandatory)
          # Any of the (error | failure | pending | success) states
          state: pending

          # A short description of the status (Mandatory)
          description: This is so awesome to use a context in a PR

          # The target URL to associate with the Context Status (Optional)
          # This Github UI will link the URL (source of status) to the Context.
          target_url: https://nice-url.gpuliyar.com

        env:
          # Default Github Token
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
