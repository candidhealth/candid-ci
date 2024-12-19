# Setup Docker Github Action

Executes common docker setup tasks, including Google Artifact Registry auth and Buildx configuration.

## Usage

### Basic Example

```yaml
steps:
- uses: candidhealth/candid-ci/setup-docker@main
  with:
    registry: my.cool.registry
    access_token: ${{ secrets.ACCESS_TOKEN }}
```

## Input Parameters

### Required Inputs
| Input | Description |
|-------|-------------|
| `registry` | The docker registry that will be logged into. |
| `access_token` | Access token to be used to auth to the registry. |