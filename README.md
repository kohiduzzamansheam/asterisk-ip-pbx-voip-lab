# Asterisk-Based IP PBX & VoIP Communication Lab

A hands-on VoIP lab built with **Asterisk PBX** on Ubuntu Server. This project explores how IP-based telephone systems work, from SIP registration and endpoint configuration to internal call routing and VoIP troubleshooting.

The lab uses a Grandstream GRP2601 IP phone and a macOS softphone to practice communication between SIP endpoints through an Asterisk server.

## Project Overview

Traditional telephone systems often require dedicated telephony hardware and infrastructure. With VoIP, voice communication can run over an IP network.

The goal of this project is to build a small IP PBX environment, understand its core components and gain practical experience with Asterisk administration.

### Lab Environment

| Component | Details |
|---|---|
| Operating System | Ubuntu Server 24.04 LTS |
| PBX Software | Asterisk 20 |
| SIP Protocol | PJSIP |
| Physical IP Phone | Grandstream GRP2601 |
| Softphone | macOS Softphone |
| Network | Local IP network |

## Architecture

The Asterisk server acts as the central PBX and manages communication between connected SIP endpoints.

```text
       Grandstream GRP2601
          IP Phone
              |
              | SIP / RTP
              |
       +--------------+
       |              |
       |   Asterisk   |
       |    PBX       |
       |              |
       | Ubuntu Server|
       +--------------+
              |
              | SIP / RTP
              |
       macOS Softphone
```

**Communication overview:**

1. The IP phone and softphone connect to the Asterisk server.
2. SIP is used for registration and call signaling.
3. Asterisk processes incoming calls using the dialplan.
4. RTP carries the voice media during calls.

> Note: The actual RTP media path depends on the Asterisk media configuration. It may pass through Asterisk or flow directly between endpoints.

## Features & Learning Areas

The project focuses on the following areas:

- Installing and managing Asterisk on Ubuntu Server.
- Understanding SIP signaling and RTP media.
- Configuring PJSIP endpoints, authentication and AORs.
- Understanding SIP registration and endpoint contacts.
- Working with Asterisk dialplans and internal extensions.
- Testing communication between IP phones and softphones.
- Using the Asterisk CLI for monitoring and troubleshooting.

Additional PBX features such as IVR, call queues, Music on Hold and call transfers are separate learning and testing areas. Their implementation status will be documented as they are completed.

## Repository Structure

```text
asterisk-ip-pbx-voip-lab/
│
├── README.md
│
├── docs/
│   ├── architecture.md
│   ├── voip-fundamentals.md
│   ├── pjsip-configuration.md
│   └── dialplan-guide.md
│
├── configs/
│   ├── pjsip.conf.example
│   └── extensions.conf.example
│
├── diagrams/
│   └── network-architecture.png
│
├── screenshots/
│   ├── installation/
│   ├── endpoint-registration/
│   └── call-testing/
│
└── testing/
    └── test-cases.md
```

## Documentation

| Document | Description |
|---|---|
| [System Architecture](docs/architecture.md) | Lab components and communication flow |
| [VoIP Fundamentals](docs/voip-fundamentals.md) | PBX, SIP, RTP, SDP, codecs and DTMF |
| [PJSIP Configuration](docs/pjsip-configuration.md) | Endpoints, authentication and AORs |
| [Dialplan Guide](docs/dialplan-guide.md) | Contexts, extensions, priorities and call routing |

## Useful Asterisk Commands

These are some of the commands I use while working with the lab.

**Check Asterisk version**

```bash
asterisk -rx "core show version"
```

**Check Asterisk service**

```bash
sudo systemctl status asterisk
```

**Open the Asterisk CLI**

```bash
sudo asterisk -rvvv
```

**List PJSIP endpoints**

```bash
asterisk -rx "pjsip show endpoints"
```

**Check registered contacts**

```bash
asterisk -rx "pjsip show contacts"
```

**Inspect the dialplan**

```bash
asterisk -rx "dialplan show"
```

## Security Considerations

Configuration files and logs can contain sensitive information. Before publishing anything from the lab, I review and remove:

- SIP usernames and passwords.
- Authentication credentials and SIP trunk details.
- Public IP addresses and private network details where necessary.
- SSH keys, TLS private keys and API credentials.
- Phone MAC addresses, serial numbers and personal information.
- Sensitive call logs, recordings and packet captures.

The repository contains sanitized example configurations rather than live production credentials.

## What I Learned

Working on this lab has helped me understand how different parts of a VoIP system work together.

Some of the key areas I have been exploring include:

- How SIP registration works between an endpoint and a PBX.
- How PJSIP uses endpoint, authentication and AOR objects.
- How Asterisk processes calls through contexts and dialplan priorities.
- Why SIP signaling and RTP media are treated separately.
- How to inspect Asterisk logs and troubleshoot communication issues.
- Building an IVR system with DTMF-based menu navigation.
- Configuring call queues and agent handling.
- Testing blind and attended call transfers.
- Exploring SIP trunk connectivity.
