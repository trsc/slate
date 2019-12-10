---
title: Swop - Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - graphql


toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Swop - Curreny Exchange Rate API

The Swop Currency Exchange Rate API aggregates publicly available sources for exchange rate data.

# Authentication

> Passing the `Authorization` header using `curl`

```shell
curl \
  -X POST \
  -H "Authorization: ApiKey <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{ "query": "{ latest { target value }}" }'\
  https://swop.cx/graphql
```

Pass your API key using the `Authorization` header:

`Authorization: ApiKey <your-api-key>`

<aside class="notice">
You must replace <code>&lt;your-api-key&gt;</code> with your personal API key.
</aside>

If you're using the GraphQL Playground the header will be automatically set for you. Note that you will need to verify your Email address before being able to use the GraphQL Playground.

<!-- TODO add link to playgound -->

# GraphQL

All of Swop's exchange rate data is made available via a [GraphQL](https://graphql.org/) endpoint.

### Endpoint

`https://swop.cx/graphql`

### Request

`POST https://swop.cx/graphql`



## Latest Rates Query

> Retrive the latest rates from "USD" to "EUR" and "GBP"

```shell
curl \
  -X POST \
  -H "Authorization: ApiKey <your-api-key>" \
  -H "Content-Type: application/json" \
  -d '{ "query": "{ latest(base: \"USD\", targets: [\"EUR\", \"GBP\"]) { base target value }}" }'\
  https://swop.cx/graphql
```


```graphql
query {
  latest(base: "USD", targets: ["EUR", "GBP"]) {
    base
    target
    value
  }
}
```

> The response will look like this

```json
{
  "data": {
    "latest": [
      {
        "base": "USD",
        "target": "EUR",
        "value": 0.902935
      },
      {
        "base": "USD",
        "target": "GBP",
        "value": 0.760226
      }
    ]
  }
}
```

This query retrieves the latest available exchange rate data. You can specify a `base` and also limit the returned `targets`.

### Query

`latest`

### Query Parameters

Parameter | Type | Optional? | Default | Description
--------- | ---- | --------- | ------- | -----------
base | String | true | EUR | Specifies the base currency
targets | [String!] | true |  all available target currencies | Only retrieve rates of the specified targets
