# Lab 4: NerdGraph

The New Relic CLI enables running any GraphQL query or mutation against
NerdGraph without having to understand how to connect/auth/etc to the
API endpoint.

This enables early adoption of any new API query/mutation that has yet to be
added to the CLI to be used in your automation or locally.


## Requirements

* New Relic CLI v0.9.0 or later
* New Relic CLI profile configured (see [lab 1](../lab1/README.md))


## Examples

### List all available New Relic Applications

Nerdpack information is available in via the NerdGraph API, but there is no
direct support in the CLI.  You can query a list of nerdpacks, and what they do
using the following:

```bash
$ newrelic nerdgraph query \
    '{ actor { nr1Catalog { nerdpacks { metadata { displayName version tagline } } } } }'
```

### List all User API Key IDs for an Account

Management for a sub-set of API keys is now available via the API.  Here is an
example query to fetch a list of key IDs and their names:

```bash
$ newrelic nerdgraph query 'query ($accountId: Int!) {
      actor { apiAccess { keySearch(query: {types: USER, scope: {accountIds: $accountId}}) {
        keys { id name }
      }
    } } }' \
    --variables "{ \"accountId\": $NEW_RELIC_ACCOUNT_ID }"
```


