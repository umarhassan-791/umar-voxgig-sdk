# Developer-experience report: Frankfurter SDK

## Selection and source

Frankfurter was selected because it is a public, no-credential exchange-rates API with an official OpenAPI 3.1 document and a compact set of useful operations. Sources: <https://frankfurter.dev/> and <https://api.frankfurter.dev/v2/openapi.json>.

On 14 October 2026, searching the Voxgig catalogue page for `Frankfurter` returned no match. A GitHub organisation search for `frankfurter-sdk` also returned no Voxgig catalogue repository. This is evidence of absence at the time checked, not a guarantee against later additions.

## Generator run

The scaffold command was `npx --yes @voxgig/create-sdkgen@0.30.7 frankfurter-sdk -o . -d .\openapi.json`. Its automatic install failed on Windows with `Failed to start npm: spawn npm ENOENT`; `.sdk` dependencies were installed with `npm.cmd install`, then the bundled generator added `ts` and `test`. `voxgig-sdkgen doctor` reported `.sdk matches the scaffold (0 additive)`.

The documented `npm run generate` resolved model-relative includes from `.sdk` rather than `.sdk/model` on this machine. Running the model from `.sdk/model` reached parsing but looked for `tm/` there. A local NTFS junction from `.sdk/model/tm` to `.sdk/tm` let the unchanged generator finish. No generated TypeScript was hand-edited.

## Results and observations

- Parsing: 4 entities, 9 paths, 9 methods.
- Generation: TypeScript completed with one `BasicRateFlow` unreachable-step warning.
- Build: `npm run build` passed.
- Offline tests: 249 total; 237 passed, 0 failed, 12 skipped, 0 todo. Skips are checks for optional features not selected.
- Live calls, credentials, and live tests were not used.

The entity surface is readable (`Currency().list()`, `Provider().load()`, `Rate().load()`), and offline definition tests cover all nine discovered operations. The main friction is Windows support: bootstrap should invoke `npm.cmd` or a shell, and model includes should resolve relative to the provided model file. The unreachable-flow warning should include an actionable model suggestion.
