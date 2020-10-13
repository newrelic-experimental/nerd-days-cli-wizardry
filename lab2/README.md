# Lab 2: Entities

Using the New Relic CLI you can easily search for entities.

## Requirements

* New Relic CLI v0.9.0 or later
* New Relic CLI profile configured (see [lab 1](../lab1/README.md))

## Examples

### Search for an entity by Name

```bash
# Replace WebPortal with a name in your environment
$ newrelic entity search \
    --name WebPortal
```


### Filter down to APM Applications

```bash
# Replace WebPortal with a name in your environment
$ newrelic entity search \
    --name WebPortal \
    --domain APM \
    --type APPLICATION
```


### Seach for any APM Applications on a specific account that have critical alerts

```bash
$ newrelic entity search \
    --domain APM \
    --type APPLICATION \
    --alert-severity CRITICAL \
    --tag "accountId:$NEW_RELIC_ACCOUNT_ID"
```


### Get a list of tags for an entity

```bash
# Replace the GUID below with a value from entity search
$ newrelic entity tags get \
   --guid MTYwNjg2MnxBUE18QVBQTElDQVRJT058NDMxOTIyMTA
```


## Advanced Combos

These may / may not work depending if you have other utilities installed.

* [jq](https://stedolan.github.io/jq/) - Lightweight and flexible command-line JSON processor

### Search for Applications with default Apdex

The default Apdex setting for an APM application is 500ms, or 0.5 seconds as
returned by NerdGraph  The following example:

* Fetches all APM Applications on the specified account
* Filters the result set through `jq` for those with apdexTarget == 0.5

```bash
$ newrelic entity search \
      --domain APM \
      --type APPLICATION \
      --tag "accountId:$NEW_RELIC_ACCOUNT_ID" | \
    jq '.[]|select(.settings.apdexTarget==0.5)'
```

