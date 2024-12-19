# Get Author Info GitHub Action

Returns info regarding author name, github id, slack id and pager duty id.

## Outputs

| Output         | Description                                                                        |
|--------------- |------------------------------------------------------------------------------------|
| `author`       | User display name from Git.                                                        |
| `github_id`    | Github User ID.                                                                    |
| `name`         | The contents of the message to send to the author. Supports slack's mrkdwn format. |
| `pagerduty_id` | Pager Duty User ID.                                                                |
| `slack_id`     | Slack User ID.                                                                     |