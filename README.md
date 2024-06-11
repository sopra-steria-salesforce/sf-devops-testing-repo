# salesforce-dx-template

A Salesforce DX template containing helpful stuff to initialise new projects, and containing GitHub workflows for easier deployment.

# Setup

See [docs/devops](docs/devops) for instructions on how to setup this template in a new project.

When the repo is up-and-running, you can make changes in a Scratch Org and deploy it to production. See next paragraph.

# Making Changes and Deployment

You can now create feature branches and create PR's. This requires validation and code reviews, to ensure quality and safety before deploying to production. New changes merged to `main` are automatically deployed to preprod. After a quick validation in preprod, you're good to go and can easily deploy to production 🎉

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
