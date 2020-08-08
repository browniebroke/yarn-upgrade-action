# Yarn upgrade action

A simple action to run `yarn upgrade` in a GitHub workflow.

## Usage

Example of workflow:

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
  
    # Read node version from `.nvmrc` file
    - id: nvmrc
      uses: browniebroke/read-nvmrc-action@v1

    - uses: actions/setup-node@v1
      with:
        # use the output from the action
        node-version: '${{ steps.nvmrc.outputs.node_version }}'

    # Run `yarn upgrade`
    - uses: browniebroke/yarn-upgrade-action@v2

    # Open a pull request if there are any changes
    - name: Create Pull Request
      uses: peter-evans/create-pull-request@v2
      with:
        token: ${{ secrets.GITHUB_TOKEN }}
        branch: update/yarn-upgrade
        title: Run yarn upgrade
        commit-message: "chore(deps): Run yarn upgrade"
```
