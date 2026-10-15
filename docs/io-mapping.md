# Legacy-to-5069 I/O Mapping

## Why the Mapping Layer Exists

The SLC migration preserved legacy output-word behavior but did not directly bind those internal words to the new 5069 physical outputs.

A dedicated routine, `_6_IO_Map`, was added so the original program flow could remain largely intact while the hardware layer changed.

## Mapping Pattern

```text
Slot1_OutputWord.0  ->  Local:1:O.Pt00.Data
Slot1_OutputWord.1  ->  Local:1:O.Pt01.Data
...
Slot2_OutputWord.0  ->  Local:2:O.Pt00.Data
...
Slot3_OutputWord.15 ->  Local:3:O.Pt15.Data
```

This produces a clear separation between:

- migrated machine logic
- legacy compatibility data
- physical 5069 I/O

## Verified Functional Aliases

Examples of readable aliases added during cleanup include:

- `DO_RunIndicator`
- `DO_RunRelay`
- `DO_HeatShield_Open`
- `DO_HeatShield_Closed`
- `DO_Feeder_Advance`
- `DO_Feeder_Retreat`
- `DO_Rotation_On`
- `DO_Oscillation_Step`
- `DO_Bridge_Advance`
- `DO_Bridge_Retreat`
- `DO_Heater_Low`
- `DO_Heater_Medium`
- `DO_Heater_High`
- `DI_CoaterReady`
- `DI_AdvanceStep`
- `DI_Restart`

## Documentation Rule

For verified points, the physical I/O description should use the known machine function.

For unknown or not-yet-field-verified points, use a neutral description such as:

`Legacy Slot 1 Output Bit 2 - Field Function TBD`

The public portfolio intentionally avoids inventing functions for unverified I/O.