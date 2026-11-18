# System Architecture

## Overview

This project is a small IP PBX lab built using **Asterisk** on Ubuntu Server. The main goal is to understand how IP-based telephone systems work and how different devices communicate through a central PBX server.

The lab uses a Grandstream GRP2601 IP phone and a softphone running on a Mac. Both devices can connect to the Asterisk server using SIP.

## Lab Components

| Component | Purpose |
|---|---|
| Ubuntu Server 24.04 | Operating system hosting the PBX |
| Asterisk 20 | Handles calls and PBX functionality |
| PJSIP | Manages SIP communication and endpoints |
| Grandstream GRP2601 | Physical IP phone |
| macOS Softphone | Software-based telephone |
| Local Network | Connects the PBX and endpoints |

## How It Works

The Asterisk server acts as the central point for call handling.

1. The IP phone and softphone register with Asterisk using SIP.
2. A user initiates a call by dialing an extension.
3. Asterisk checks the dialplan to determine how the call should be handled.
4. Once the call is established, RTP carries the voice between the communicating devices.

SIP handles call setup and control, while RTP carries the actual audio.

## Communication Flow

```text
       Grandstream IP Phone
              |
           SIP / RTP
              |
              |
        Ubuntu Server
         Asterisk PBX
          (PJSIP)
              |
           SIP / RTP
              |
              |
        macOS Softphone
```

## Project Scope

The lab focuses on understanding and practicing:

- Asterisk installation and basic administration
- SIP endpoint configuration using PJSIP
- Extension registration
- Internal call routing through the dialplan
- Basic VoIP troubleshooting
- Additional PBX features as they are configured and tested

This is a learning and demonstration environment, not a production telephone system.
