# Frankfurter SDK assessment

An unofficial TypeScript SDK generated with Voxgig SDK Generator for the [Frankfurter exchange-rates API](https://frankfurter.dev/). It exposes coverage, currencies, providers, and exchange rates as generated entities.

- Official API: <https://frankfurter.dev/>
- Official OpenAPI document: <https://api.frankfurter.dev/v2/openapi.json>
- Generator: <https://github.com/voxgig/sdkgen>
- Generated package: [`ts/`](ts/)

## Generation and local use

The checked-in model and source were produced from `openapi.json` using `@voxgig/create-sdkgen` 0.30.7 and `@voxgig/sdkgen` 4.34.5, with the `ts` target and `test` feature. The source of truth is `.sdk/model/`; do not hand-edit generated `ts/` files. Node.js 24 or later is required.

```powershell
cd ts
npm install
npm run build
npm test
```

## Usage

The API is public and the generated model declares no authentication. No API key or environment variable is needed. This actual generated API example uses test mode and makes no live call.

```ts
import { FrankfurterSdkSDK } from './ts/dist/FrankfurterSdkSDK.js'

const client = FrankfurterSdkSDK.test()
const currencies = await client.Currency().list()
console.log(currencies.map((currency) => currency.data()))
```

For live use, construct `new FrankfurterSdkSDK()` and call an entity method such as `client.Currency().list()`. See [`ts/README.md`](ts/README.md) and [`ts/REFERENCE.md`](ts/REFERENCE.md). Live requests were not run.

## Limitations

Only TypeScript and the offline test feature were selected. Generation emitted a `BasicRateFlow` unreachable-step warning. The generated offline suite covers all nine parsed HTTP operations. See [DX_REPORT.md](DX_REPORT.md) for results and workflow findings.

## License

MIT. Upstream notices remain in `NOTICE`.
