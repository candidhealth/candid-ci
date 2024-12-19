# Notify Author Github Action

## Input Parameters

### Required Inputs

| Input | Description |
|-------|-------------|
| `slack_token` | Token used to auth with when sending the message to slack |
| `message` | The contents of the message to send to the author. Supports slack's mrkdwn format. |

### Optional Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `update_existing` | The timestamp of a deployment slack message to update instead of sending a new message. | `""` |