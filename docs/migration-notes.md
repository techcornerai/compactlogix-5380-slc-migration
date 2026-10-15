# Migration Notes

## Conversion Philosophy

The objective was not to rewrite a working machine from scratch. The migration preserved the original machine behavior where practical and isolated modernization changes into clear compatibility and hardware layers.

## Key Issues Resolved

### Timer-base differences

Legacy SLC timers may use time bases that do not translate directly to Logix timer presets. Timer behavior was validated against the original project and corrected for Logix millisecond timing.

### COP source references

Some converted `COP` instructions referenced arrays in a way that Logix 5000 would not accept. Explicit starting elements were added where required.

### Migration placeholder instructions

The conversion introduced placeholder/error instructions that identified logic requiring engineering review. Those locations were reviewed against the original SLC behavior and cleaned after validation.

### Legacy output words

The migrated program retained legacy output words for compatibility, but the new 5069 output modules required explicit mapping. The `_6_IO_Map` routine provides that interface.

### Readability

Readable aliases were added for key legacy tags and physical points so technicians do not have to troubleshoot solely from raw `B3`, `N7`, `T4`, `C5`, and `Local:` references.

## Engineering Principle

A successful PLC migration requires more than a project that compiles. The conversion must preserve machine intent, timing, operator interaction, physical I/O behavior, and maintainability.