# Controls Architecture

## Modernized Platform

The migrated system uses a **CompactLogix 5380 (5069-L306ER)** controller with local 5069 I/O and a PanelView Plus 7 HMI target.

### Controller and I/O

- CompactLogix 5380 controller
- 5069 relay output modules
- 5069 AC input module
- Local 5069 backplane
- Dedicated legacy-to-physical I/O mapping routine

## Network Design

The 5380 dual Ethernet interfaces were used as separate networks during development and commissioning.

- **A1** — isolated machine/HMI network
  - controller
  - PanelView Plus 7
  - engineering workstation during commissioning
- **A2** — separate engineering / future plant-integration network

This keeps the machine network independent while preserving a path for later plant integration.

> Exact production IP addresses and host identifiers are intentionally omitted from this public portfolio.

## Design Intent

The migration was structured in layers:

```text
Operator/HMI Layer
        |
        v
Sequence / Program Logic
        |
        v
Legacy Compatibility Tags
        |
        v
_6_IO_Map
        |
        v
5069 Physical I/O
```

This approach minimizes unnecessary changes to validated sequence logic while modernizing the hardware and communications layers.