# External References

This repo is the domain implementation for incident/dispatch management. Blockchain anchoring and
cross-device sync are delegated to a separate, generic wallet — not duplicated here.

| Repo | What it's for | This repo's integration point |
|---|---|---|
| [`../wallet`](../wallet) | Generic offline/online BSV wallet with a protocol-adapter layer | Integrate via [`PROTOCOL_ADAPTER_SPEC.md`](../wallet/PROTOCOL_ADAPTER_SPEC.md) — implement `ProtocolAdapter` and self-register by `id`/`tags`/`discoveryMetadata`, no naming coupling required. The wallet's own `IncidentAdapter` (`../wallet/src/adapters/incident-adapter.ts`) mirrors this domain's incident lifecycle (create → update-status → close → dispatch-resource → anchor-evidence) as a worked example, not a dependency. |

See [`../wallet/REFERENCES.md`](../wallet/REFERENCES.md) for the wallet's own external-reference catalog (BSV SDKs, sCrypt examples, BRC-100/Paymail research).

## This repo's own functions

[`docs/readme-functions.md`](docs/readme-functions.md) maps every implemented `IncidentManager` /
`DispatchManager` / `ResourceManager` method (legacy-equivalent and blockchain-native) with a mermaid
sequence diagram per function — §13-17 cover the functions that exist in code but had no legacy
counterpart to map against (`reopenIncident`, `addFieldNotes`, `autoDispatch`, `cancelDispatch`,
`ResourceManager.updateStatus/batchUpdateLocations/findNearestAvailable/release`).
