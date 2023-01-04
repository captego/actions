# captego/actions
This is a mono-repo containing all sorts of github actions that is commonly use by the Captego development team

## Example
```yml 
name: Example
jobs:
  main:
    name: ${{ github.workflow }}
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: captego/actions/setup-node@master
      - uses: captego/actions/install-dependencies@master
      - uses: captego/actions/tag-and-release@master
      - uses: captego/actions/notify-slack@master
        with: 
          job-name: Tag & Release
          webhook-url: ${{ secrets.SLACK_WEBHOOK_URL }}
```

### Notes
How to use composite actions in composite actions
If you wish to use one of these composites actions in another composite action you will need to use the full name (eg captego/actions/setup-node@master)

Example:
The the publish-release-action depends on setup-node. In this case you would need to do - uses: captego/actions/setup-node@master.

If you use ./setup-node in a workflow in another repository (lets call it MY_REPOSITORY), the workflow in MY_REPOSITORY will look for for ./setup-node/action.yml-file in the MY_REPOSITORY.