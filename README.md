# CodeAuditor Feedback Loop Workflow

This workflow action runs CodeAuditor scan on your website and creates new GitHub issue if it sees an increase in the number of broken links or code warnings/errors found from CodeAuditor scan

## Inputs

| name         | required | type  | description |
| ------------ | ---      | ------ | ----------- |
| GitHub_Token        | yes      | string | Your GitHub personal access token used to fetch data. Pass a secret by for instance using `${{ secrets.GH_TOKEN }}`. [Go here](https://github.com/settings/tokens/new?scopes=read:user) to generate one
| token     | yes      | string | Your personal CodeAuditor token that can be found on CodeAuditor's How It Works page
| url       | yes      | string | The url used on your CodeAuditor scan

## Example usage

Check out [`test.yml`](./.github/workflows/test.yml) for an example workflow.

Workflow:

```yml
name: Test CodeAuditor Workflow

on:
  workflow_dispatch:
    inputs:
      token:
        description: 'Your CodeAuditor token'
        required: true
      url:
        description: 'Your URL'
        required: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: CodeAuditor Feedback Loop Workflow
        uses: tombui99/codeauditor-github-workflow@v1.0.0
        with:
          # Your CodeAuditor token
          token: ${{github.event.inputs.token}}
          # Your URL
          url: ${{github.event.inputs.url}}
          # Your GitHub Token
          GitHub_Token: ${{secrets.GH_TOKEN}}
```
