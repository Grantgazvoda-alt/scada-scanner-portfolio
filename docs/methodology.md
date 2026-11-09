# Scanning Methodology

## Scope definition

Every scan begins with an authorized target range. No scanning occurs without a defined scope — IP blocks, VLANs, or site boundaries supplied by the operator.

## Phase 1: Host discovery

- ICMP echo and TCP SYN probes on a baseline port set
- ARP scanning on local segments for Layer-2 visibility
- Results deduplicated into a live-host inventory

## Phase 2: ICS port scan

Targeted port set covering industrial protocols:

| Port | Protocol | Domain |
|------|----------|--------|
| 502 | Modbus TCP | Building automation, PLCs |
| 102 | Siemens S7 | Siemens PLCs |
| 44818 | EtherNet/IP | Allen-Bradley, Rockwell |
| 20000 | DNP3 | Utility SCADA |
| 47808 | BACnet | HVAC, building controls |
| 1911/49320 | Niagara Fox | Tridium building automation |
| 789 | Crimson v3 | Red Lion HMIs |
| 2404 | IEC 60870-5-104 | Utility telecontrol |

## Phase 3: Service fingerprinting

- Protocol-aware handshakes extract device make, model, and firmware version
- Banner parsing handles both standard and non-standard response formats
- Confidence scoring on each fingerprint based on response completeness

## Phase 4: Vulnerability correlation

- Discovered versions matched against CVE databases and vendor advisories
- Severity assigned using CVSS where available, adjusted for OT context
- OT-specific risk factors noted: physical process impact, safety system adjacency

## Phase 5: Reporting

- Structured JSON and human-readable summaries
- Findings grouped by asset, protocol, and severity
- Remediation guidance per finding class

## Safety constraints

- No exploit payloads transmitted
- No configuration changes attempted
- Scan intensity capped to avoid process disruption
- All activity logged with timestamps and scope reference
