# Tasks

The `tasks` here are designed to be consumed via remote task includes in a single root level `tasks.yaml` in the downstream repo. Includes should follow the standard remote include pattern documented by UDS CLI:

```yaml
includes:
  - deploy: https://raw.githubusercontent.com/defenseunicorns/uds-common/$TAG/tasks/deploy.yaml
```

Pinning to a specific tag of a task (rather than `main`) with renovate watching for updates is **strongly recommended** since tasks do rely on dependencies like command syntax for `zarf` and `uds` as well as the published versions of `uds-core`.

## Supported Tool Versions

- UDS CLI: 0.17.0
- UDS Core: 0.27.3
- K3D: 5.7.4
- Lula: 0.7.0

> [!NOTE]
> Zarf is not required for tasks in this repo, the vendored zarf (`uds zarf`) included with UDS CLI is used instead to prevent version mismatches.

## Task Files

There are multiple task files available in this repository with different objectives and required variables.

### [setup.yaml](./tasks/setup.yaml)

| Name | Description |
|------|-------------|
| **k3d-test-cluster** | Creates a k3d cluster for testing based on the K3d + UDS Core Slim Dev bundle |
| **k3d-full-cluster** | Creates a k3d cluster for testing based on the K3d + UDS Core Full bundle |
| **print-keycloak-admin-password** | Print the default keycloak 'admin' password to standard out (if INSECURE_ADMIN_PASSWORD_GENERATION was used on uds-core) |
| **create-doug-user** | Creates a user named 'doug' in the uds realm of keycloak (using the default admin account) |

### [create.yaml](./tasks/create.yaml)

| Name | Description |
|------|-------------|
| **package** | Create the UDS Zarf Package in the repository |
| **test-bundle** | Create the test bundle (bundling package + dependencies for testing) |

### [deploy.yaml](./tasks/deploy.yaml)

| Name | Description |
|------|-------------|
| **package** | Deploy the created UDS Zarf Package |
| **test-bundle** | Deploy the created test bundle (deploying package + dependencies for testing) |

### [remove.yaml](./tasks/remove.yaml)

| Name | Description |
|------|-------------|
| **test-bundle** | Remove the deployed test bundle |

### [publish.yaml](./tasks/remove.yaml)

| Name | Description |
|------|-------------|
| **package** | Publish the UDS package for the supplied architecture |
| **test-bundle** | Publish the test bundle for the supplied architecture |

### [pull.yaml](./tasks/remove.yaml)

| Name | Description |
|------|-------------|
| **latest-package-release** | Pull the last release of the UDS Package (useful for upgrade testing) |
| **latest-bundle-release** | Pull the last release of the UDS Bundle (useful for upgrade testing) |

### [upgrade.yaml](./tasks/upgrade.yaml)

| Name | Description |
|------|-------------|
| **create-latest-tag-bundle** | Creates the test bundle at the latest tag in preparation for upgrade testing |

### [utils.yaml](./tasks/utils.yaml)

| Name | Description |
|------|-------------|
| **determine-repo** | Determines the OCI repository that this flavor should go into (i.e. 'unicorn' should be private) |

### [lint.yaml](./tasks/lint.yaml)

| Name | Description |
|------|-------------|
| **deps** | Install linting tool dependencies |
| **yaml** | Run YAML linting checks |
| **oscal** | Run linting checks on OSCAL |

### [badge.yaml](./tasks/badge.yaml)

| Name | Description |
|------|-------------|
| **verify-badge** | Verifies that a UDS Package implements UDS Package Practices flagging things that are out of compliance |

### [compliance.yaml](./tasks/compliance.yaml)

| Name | Description |
|------|-------------|
| **validate** | Lula Validate OSCAL Compliance |
| **evaluate** | Lula Evaluate multiple OSCAL Assessment Results |