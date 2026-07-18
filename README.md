# Nordlet TypeScript Library

[![fern shield](https://img.shields.io/badge/%F0%9F%8C%BF-Built%20with%20Fern-brightgreen)](https://buildwithfern.com?utm_source=github&utm_medium=github&utm_campaign=readme&utm_source=Nordlet%2FTypeScript)
[![npm shield](https://img.shields.io/npm/v/nordlet)](https://www.npmjs.com/package/nordlet)

The Nordlet TypeScript library provides convenient access to the Nordlet Accounting API from TypeScript and JavaScript (Node.js ≥ 18, browsers, and edge runtimes — anywhere `fetch` is available).

## Installation

```sh
npm install nordlet
```

## Usage

Instantiate the client with your API key and call any endpoint:

```ts
import { NordletApiClient } from "nordlet";

const client = new NordletApiClient({ token: "nl_..." });

const invoice = await client.sales.postV1SalesInvoicesCreate({
    partnerId: "partner-id",
    lines: [{ description: "Consulting", quantity: 4, unitPriceExclVat: "75.0000" }],
});
```

Every operation is `POST /v1/{module}/{resource}/{action}`; monetary amounts are decimal strings, never floats.

## Environments and custom base URL

The client defaults to production (`https://api.nordlet.com`). Point it elsewhere with `environment` or `baseUrl`:

```ts
import { NordletApiClient } from "nordlet";

const client = new NordletApiClient({
    token: "nl_...",
    baseUrl: "http://localhost:3001",
});
```

## Retries and timeouts

Requests are retried twice by default with exponential backoff. Configure per client or per request:

```ts
const client = new NordletApiClient({ token: "nl_...", maxRetries: 0, timeoutInSeconds: 30 });

await client.sales.postV1SalesInvoicesList({}, { maxRetries: 5, timeoutInSeconds: 60 });
```

## Documentation

The full API reference lives at [docs.nordlet.com](https://docs.nordlet.com) — every endpoint, request/response schema, error envelope, idempotency and webhook conventions.

## Contributing

This SDK is generated from the Nordlet OpenAPI specification; releases are cut automatically and any manual change here would be overwritten. Open issues and suggestions on the [GitHub repository](https://github.com/nordlet/nordlet-sdk-typescript).
