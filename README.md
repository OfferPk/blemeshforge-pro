\# BLEMeshForge Pro (v1.0.0)  
\> \*\*Enterprise Bluetooth Mesh (Profile v1.0.1 / v1.1) Protocol Studio, Network PDU Dissector, SIG Model Synthesizer & 10-Point Normative Zero-Trust Compliance Auditor\*\*

\[\!\[Bluetooth Mesh\](https\://img.shields.io/badge/Bluetooth%20SIG-Mesh%20v1.1%20%7C%20v1.0.1-00E5FF.svg)\](\#)  
\[\!\[Model Support\](https\://img.shields.io/badge/Models-Generic%20OnOff%20%7C%20Config%20Server-7C4DFF.svg)\](\#)  
\[\!\[Audit Score\](https\://img.shields.io/badge/Normative%20Audit-10%2F10%20PASS-00E676.svg)\](\#)  
\[\!\[Zero Dependency\](https\://img.shields.io/badge/CLI-Python%203.8%2B-FF9100.svg)\](\#)

\---

\#\# Overview  
\*\*BLEMeshForge Pro\*\* is an enterprise developer tool designed for firmware engineers, IoT hardware manufacturers, and commercial lighting/building automation developers building products for \*\*Bluetooth Mesh (Mesh Profile Specification v1.0.1 & v1.1)\*\*.

It eliminates costly mesh commissioning failures and expensive proprietary RF sniffers (\$15,000–\$45,000+ per bench) by delivering a zero-dependency web studio, a bit-accurate Network Layer & Lower Transport PDU synthesizer, an interactive packet dissector, and an automated 10-point normative compliance audit engine.

\#\#\# Core Capabilities  
1\. \*\*Interactive Web Studio\*\*: Real-time Mesh Network PDU assembler (IVI, NID, CTL, TTL, SEQ, SRC, DST, Transport PDU, NetMIC) and PB-ADV advertising packet framing (AD Type 0x2A).  
2\. \*\*SIG Foundation & Generic Models\*\*: Synthesizes Generic OnOff (Get, Set, Set Unack, Status) and Configuration Server (Composition Data Get, AppKey Bind) messages.  
3\. \*\*Address Classification Engine\*\*: Categorizes 16-bit address fields into Unassigned (0x0000), Unicast (0x0001–0x7FFF), Virtual (0x8000–0xBFFF), Group (0xC000–0xFEFF), and Fixed Groups (0xFFFC All-Proxies, 0xFFFD All-Friends, 0xFFFE All-Relays, 0xFFFF All-Nodes).  
4\. \*\*10-Point Normative Zero-Trust Auditor\*\*: Validates the critical 29-byte PB-ADV Network PDU limit, Unicast source constraints, non-zero destination checks, TTL boundaries (0–127), IVI 1-bit flags, sequence number exhaustion thresholds (\>= 0xC00000 warning), and NetMIC lengths (4 bytes for Access, 8 bytes for Control).  
5\. \*\*Zero-Dependency Python CLI\*\*: Standalone command-line runner for automated CI/CD pipelines, headless testing, and regression suites (\`packet\`, \`dissect\`, \`audit\`).  
6\. \*\*Embedded C SDK Exporter\*\*: Generates production C data structures for Zephyr RTOS and Nordic Semiconductor nRF Connect SDK.

\---

\#\# Directory Structure  
\`\`\`  
product\_299/  
├── README.md                                  \# Complete product guide and quick start  
├── source-code/  
│   ├── index.html                             \# Multi-tab responsive web studio  
│   ├── mesh.css                               \# Modern cybersecurity dark theme  
│   ├── mesh-engine.js                         \# Core Bluetooth Mesh protocol engine  
│   ├── mesh-auditor.js                        \# 10-point normative compliance rules  
│   └── app.js                                 \# Interactive Studio controller  
├── build/  
│   ├── blemesh-cli.py                         \# Zero-dependency Python 3 CI/CD CLI runner  
│   └── blemeshforge-pro-v1.0.0.zip            \# Packaged distribution archive  
├── documentation/  
│   ├── ARCHITECTURE.md                        \# Protocol stack and framing spec  
│   ├── USER\_GUIDE.md                          \# Studio and CLI user guide  
│   └── MONETIZATION\_AND\_MARKETING\_PLAYBOOK.md \# Pricing, GTM, and market strategy  
├── screenshots/  
│   └── blemesh-studio-preview.svg             \# Vector architecture & UI mock  
└── test\_blemesh.py                            \# Automated 10-point unit verification suite  
\`\`\`

\---

\#\# Automated Verification & Test Coverage  
BLEMeshForge Pro is validated against a 10-test automated verification suite (\`test\_blemesh.py\`):  
\- \[x\] Generic OnOff Set OpCode (0x8202) serialization and parameters  
\- \[x\] Generic OnOff Status OpCode (0x8204) payload formatting  
\- \[x\] Unsegmented Lower Transport PDU framing with TransMIC  
\- \[x\] Network Layer PDU big-endian packing and NetMIC length (CTL=0 vs CTL=1)  
\- \[x\] PB-ADV BLE Advertising framing (AD Type 0x2A, Flags 0x01)  
\- \[x\] Network PDU dissection accuracy (roundtrip test)  
\- \[x\] 10-point normative compliance audit on standard profiles (10/10 PASS)  
\- \[x\] Rejection of oversized Network PDU (\> 29 bytes on PB-ADV)  
\- \[x\] Rejection of invalid Unicast SRC address (out of 0x0001–0x7FFF)  
\- \[x\] Address classification across Unassigned, Unicast, Virtual, Group, and Fixed

\---

\#\# Quick Start  
\`\`\`bash  
\# Synthesize a Generic OnOff Set packet  
python3 build/blemesh-cli.py packet \--opcode GENERIC\_ONOFF\_SET \--state 1 \--src 0x1201 \--dst 0xC001 \--ttl 7

\# Dissect raw Network PDU hex stream  
python3 build/blemesh-cli.py dissect \--hex 68070001001201C0010082020101AAAA55A055A0

\# Run 10-point normative compliance audit  
python3 build/blemesh-cli.py audit

\# Execute unit verification tests  
python3 test\_blemesh.py  
\`\`\`  
