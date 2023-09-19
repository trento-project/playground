# Trento Playground

A simple setup delivering a local trento playground that lets you control its behaviors.

It targets whoever wants to try or showcase trento features, with the ability to instrument the system to behave in a certain way.

PMs, POs, presales engineers, etc... 

## Dependencies

In order to leverage this playground make sure to have installed
- `Docker`
- `Docker Compose`
- `make`

### Windows users
Install [Docker Desktop](https://docs.docker.com/desktop/install/windows-install/) and/or leverage [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

### Mac users
Playground allows to override the docker compose configuration to allow the explicit specification of the image platform for usage on Mac.

Copy the `docker-compose.override.yaml.dist` file to `docker-compose.override.yaml`.

```bash
$ cp docker-compose.override.yaml.dist docker-compose.override.yaml
```

The default content of the compose override file already specifies `linux/amd64` as the platform for the `trento-web` and `wanda` services
```yaml
services:
  trento-web:
    platform: linux/amd64

  wanda:
    platform: linux/amd64
```


## Usage

1. clone the current repository
2. enter in the directory
3. run [commands](#commands)

```bash
$ git clone git@github.com:trento-project/playground.git
$ cd playground
$ make
```

## Commands

Run `make` or `make help` to see the list of available commands.

```bash
Usage:
 make [target]
 make [target] [args]

Available targets:
 help:                    Help
 clean:                   Cleans up local setup
 get-scenarios:           Prepares photofinish scenarios
 get-catalog:             Prepares Checks catalog
 get-facts-config:        Prepares fake facts configuration
 start:                   Starts containers
 load-default-scenario:   Loads default photofinish scenario healthy-27-node-SAP-cluster
 load-scenario:           Loads a specific photofinish scenario by name. Usage: make load-scenario scenario=<scenario-name>
```

### Getting started

Run `make start` to initialize the local environment. 

What this command does:
- get photofinish scenarios
- get a local copy of the checks catalog
- get a local copy of the fake facts configuration
- start containers

> Note that `start` keeps the terminal busy, so that when hitting `CTRL+C` the containers are shut down.
> 
> Open other terminal to run further commands.

Hang tight and wait until everything is ready...

When ready browse to http://localhost:4000 and log in with the following credentials: user `admin`, password `adminpassword`

### Environment variables

It is possible to customize the playground by setting environment variables.

Copy the `.env.dist` file to `.env` and edit it as per the specific needs.

```bash
$ cp .env.dist .env
```

See [.env.dist](./.env.dist) for a list of available variables.

#### Changing the images tags

By default `demo` images are used for weba nd wanda containers.
Edit the `.env` file to use a different tag.

Example
```bash
WEB_IMAGE_TAG=2.1.0 # a specific release tag
# WEB_IMAGE_TAG=1790-env # a PR branch tag ${PR_NUMBER}-env
WANDA_IMAGE_TAG=rolling
```

### Loading photofinish scenarios

Scenarios are loaded with [photofinish](https://github.com/trento-project/photofinish). 

With containers up and ready, run `make load-default-scenario` to load the default `healthy-27-node-SAP-cluster` scenario.

Run `make load-scenario scenario=<scenario-name>` to run any of the available scenarios. ie: `make load-scenario scenario=aws-landscape`

Take a look at [./data/photofinish/.photofinish.toml](./data/photofinish/.photofinish.toml) for extra information about scenarios and scenarios names.

### Catalog

After the setup, the whole community catalog is available for experimentation in [./data/catalog/](./data/catalog/).

Any changes to the existing checks, newly added checks or removed ones are reflected in the running instance.

### Facts Gathering

After the setup, also a configuration file useful to instrument what target agents should return during facts gathering is available at [./data/facts-gathering/fake_facts.yaml](./data/facts-gathering/fake_facts.yaml).

Any changes to the file are reflected in the running instance.

Please see [Wanda demo doc](https://github.com/trento-project/wanda/blob/main/guides/development/demo.md#modify-demo-facts-configuration) for extra information about the file format.