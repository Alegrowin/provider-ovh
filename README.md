# Provider OVH

`provider-ovh` is a [Crossplane](https://crossplane.io/) provider that
is built using [Upjet](https://github.com/crossplane/upjet) code
generation tools and exposes XRM-conformant managed resources for the
OVH API.

## Prerequisites

* Install [up CLI](https://github.com/upbound/up?tab=readme-ov-file#install)
* Install [Crossplane in your cluster](https://docs.crossplane.io/latest/software/install/)

## Getting Started

Install the provider by using the following command:
```
up ctp provider install alegrowin/provider-ovh
```

Alternatively, you can use declarative installation:
```
cat <<EOF | kubectl apply -f -
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: provider-ovh
spec:
  package: alegrowin/provider-ovh
EOF
```

If you want to specify a version of the provider, add an image tag
to the [latest release](https://marketplace.upbound.io/providers/edixos/provider-ovh).
Example:
`alegrowin/provider-ovh:v.1.2.0`

Notice that in this example Provider resource is referencing ControllerConfig with debug enabled.

You can see the API reference [here](https://doc.crds.dev/github.com/alegrowin/provider-ovh).

## Developing

Run code-generation pipeline:
```console
go run cmd/generator/main.go "$PWD"
```

Run against a Kubernetes cluster:

```console
make run
```

Build, push, and install:

```console
curl -sL "https://cli.upbound.io" | sh
curl -sL "https://cli.upbound.io" | BIN=docker-credential-up sh
curl -sL "https://raw.githubusercontent.com/crossplane/crossplane/main/install.sh" | sh

sudo mv docker-credential-up /usr/local/bin/
sudo mv up /usr/local/bin/
sudo mv crossplane /usr/local/bin

docker-credential-up -v
up version
crossplane --help

code ~/.docker/config.json 
  "credHelpers": {
    "xpkg.upbound.io": "up"
  }

up login
make build.all
make publish
```

Build binary:

```console
make build
```

## Report a Bug

For filing bugs, suggesting improvements, or requesting new features, please
open an [issue](https://github.com/alegrowin/provider-ovh/issues).



