# Crowsi Network Observer

`crowsi-network-observer` is the read-only observation boundary for Crowsi.
It exposes a small Rust probe interface and a closed JSON contract that a Nuxt
client can consume without depending on this repository's source.

The bundled system probe reads Linux `/proc/net/dev` as an unprivileged user.
The production probe has no configurable path and rejects non-regular sources.
It reports only the presence of network interfaces. It does not emit byte
counters, addresses, packet bodies, environment variables, or credentials.
The deterministic sample probe performs no I/O.

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

## Embedding a probe

Implement `NetworkProbe` and create records with
`NetworkObservationV1::try_new(NetworkObservationInputV1)`. Output fields are
private so invalid records cannot later be mutated and serialized. Use `collect`
to validate cross-record uniqueness and collection limits before sorting and
calculating the declared count. A probe is responsible for observation only;
remediation belongs to a separately authorized controller.

## Contract policy

- Consumers select behavior from `schema`, never from repository layout.
- Unknown JSON fields are rejected when the contract is deserialized.
- Nullable latency and loss mean the probe did not measure those properties.
- New incompatible fields require a new contract URI.
