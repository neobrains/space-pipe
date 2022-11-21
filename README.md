# Space Deployment Github Action

Thanks for the help ✨ [Sponge](https://github.com/rohanshiva).

## Usage
GitHub Action to 🚀 push your project to [Deta Space](https://alpha.deta.space/).

## Inputs
- ### `access_token`
  Used for Space CLI authentication. From [Deta Space Dashboard](https://alpha.deta.space), open the teletype (command bar) and click on `Settings`. In the settings modal, click on `Generate Token` to generate an access token and copy the resulting token.

- ### `project_id`
  Used for getting the .space folder for pushing your code to Deta Space. To get your project id go to the [Builder](https://alpha.deta.space/builder) and in your project’s `Develop` tab, open the teletype (command bar) and copy the Project ID.

<br/><br/>
⚠️ Use [GitHub Actions secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) to store your inputs.

⚠️ Make sure to add your 📝 [Spacefile](https://alpha.deta.space/docs/en/reference/spacefile) in your repository. It contains the configuration of your project and is used by Deta Space to understand what your project looks like and how to run it.

## Example workflow
```
name: Push to Space
on: push

jobs:
  push-to-space:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deta Space Deployment Github Action
        uses: neobrains/space-deployment-github-action@0.1
        with:
          access_token: ${{ secrets.ACCESS_TOKEN }}
          project_id: ${{ secrets.PROJECT_ID }}
```

Here [access_token](#access_token) and [project_id](#project_id) are stored as ACCESS_TOKEN and PROJECT_ID in GitHub Actions secrets.
<br/>

💬 The [Space CLI](https://alpha.deta.space/docs/en/reference/cli) needs standard inputs for creating releases. ***As of now*** this feature is not implemented in this GitHub Action. Follow the instructions [here](https://alpha.deta.space/docs/en/basics/releases#releasing-from-the-gui) to create a release for your project.
