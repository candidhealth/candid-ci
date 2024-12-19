# Get Author Info GitHub Action

Returns info regarding author name, github id, slack id and pager duty id.

## Usage

### Basic Example

```yaml
steps:
- uses: candidhealth/candid-ci/get-author-info@main
  id: author_info
- name: Echo author info
  shell: bash
  run: |
        echo ${{ steps.author_info.outputs.author }}
        echo ${{ steps.author_info.outputs.github_id }}
        echo ${{ steps.author_info.outputs.name }}
        echo ${{ steps.author_info.outputs.pagerduty_id }}
        echo ${{ steps.author_info.outputs.slack_id }}
```

## Outputs

| Output         | Description                                                                        |
|--------------- |------------------------------------------------------------------------------------|
| `author`       | User display name from Git.                                                        |
| `github_id`    | Github User ID.                                                                    |
| `name`         | The contents of the message to send to the author. Supports slack's mrkdwn format. |
| `pagerduty_id` | Pager Duty User ID.                                                                |
| `slack_id`     | Slack User ID.                                                                     |