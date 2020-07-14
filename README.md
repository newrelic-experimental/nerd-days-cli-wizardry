# Nerd Days: Reducing toil with Terraform

## Requirements

To get the most value out of the following, you should have a basic understanding of shell scripting, and a New Relic account that you can test with.

* [New Relic CLI](https://github.com/newrelic/newrelic-cli#installation) version 0.9.0 or later
* New Relic Account
  * Application reporting to New Relic


## References

* [Getting Started Guide](https://github.com/newrelic/newrelic-cli/blob/master/docs/GETTING_STARTED.md)
* [Documentation](https://github.com/newrelic/newrelic-cli/blob/master/docs/cli/newrelic.md)
* [Source Repo](https://github.com/newrelic/newrelic-cli)

The CLI also has build-in help, simply run `newrelic help` to get more
information.


## Setup

* These labs require that you already have a New Relic agent deployed. If you don't have New Relic integrated yet, check out [New Relic's introduction documentation](https://docs.newrelic.com/docs/using-new-relic/welcome-new-relic/get-started/introduction-new-relic) to get started there, then head back over here to get started with the New Relic Terraform Provider using the examples provided.
* [Install the New Relic CLI](https://github.com/newrelic/newrelic-cli#installation) and read the [getting started guide](https://github.com/newrelic/newrelic-cli/blob/master/docs/GETTING_STARTED.md). This guide will assume a basic understanding of shell scripting.
* Locate your Personal API key by following [New Relic's Personal API key docs](https://docs.newrelic.com/docs/apis/get-started/intro-apis/types-new-relic-api-keys#personal-api-key).

## Environment

You can either create a profile for yourself, or store secrets in Environment
variables.  **Note:** Environment variables take precedence! If you're having
unexpected access issues, ensure that the environment is set correctly or
unset!

### Environment setup for bash:

```bash
export NEW_RELIC_API_KEY=
export NEW_RELIC_REGION="US"   # or "EU"
```


## Instructions

* [Lab 1](lab1/README.md): Profiles
* [Lab 2](lab2/README.md): Entities
* [Lab 3](lab3/README.md): NRQL
