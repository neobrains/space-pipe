# Space Deployment Github Action
A simple GitHub Action to deploy your projects to [Deta Space](https://alpha.deta.space/) and let their [builder](https://alpha.deta.space/docs/en/basics/projects#projects-in-builder) build your apps.

Thanks for the help ✨ [Sponge](https://github.com/rohanshiva).

## Usage
- Push your changes to create a new revision of your app.
- Release your latest revision. Each release can either be unlisted, where only people with the link can install it, or listed, which makes a release available for anyone to discover and install with [Deta Discovery](https://alpha.deta.space/discovery).

## Inputs
- `access_token` : Used for Space CLI authentication. From [Deta Space Dashboard](https://alpha.deta.space), open the *teletype* (command bar) and click on *Settings*. In the settings modal, click on *Generate Token* to generate an access token and copy the resulting *access token*.

- `project_id` : Used for getting the *.space folder* for pushing your code to Deta Space. To get your project id go to the [Builder](https://alpha.deta.space/builder) and in your project’s *Develop* tab, open the *teletype* (command bar) and copy the *Project ID*.

- `space_push` : (Optional) If *true*, pushes your changes to Space and creates a new revision. The default value is false.

- `space_release` : (Optional) If *true*, the latest revision will be released to Space. The default value is false.

- `list_on_discovery` : (Optional) If *true*, the latest revision will be released to Space & listed on Space Discovery. The default value is false.<br> 📌 No need to use *space_release* with this.

<br>

⚠️ Use [GitHub Actions secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository) to store your inputs.

⚠️ Make sure to add your 📝[Spacefile](https://alpha.deta.space/docs/en/reference/spacefile) in your repository. It contains the configuration of your project and is used by Deta Space to understand what your project looks like and how to run it.

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
          space_push: true
          list_on_discovery: true
```

Here [access_token](#access_token) and [project_id](#project_id) are stored as ACCESS_TOKEN and PROJECT_ID in GitHub Actions secrets. After creating a new revision with *space_push*, the latest revision will be listed on Space Discovery with *list_on_discovery*.

### Some workflow examples to manage your deployments:
- A single workflow can be created with [jobs](https://docs.github.com/en/actions/using-jobs/using-jobs-in-a-workflow#defining-prerequisite-jobs) to do space push, release of that revision and list that on Space Discovery with conditions to run a subsequent job if the previous one was successful.
- A workflow with *space_push* can be set up to run on [each push to the workflow's repository](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#push). Separate workflows for *space_release* and *list_on_discovery* can be set up to run on [workflow_dispatch](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows#workflow_dispatch) to be executed when needed.

- Configure your workflow to do *space_push* on each push to devlopment branch, *space_release* on each push to test branch and *list_on_discovery* on each push to main branch.

## License
This GitHub Action and associated documentation in this project are released under the [MIT License](https://github.com/neobrains/space-deployment-github-action/blob/master/LICENSE).
