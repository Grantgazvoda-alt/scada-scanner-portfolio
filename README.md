# SCADA Scanner

**Industrial control system exposure and vulnerability scanner.**

A network reconnaissance tool for identifying exposed OT/ICS assets — banner grabbing, service fingerprinting, and known-vulnerability correlation across industrial protocol ranges.

## What it does

- **Host discovery**: sweep IP ranges and identify live devices on industrial networks
- **Service fingerprinting**: detect exposed services on common ICS ports (Modbus 502, DNP3 20000, EtherNet/IP 44818, BACnet 47808, Siemens S7 102, and others)
- **Banner analysis**: extract version strings and device identifiers from service responses
- **Vulnerability correlation**: map discovered services to known CVEs and public advisories
- **Report generation**: structured output of findings with severity ratings

## Why it matters

Industrial networks were built before the internet existed. Many still run with default credentials, unpatched firmware, and no network segmentation. A single exposed Modbus controller or BACnet gateway can be the entry point to physical processes — pumps, valves, power distribution, manufacturing lines.

This scanner exists to find those exposures before someone with worse intentions does.

## Architecture

```
┌──────────────┐
│ IP Range     │
│ Input        │
└──────┬───────┘
       ▼
┌──────────────┐
│ Host         │  ping sweep / ARP discovery
│ Discovery    │
└──────┬───────┘
       ▼
┌──────────────┐
│ Port Scan    │  ICS-specific port set
└──────┬───────┘
       ▼
┌──────────────┐
│ Service      │  protocol handshake, banner grab
│ Fingerprint  │
└──────┬───────┘
       ▼
┌──────────────┐
│ Vuln         │  CVE/advisory lookup
│ Correlation  │
└──────┬───────┘
       ▼
┌──────────────┐
│ Report       │  structured findings, severity-ranked
└──────────────┘
```

## Design principles

- **Read-only by default**: the scanner observes; it does not modify. No write operations against discovered services unless explicitly enabled.
- **Rate-limited**: respects network etiquette and avoids disrupting live industrial processes
- **Authenticated context**: designed to run with operator authorization on owned or contracted networks

## Status

Active development. Methodology and architecture public; implementation retained as proprietary IP.

## Contact

Open to contract and employment discussions in OT security, ICS penetration testing, and critical infrastructure defense.
