# best-values-example

One of the best values parsing example charts here, exhibits several more complicated examples

![Version: 0.2.0](https://img.shields.io/badge/Version-0.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

## Additional Information

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore
et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut
aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse
cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in
culpa qui officia deserunt mollit anim id est laborum.

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm repo add foo-bar http://charts.foo-bar.com
$ helm install my-release foo-bar/best-values-example
```

Some file contents:

```
some:
  data: "test"
```

Glob contents as config map:

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: test
data:
  resource1.yaml: |-
      some:
        resource: "blah"
  resource2.yaml: |-
      some:
        resource: "blah2"
dataSecret:
  resource1.yaml: c29tZToKICByZXNvdXJjZTogImJsYWgi
  resource2.yaml: c29tZToKICByZXNvdXJjZTogImJsYWgyIg==
```

File: Chart.yaml
File: somefile.yaml
File: templates/resource1.yaml
File: templates/resource2.yaml
File: values.yaml

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| config.databasesToCreate[0] | string | `"postgresql"` | default database for storage of database metadata |
| config.databasesToCreate[1] | string | `"hashbash"` | database for the [hashbash](https://github.com/norwoodj/hashbash) project |
| config.usersToCreate[0] | object | `{"admin":true,"name":"root"}` | admin user |
| config.usersToCreate[1] | object | `{"name":"hashbash","readwriteDatabases":["hashbash"]}` | user with access to the database with the same name |
| statefulset.extraVolumes | list | `[{"emptyDir":{},"name":"data"}]` | Additional volumes to be mounted into the database container |
| statefulset.image.repository | string | `"jnorwood/postgresq"` | Image to use for deploying, must support an entrypoint which creates users/databases from appropriate config files |
| statefulset.image.tag | string | `"11"` |  |
| statefulset.livenessProbe | object | `{"enabled":false}` | Configure the healthcheck for the database |
| statefulset.podLabels | object | `{}` | The labels to be applied to instances of the database |

