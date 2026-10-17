# install-octopus-cli-action

<img alt= "" src="https://github.com/OctopusDeploy/install-octopus-cli-action/raw/main/assets/github-actions-octopus.png" />

This is a GitHub Action to install the new [Octopus CLI](https://octopus.com/blog/building-octopus-cli-vnext#introducing-the-new-octopus-cli-octopus) (`octopus`) on runners and self-hosted environments. Once installed, the Octopus CLI may be used to issue commands to [Octopus Deploy](https://octopus.com/). Subsequent actions may use the Octopus CLI, which is cached and available via `PATH`.

## What is the Octopus CLI?

The Octopus CLI is a command line tool that builds on top of the [Octopus REST API](https://octopus.com/docs/octopus-rest-api). It enables you to package applications for deployment and manage your environments, deployments, channels, projects, and workers in Octopus Deploy.

## Features

- Download, install, and cache Octopus CLI to be used in workflows
- Supports SemVer-based version numbers with wildcards (i.e. `0.8.*`) but not ranges

## Migration Guide(s)

Please refer to the [migration guide](migration-guide.md) if moving between major versions of this action.

## Examples

To install the latest version (i.e. `*` or `latest`) of the Octopus CLI:

```yml
- name: Install Octopus CLI 🐙
  id: install_octopus_cli
  uses: OctopusDeploy/install-octopus-cli-action@v4
  with:
    version: '*'
```

To install a specific version of the Octopus CLI:

```yml
- name: Install Octopus CLI 🐙
  id: install_octopus_cli
  uses: OctopusDeploy/install-octopus-cli-action@v4
  with:
    version: 0.8.0
```

Here's an example of invoking the `account list` command after installing the Octopus CLI:

```yml
- name: Install Octopus CLI 🐙
  id: install_octopus_cli
  uses: OctopusDeploy/install-octopus-cli-action@v4
  with:
    version: 0.8.0
- name: list-octopusdeploy-accounts
  id: list_octopusdeploy_accounts
  env:
    OCTOPUS_API_KEY: ${{ secrets.apiKey }}
    OCTOPUS_URL: ${{ secrets.serverURL }}
    OCTOPUS_SPACE: 'Outer Space'
  run: >
    octopus account list
```

## 📥 Inputs

The following input is optional:

| Name      | Description                                                                                                                            |   Default    |
| :-------- | :------------------------------------------------------------------------------------------------------------------------------------- | :----------: |
| `version` | The [release](https://github.com/OctopusDeploy/cli/releases) version number of the Octopus CLI to download and install (e.g. `0.8.0`). | `*` (latest) |

## 🤝 Contributions

Contributions are welcome! :heart: Please read our [Contributing Guide](CONTRIBUTING.md) for information about how to get involved in this project.

## Privacy

This Action contacts Chainguard's licensing server to verify authorization. Connection metadata (IP address, GitHub repository identifier, timestamp, and any metadata encoded in the auth token) is transmitted to Chainguard, Inc. even if authorization is denied in accordance with our [Privacy Notice](https://www.chainguard.dev/legal/privacy-notice)
