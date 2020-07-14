# Lab 1: Profiles

The New Relic CLI enables you to store multiple profiles for accessing
different accounts / using different API keys.

## Requirements

* New Relic CLI v0.9.0 or later

## Steps

1. Creating a new Profile

   ```bash
   # Add a new Profile (not needed if you have one already)
   $ newrelic profile add \
     --name wizardry \
     --apiKey $NEW_RELIC_API_KEY \
     --region $NEW_RELIC_REGION
   ```

1. Set the new profile as your default

   ```bash
   # Set the new profile as a default
   $ newrelic profile default \
     --name wizardry
   ```

1. View profiles

   ```bash
   $ newrelic profile list

   Name                    Region  APIKey
   ----------------------- ------- --------
   wizardry (default)      US      <hidden>
   ```

1. Unset environment variables (if they were set)

   ```bash
   unset NEW_RELIC_API_KEY
   unset NEW_RELIC_REGION
   ```

