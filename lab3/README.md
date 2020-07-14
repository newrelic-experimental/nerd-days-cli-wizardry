# Lab 3: NRQL

The New Relic CLI enables fetching of any data from NRDB via NRQL queries.

**Note:** NRQL queries are always account scoped, so you must provide an
accountId for each query.  You can run the same query against multiple
accounts by wrapping the command in another script.

## Requirements

* New Relic CLI v0.9.0 or later
* New Relic CLI profile configured (see [lab 1](../lab1/README.md))


## Examples

### Simple count

Fetch the number of transactions in the last hour

```bash
$ newrelic nrql query \
    --accountId $NEW_RELIC_ACCOUNT_ID \
    --query 'FROM Transaction SELECT count(*) SINCE 1 hour ago'
```


### Identify Event Types

List all of the event types that are reporting to the specific account

```bash
$ newrelic nrql query \
    --accountId $NEW_RELIC_ACCOUNT_ID \
    --query 'SHOW eventtypes'
```


### Find all of the Attributes on an EventType

NRDB is schema-less, so it can be useful to lookup what the latest set of
attributes on an Event Type happen to be.  Or perhaps you're working on a query
but can not remember the attribute name you want to Facet on.

```bash
$ newrelic nrql query \
    --accountId $NEW_RELIC_ACCOUNT_ID \
    --query 'FROM NrAuditEvent SELECT keyset() SINCE 1 month ago'
```


### Count audit events in the last week

Specific actions create audit events that can be queried. To get a quick view
of what's happening, try the following query:

```bash
$ newrelic nrql query \
    --accountId $NEW_RELIC_ACCOUNT_ID \
    --query 'FROM NrAuditEvent SELECT count(*) FACET targetType SINCE 1 week ago'
```

## Advanced Combos

These may / may not work depending if you have other utilities installed.

* [jq](https://stedolan.github.io/jq/) - Lightweight and flexible command-line JSON processor
* [awk](https://en.wikipedia.org/wiki/AWK) - pattern-directed scanning and processing language
* [xargs](https://en.wikipedia.org/wiki/Xargs) - construct argument list(s) and execute utility


### Calculate Apdex for APM Applications with the default

This is a solid chunk...

1. Fetch list of reporting APM Applications for a specific account (`newrelic`)
1. Filter the results down to those that have a default `apdexTarget` (i`jq`)
1. Build a new NRQL query to fetch `appId, appName, average request duration` (`awk`)
1. Create new queries againts New Relic (`xargs`)
1. Fetch the requested data (`newrelic`)

```bash
$ newrelic entity search \
      --domain APM \
      --type APPLICATION \
      --reporting true \
      --tag "accountId:$NEW_RELIC_ACCOUNT_ID" | \
    jq '.[]|select(.settings.apdexTarget==0.5)|.applicationId' | \
    awk '{ print "\"FROM Transaction SELECT uniques(appId), uniques(appName), average(duration) WHERE appId = " $1 " SINCE 1 week ago\"" }' | \
    xargs -n 1 \
      newrelic nrql query \
        --accountId $NEW_RELIC_ACCOUNT_ID \
        --query
```
