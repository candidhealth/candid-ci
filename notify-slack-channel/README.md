# Notify Slack Channel Github Action

## Input Parameters

### Required Inputs
| Input | Description |
|-------|-------------|
| `environment` | The environment being deployed to |
| `deploy_status` | Deploy status string. Color for the message sidebar will be set to red for 'Failed' and green for 'Completed' |
| `slack_token` | Token used to auth with when sending the message to slack |

### Optional Inputs
| Input | Description | Default |
|-------|-------------|---------|
| `channel_id` | The slack channel ID (different than channel name) to notify. Defaults to deploys channel. | `CQECM8V53` |
| `update_existing` | The timestamp of a deployment slack message to update instead of sending a new message. | - |