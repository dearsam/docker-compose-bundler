# docker-compose-bundler

Internal tool used to bundle our Vue Storefront installations with.

## Usage
```
yarn add --dev @kodbruket/docker-compose-bundler
yarn docker-compose-bundler [-e environment]
```

Make sure both `docker-compose.yml` and `docker-compose.override.yml` exists. Both must have the `services` key. Also need the `bundle` label which will be the bundle folder.

## Example
```
version: '3.4'
services:
  api:
    labels:
      bundle: "vue-storefront-api"
  ui:
    labels:
      bundle: "vue-storefront"
```

In this example `ui` will be bundled to `.output/vue-storefront/`.

## Config bundling

If the following are true:
* environment is either `staging` or `production`
* if you have a mounted config file called `base.json` (example: `- './frontend/config/base.json:/var/www/config/local.json'`)
* if the selected environment file exists (e.g. `./frontend/config/staging.json` when `environment=staging`)

then the output file (`/var/www/config/local.json`) will be the result of merging `staging.json` on `base.json` using `deepmerge`

## Context

`service.context` will be used as a base 