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

For other means of using make on windows, google will help: `install make on windows`

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

Hang tight and wait a good 5 minutes for everything to be ready...

When ready browse to http://localhost:4000 and log in with the following credentials: user `admin`, password `adminpassword`

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