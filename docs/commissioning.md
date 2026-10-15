# Bench Commissioning and Validation

## Validation Sequence

The modernized controller was commissioned on the bench before field deployment.

- Verified controller project: **0 errors / 0 warnings**.
- Confirmed controller discovery in FactoryTalk Linx / Studio 5000.
- Tested both controller Ethernet interfaces independently.
- Performed the first full project download to the CompactLogix 5380.
- Confirmed download completed successfully with no download errors.
- Placed the controller into **Remote Run**.
- Confirmed **Controller OK**.
- Confirmed **I/O OK**.
- Confirmed **No Forces**.
- Monitored live sequence, timer, input, and output values using Studio 5000 Watch.

## Watch-Table Strategy

The bench checkout used grouped watch views similar to watch tables used in other PLC platforms.

### Sequence

- `Program_Selected`
- `Program_Active`
- `Step_Current`
- `Step_Requested`
- `T4[0].PRE`
- `T4[0].ACC`

### Inputs

- `DI_CoaterReady`
- `DI_AdvanceStep`
- `DI_Restart`

### Outputs

- `Slot1_OutputWord`
- `Slot2_OutputWord`
- `Slot3_OutputWord`
- selected `Local:X:O.PtYY.Data` points

## Why Bench Validation Matters

Running the migrated application on the actual target controller before field cutover exposes conversion, I/O configuration, communications, and execution problems without putting production equipment at risk.