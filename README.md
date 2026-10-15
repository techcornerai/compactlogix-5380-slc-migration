# Legacy SLC 500 to CompactLogix 5380 Modernization

A controls-engineering modernization project documenting the migration of a legacy Allen-Bradley SLC 500–based machine control system to a CompactLogix 5380 platform with 5069 I/O, modern Ethernet/IP communications, and a redesigned PanelView Plus 7 HMI.

> **Portfolio note:** This repository is intentionally sanitized for public use. Customer, employer, machine-identifying, serial-number, workstation, credential, and plant-network details are omitted or generalized.

## Project Summary

The original machine used a legacy SLC 500 controller, PanelView Standard HMI, timer/counter data files, integer and binary file addressing, and discrete I/O organized around legacy slot words. The modernization objective was to preserve machine behavior while moving the controls architecture to a current Rockwell platform that is easier to support, troubleshoot, and expand.

The migrated system was bench-validated on a **5069-L306ER CompactLogix 5380** controller with **5069 discrete I/O** and a **PanelView Plus 7** target.

## What I Delivered

- Converted and cleaned legacy SLC 500 logic for Logix 5000 execution.
- Preserved the original program-selection and machine-sequence behavior.
- Reworked legacy timer handling to account for SLC versus Logix time-base differences.
- Corrected migrated COP array references and other conversion artifacts.
- Removed obsolete migration placeholder instructions after validation.
- Created readable alias tags for legacy data-file and physical I/O references.
- Built a dedicated `_6_IO_Map` routine that maps legacy output-word bits to physical 5069 output points.
- Redesigned the PanelView application for PanelView Plus 7 / FactoryTalk View ME.
- Added maintenance access and technician-focused navigation.
- Implemented a dual-network architecture using the CompactLogix 5380 dual Ethernet interfaces.
- Verified communications over both controller Ethernet interfaces.
- Completed a clean controller verification with **0 errors and 0 warnings**.
- Successfully downloaded the migrated application to the CompactLogix 5380.
- Placed the controller in **Remote Run** and confirmed **Controller OK**, **I/O OK**, and **No Forces** during bench validation.
- Built online watch views for sequence, timer, input, and output commissioning.

## Architecture

```text
Legacy System

SLC 500 PLC
   |
   +-- Legacy discrete I/O
   |
   +-- PanelView Standard / legacy communications

               MIGRATION
                  |
                  v

Modernized System

CompactLogix 5380 (5069-L306ER)
   |
   +-- 5069-OW16/A relay output modules
   +-- 5069-IA16/A AC input module
   |
   +-- A1: isolated machine/HMI Ethernet network
   |      +-- PanelView Plus 7
   |      +-- engineering access during commissioning
   |
   +-- A2: separate engineering / future plant integration network
```

Exact production IP addresses are intentionally not published.

## Key Migration Challenges

### Legacy data-file addressing
The SLC application relied heavily on references such as `B3`, `N7`, `T4`, and `C5`. The conversion preserved these structures where useful, while readable aliases were added for technician-facing logic and diagnostics.

### Timer conversion
The original SLC program used timer behavior based on legacy timer time bases. Logix timers use millisecond presets, so timer logic had to be validated rather than accepted blindly from the migration tool.

### COP array syntax
Converted COP instructions contained source references that did not compile correctly in Logix 5000 until explicit array starting elements were used.

### Legacy output words versus physical 5069 outputs
The migration preserved internal output words, but those words did not automatically drive the new 5069 physical output points. A dedicated mapping routine was created so the original machine logic could remain intact while the hardware layer changed.

Example concept:

```text
Legacy output word bit
        |
        v
Slot1_OutputWord.0
        |
        v
_6_IO_Map
        |
        v
Local:1:O.Pt00.Data
        |
        v
5069 physical output
```

This separation keeps the migrated sequence logic readable and makes field troubleshooting much easier.

## HMI Modernization

The legacy PanelView Standard project was converted and rebuilt for FactoryTalk View Machine Edition and PanelView Plus 7. The new HMI work included:

- 640 × 480 PanelView Plus 7 target layout.
- Modernized primary operator display.
- Program selection and numeric step-entry functions.
- Stop/Run, Previous Step, Next Step, and Go To Step controls.
- Maintenance-only access to configuration functions.
- Technician-focused troubleshooting and diagnostics planning.
- Direct Ethernet/IP architecture for the modernized controller/HMI system.

## Bench Validation

The migrated controller project was validated in stages:

1. Controller verification completed with **0 errors / 0 warnings**.
2. Both Ethernet interfaces were configured and tested independently.
3. The project was downloaded successfully to the new CompactLogix 5380.
4. The controller was placed in **Remote Run**.
5. **Controller OK** remained healthy.
6. **I/O OK** remained healthy.
7. No forces were present.
8. Online watch tables were used to monitor program selection, current step, requested step, timer preset/accumulator, physical inputs, legacy output words, and mapped 5069 outputs.

## Skills Demonstrated

- Allen-Bradley SLC 500 / RSLogix 500
- CompactLogix 5380 / Studio 5000 Logix Designer
- 5069 I/O configuration
- Ladder Logic
- Legacy PLC migration
- FactoryTalk View Machine Edition
- PanelView Standard to PanelView Plus 7 modernization
- EtherNet/IP
- Industrial network segmentation
- PLC/HMI integration
- I/O mapping and commissioning
- Cross-reference analysis
- Online troubleshooting and watch tables
- Controls documentation
- Bench testing and staged commissioning

## Repository Guide

- [`docs/architecture.md`](docs/architecture.md) — controls and network architecture
- [`docs/io-mapping.md`](docs/io-mapping.md) — legacy-word to 5069 physical I/O strategy
- [`docs/migration-notes.md`](docs/migration-notes.md) — key conversion problems and resolutions
- [`docs/commissioning.md`](docs/commissioning.md) — bench validation and commissioning workflow
- [`docs/hmi-modernization.md`](docs/hmi-modernization.md) — PanelView modernization approach

## Status

**Current milestone:** migrated PLC application successfully verified, downloaded, and executed on the CompactLogix 5380 bench system. HMI integration and technician troubleshooting documentation are continuing.

---

### Author

**Neuris Feliz**  
Instrumentation & Controls / Automation | PLC | HMI | Industrial Networking | Cybersecurity

This repository is presented as a professional engineering portfolio project. Proprietary production files and sensitive infrastructure details are intentionally excluded.