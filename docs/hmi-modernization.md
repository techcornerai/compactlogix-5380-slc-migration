# HMI Modernization

## Legacy HMI

The original operator interface was a PanelView Standard application using a legacy communications architecture and a 4:3 operator layout.

## Modern Target

The replacement platform is a **PanelView Plus 7** running FactoryTalk View Machine Edition.

## Migration Work

- Converted the legacy application into a FactoryTalk View ME project.
- Reworked the graphics for a 640 × 480 PanelView Plus target.
- Preserved core operator functions such as Program Select, Stop/Run, Previous Step, Next Step, Go To Step, and Numeric Entry.
- Retained legacy PLC tag behavior where required for functional compatibility.
- Added technician-oriented maintenance access and troubleshooting planning.
- Prepared the HMI for direct Ethernet/IP communication with the CompactLogix platform.

## Security / Maintenance Access

Maintenance functions are being separated from normal operator controls so configuration access is not exposed during routine operation.

## Portfolio Scope

The public repository documents the engineering approach rather than publishing proprietary HMI runtime files, credentials, or complete production graphics.