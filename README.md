# crowsi-network-observer

Read network-state metadata and produce a bounded observation for review.

## What you can do

- Inspect configured observation inputs.
- Return a structured network-state snapshot.

## Current scope

Observation is read-only. The output does not authorize network changes.

Package distribution is not activated by this documentation. Use the checked-in source and the declared dependency versions; published availability must be verified separately.

## Getting started

Install Rust 1.97 or newer and make the declared dependencies available. Use the configured private registry when a dependency is not distributed publicly. Run from this repository:

```sh
cargo test --locked
```

## Examples and interface details

## Commands

```bash
cargo run -- sample
cargo run -- observe
cargo run --example sample
cargo test
```

`sample` always emits the checked-in contract example. `observe` reads local
interface metadata and emits `crowsi://network/observations/v1`. Both set
`external_actions` to `false`.

## Contract policy

- Consumers select behavior from `schema`, never from repository layout.
- Unknown JSON fields are rejected when the contract is deserialized.
- Nullable latency and loss mean the probe did not measure those properties.
- New incompatible fields require a new contract URI.

## Documentation and source

[Interface reference](docs/interface-reference.md)

[Usage guide](docs/getting-started.md)

[Examples](examples) · [Schemas](schemas) · [Implementation and public interfaces](src) · [Verification cases](tests) · [Contributing](CONTRIBUTING.md) · [Security reporting](SECURITY.md) · [License](LICENSE) · [Attribution notices](NOTICE)
