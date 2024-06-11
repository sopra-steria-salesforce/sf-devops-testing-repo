# salesforce-dx-template

A Salesforce DX template containing helpful stuff to initialise new projects, and containing GitHub workflows for easier deployment.

# 🧑‍💻 Setup

See [docs/devops](docs/devops) for instructions on how to setup this template in a new repo.

# 🤓 Develop

After all setup is done in the previous step, you're ready to develop!

You can now (typically):

-   Create feature branches and create PR's
-   This requires validation and code reviews, to ensure quality and safety before deploying to production
-   New changes merged to `main` are automatically deployed to preprod
-   After a quick validation in preprod, you're good to go and can easily deploy to production 🎉

## First-time Install

Make sure you've performed the steps in [Local Setup](docs/devops/local-setup.md) before trying to create a Scratch Org.

## Make Changes

1. Run `npm run scratch:create`
1. Make your change inside the Scratch Org
1. Run `npm run scratch:pull` to add the changes from the Scratch Org to your local computer
1. Commit & Push the changes inside GitHub Desktop
1. Create a Pull Request
    - To `main` or `preprod`, depending on use case
    - Get validated successfully
    - If Slack Integration is setup, a post is added for others to code review your changes. Otherwhise, get someone to approve it.
1. Merge it
1. Check the package creation status in the `Actions` tab
1. Once the package is done, check it in the `Code` tab → `Releases`
1. Click `Deploy` on the release you want to deploy it to production
    - Click `Run Workflow`
    - Keep `Branch: main` if you want to deploy the latest package.
    - If you want a specific package, click the dropdown → `Tags` → Choose the version
    - Finally, click `Run workflow` again to deploy
    - Wait a couple of seconds, and a new entry should appear in the list. You can open it to view the progress of the deployment.

# Licensing

See [LICENSE](LICENSE), or summarised:

## Permissions

You're allowed to use this template:

-   For commercial use
-   For private use
-   To distribute it
-   To modify it

## Conditions

You must specify proper copyright notices. That means, somewhere in your code (e.g., the `LICENSE` file or the readme), you must link to this repository.

## Limitations

The author of this template refrains from any liability or warranty on the use of this template.
