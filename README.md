# Application my-stack
Application my-stack is a web application simulation based on simple nginx image. Docker image hello-world (https://hub.docker.com/_/hello-world)  is not suitable to be used as an application.


## Configuration
Application my-stack depends on Redis and PostgreSQL. Dependencies are defined in the **Chart.yaml file**.
Chart configuration is described in **values.yaml** file . It contains three sections, each of which describes the configuration of all chart components.

The database chart contain database passwords by default. This is possible to encrypt Helm charts with **helm-secrets** plugin, but in real life I'd recommend using Hashicorp Vault to dynamically generate and keep passwords. The these passwords can be mounted with Vault agent into a pod.

Environment variables configuration is added to **_helpers.tpl**.


## Installation
### Create namespace
Installation is supposed to be done into namespace my-stack. To create the namespace, use the command
```
kubectl create namespace my-stack
```

### Build dependencies
To prepare the chart for installation, build dependencies with command
```
helm dependency build
```

### Chart installation
Install the chart using command
```
helm -n my-stack install my-stack .
```


## Removing
To remove the chart, use command
```
helm -n my-stack delete my-stack
```
or
```
helm -n my-stack uninstall my-stack
```