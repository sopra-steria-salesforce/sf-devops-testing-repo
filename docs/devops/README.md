# Setup Repo

This documentation is for when you want to setup a new repo. Either because you want another package or because this is a brand new project 🎉

1. On the [salesforce-dx-template](https://github.com/sopra-steria-salesforce/salesforce-dx-template) main page, click `Use this template` and give your repo a name
    - Do _**not**_ copy branches
1. From now on, all changes described are to be done on the new repo you jsut created
1. Go to `Settings` → `Collaborators and teams`
    - Add whoever needs access.
1. Setup Environments
 <!-- TODO: add -->
1. Add secrets and variables
    - Secrets and variables can be added globally (GitHub org settings), in a specific repo (repo settings) or using environments. Unsure? Repo settings is a safe bet.
    - In org or repo settings → `Secrets and Variables` → `Actions`
    - Add the needed secrets and variables (see [Variables](#variables) and [Secrets](#secrets) below)
1. Initialise repo
    - The last step! This step will automatically:
        - Set Labels
        - Set Settings
        - Create Rulesets
        - Create first GitHub release
        - Create Salesforce Unlocked Package
        - Create preprod branch
    - **Make sure all secrets are added before this step!**
    - On your new repo → `Actions` tab → `Show more workflows...` → `[X] Initialise/Update Repo` → `Run workflow` (x2)
    - Ensure the job runs successfully. You can retry or re-run the job safely if something failed.
1. Your repo should now be done! 🎉
    - Go to thw main page of your new repo, and look for the header `Making Changes and Deployment` for further instructions.

# Variables

<!-- prettier-ignore -->
| Name | Description | Required? |
| ---- | ----------- | --------- |
| `SF_PROD_USERNAME`<br>`SF_PROD_INSTANCE_URL`<br>`SF_PREPROD_USERNAME`<br>`SF_PREPROD_INSTANCE_URL`<br>`SF_SIT_USERNAME`<br>`SF_SIT_INSTANCE_URL` | See [Create SF CLI Integration User](#create-sf-cli-integration-user) | ✅ |
| `SF_SLACK_ENABLED` | Set this value to `true`/`false` | ✅ |
| `SF_SLACK_DEPLOYMENT_CHANNEL_ID`<br>`SF_SLACK_RELEASE_CHANNEL_ID`<br>`SF_SLACK_REVIEW_CHANNEL_ID`<br>`SF_SLACK_SYNC_CHANNEL_ID` | See [Create Slack Channels](#create-slack-channels) | 🙅 No |
| `SF_JIRA_URL` | | 🙅 Nope |

## Create SF CLI Integration User

<!-- TODO: create -->

## Create Slack Channels

1. Create the following channels in Slack:
    - `salesforce-github-reviews`
    - `salesforce-deployment-log`
    - `salesforce-sync-log`
    - `salesforce-releases`
1. For each channel, right-click it and click `View channel details`
    - Scroll to the bottom and copy the `Channel ID`
    - Save the `Channel ID` for each channel into the four variables needed.

# Secrets

<!-- prettier-ignore -->
| Name | Description | Required? |
| ---- | ----------- | --------- |
| `SF_PACKAGE_KEY`| Can be whatever you want.<br>But it's a password every developer needs to remember. | ✅ |
| `SF_GITHUB_BOT_APP_ID`<br>`SF_GITHUB_BOT_PRIVATE_KEY` | See [Create GitHub App](#create-github-app) | ✅ |
| `SF_PROD_CLIENT_ID`<br>`SF_PROD_CLIENT_SECRET`<br>`SF_PROD_PRIVATE_KEY`<br>`SF_PREPROD_CLIENT_ID`<br>`SF_PREPROD_PRIVATE_KEY`<br>`SF_SIT_CLIENT_ID`<br>`SF_SIT_PRIVATE_KEY` | See [Create SF CLI Connected App](#create-sf-cli-connected-app) | ✅ |
| `SF_SLACK_BOT_TOKEN` | See [Slack Integration](#slack-integration) | 🙅 Hell nah |
| `SF_JIRA_ACCESS_TOKEN` | See [Jira Integration](#jira-integration) | 🙅 Nah girl |

## Create GitHub App

1. Open the GitHub org settings → `Developer settings` → `GitHub Apps` → `New GitHub app`
1. Give it a unique name
1. `Homepage URL`: `https://localhost` (or the url to the GitHub org, doesn't matter)
1. `Webhook Active`: uncheck this
1. Repository permissions
    - `Actions`: Read and write
    - `Administration`: Read and write
    - `Contents`: Read and write
    - `Pull requests`: Read and write
    - `Variables`: Read and write

-   Organization permissions:
    -   `Members`: Read-only

1. Click `Create GitHub app`
1. Click `Generate a new client secret`
    - You should now have created a value needed for the secret `SF_GITHUB_BOT_PRIVATE_KEY`
1. Also store the `App ID` as the secret `SF_GITHUB_BOT_APP_ID`

## Create SF CLI Connected App

<!-- TODO: create -->

## Slack Integration

By adding an API token for Slack, you'll get deployment logs/errors, release notes and code reviews posted to Slack automatically.

1. Go to [api.slack.com](https://api.slack.com/apps)
1. Click `Create New App` → `From an app manifest` → Choose a Slack workspace
1. Copy & paste the JSON below into the input field (replace everything already there) → `Next` → `Create`
1. Click `Install to Workspace` → Add the four channels you just created → `Allow`
1. Add a cute logo to the bot, if you want to
1. Go to `OAuth & Permissions` → Press `Copy` on the `Bot User OAuth Token`
    - This will be the secret `SF_SLACK_BOT_TOKEN`

### App Manifest to Copy/Paste

```json
{
	"display_information": { "name": "Salesforce Bot", "description": "Jeg poster oppdateringer om Salesforce", "background_color": "#3854a1" },
	"features": { "bot_user": { "display_name": "Salesforce Bot", "always_online": false } },
	"oauth_config": { "scopes": { "bot": ["channels:history", "chat:write", "chat:write.customize", "groups:history", "im:history", "incoming-webhook", "mpim:history", "reactions:write"] } },
	"settings": { "interactivity": { "is_enabled": false }, "org_deploy_enabled": false, "socket_mode_enabled": false, "token_rotation_enabled": false }
}
```

## Jira Integration

See [Manage API tokens for your Atlassian account](https://support.atlassian.com/atlassian-account/docs/manage-api-tokens-for-your-atlassian-account/) for how to create an API token. This token will be stored as the secret `SF_JIRA_ACCESS_TOKEN`.
