# candid-ci

A collection of Github Actions to be consumed from Github Actions workflows.

## Available Actions
### [Get Author Info](./get-author-info/README.md)

Gets name, Github ID, Pagerduty ID, and Slack ID for author of the latest commit.

### [Helm Deploy Action](./helm-deploy/README.md)

Performs Helm upgrades and installations with configurable options. Supports several Helm flags and provides defaults for common scenarios.

### [Notify Author](./notify-author/README.md)

Sends slack message to the Author of the latest commit.

### [Notify Slack Channel](./notify-slack-channel/README.md)

Sends slack messages concerning deployments.

### [Setup Docker](./setup-docker/README.md)

Executes common docker setup tasks, including Google Artifact Registry auth and Buildx configuration.