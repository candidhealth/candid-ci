# Helm Upgrade GitHub Action

This GitHub Action performs Helm upgrades with configurable options, supporting both new installations and upgrades of existing releases. The action wraps the `helm upgrade` command with support for all standard Helm flags and options.

## Usage

### Basic Example

```yaml
steps:
  - uses: candidhealth/candid-ci/helm-deploy@v1
    with:
      release_name: my-application
      chart: ./charts/application
      namespace: production
```

### Complete Example with All Options

```yaml
steps:
  - uses: candidhealth/candid-ci/helm-deploy@v1
    with:
      release_name: my-application
      chart: ./charts/application
      namespace: production
      values_file: ./values/prod.yaml
      version: 1.2.3
      timeout: 10m0s
      atomic: true
      install: true
      force: false
      wait: true
      create_namespace: true
      set_values: "image.tag=v1.2.3,replicas=3,ingress.enabled=true"
      kubeconfig: ./kubeconfig.yaml
```

## Real-World Examples

### Deploying to Multiple Environments

```yaml
name: Deploy Application
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        environment: [staging, production]
        include:
          - environment: staging
            namespace: staging
            values_file: ./values/staging.yaml
          - environment: production
            namespace: production
            values_file: ./values/production.yaml
    
    steps:
      - uses: actions/checkout@v3
      
      - uses: candidhealth/candid-ci/helm-deploy@v1
        with:
          release_name: myapp-${{ matrix.environment }}
          chart: ./charts/myapp
          namespace: ${{ matrix.namespace }}
          values_file: ${{ matrix.values_file }}
          set_values: "image.tag=${{ github.sha }}"
          create_namespace: true
```

## Input Parameters

### Required Inputs

| Input | Description |
|-------|-------------|
| `chart` | Chart reference (path/name) |
| `namespace` | Kubernetes namespace |
| `release_name` | Name of the Helm release |

### Optional Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `atomic` | Roll back on failed upgrade | `true` |
| `create_namespace` | Create namespace if missing | `false` |
| `dry_run` | Simulate an upgrade | `false` |
| `force` | Force resource updates | `false` |
| `install` | Install if release not present | `true` |
| `kubeconfig` | Path to kubeconfig file | `""` |
| `repository` | Helm chart reposiotry. Only used for remote charts. | `""` |
| `set_values` | Set values on command line | `""` |
| `timeout` | Time to wait for operations | `5m0s` |
| `values_file` | Path to values YAML file | `""` |
| `version` | Version constraint for the chart | `""` |
| `wait` | Wait for resources to be ready | `true` |

## Advanced Usage Tips

### Setting Multiple Values

Values can be set in multiple ways:
1. Using a values file:
```yaml
values_file: ./values/production.yaml
```

2. Using the set_values input with multiple values:
```yaml
set_values: "key1=value1,key2=value2"
```

3. Using multiline set_values:
```yaml
set_values: |
  global.environment=production
  image.tag=${{ github.sha }}
  replicas=3
```

### Version Control

Specify exact versions for production:
```yaml
version: 1.2.3
```

Or use version constraints:
```yaml
version: ">= 1.2.0"
```

### Timeout Configuration

For large deployments, increase the timeout:
```yaml
timeout: 15m0s
```

For development environments, use shorter timeouts:
```yaml
timeout: 2m0s
```

## Error Handling

The action includes several safety features:

1. `atomic: true` (default) ensures clean rollback on failure
2. `wait: true` (default) ensures deployment completion before marking success
3. Setting `force: true` can help resolve stuck deployments but should be used carefully

## Troubleshooting

Common issues and solutions:

1. **Timeout Errors**
   - Increase the timeout value
   - Check for resource constraints
   ```yaml
   timeout: 10m0s
   ```

2. **Namespace Issues**
   - Enable namespace creation
   ```yaml
   create_namespace: true
   ```

3. **Resource Conflicts**
   - Use force flag (carefully!)
   ```yaml
   force: true
   ```

4. **Value Override Issues**
   - Check value precedence (command-line sets override values file)
   - Use `--set` for critical values
   ```yaml
   set_values: "critical.setting=value"
   values_file: ./values/base.yaml
   ```