# Reproduction case for backstage/backstage#20174

See https://github.com/backstage/backstage/issues/20174

## How to reproduce

1. Checkout this repo
1. Run `yarn install`
1. Run `yarn backstage-cli config:print --lax --config test-config.yaml`

## Expected

```
Loaded config from test-config.yaml
app:
  baseUrl: x
backend:
  listen: 5000
  baseUrl: x
  database:
    client: better-sqlite3
    connection: <secret>
techdocs:
  builder: local
integrations:
  azure:
    - host: test
      credentials:
        - clientSecret: <secret>
    - host: dev.azure.com
      credentials:
        - organizations:
            - my-org
          personalAccessToken: <secret>
        - organizations:
            - my-other-org
          clientSecret: <secret>
```

## Actual

```
Loaded config from test-config.yaml
app:
  baseUrl: x
backend:
  listen: 5000
  baseUrl: x
  database:
    client: better-sqlite3
    connection: <secret>
techdocs:
  builder: local
integrations:
  azure:
    - host: test
      credentials:
        - clientSecret: azure-client-secret
    - host: dev.azure.com
      credentials:
        - organizations:
            - my-org
          personalAccessToken: azure-pat
        - organizations:
            - my-other-org
          clientSecret: azure-client-secret
```

## Additional information

This repo was created via `npx @backstage/create-app@latest`.
Node.js version v18.17.1
