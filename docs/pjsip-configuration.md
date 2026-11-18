# PJSIP Configuration

## Introduction

PJSIP is the SIP channel driver used by Asterisk to communicate with IP phones and softphones.

In this lab, PJSIP is used to configure endpoints and handle SIP communication between the Asterisk server and the connected devices.

The main configuration file is:

```text
/etc/asterisk/pjsip.conf
```

## Understanding the Main Components

PJSIP configuration uses different object types. Each has a specific responsibility.

### 1. Endpoint

An endpoint represents a device or user that communicates with Asterisk.

It defines settings such as:

- Authentication
- Audio codecs
- Context
- Media handling

Example:

```ini
[7000]
type=endpoint
context=from-internal
disallow=all
allow=ulaw
auth=7000-auth
aors=7000
```

### 2. Authentication

The authentication object contains the credentials used by an endpoint when authenticating with Asterisk.

```ini
[7000-auth]
type=auth
auth_type=userpass
username=7000
password=CHANGE_THIS_PASSWORD
```

Use a placeholder password in public examples. Never publish your actual SIP password.

### 3. AOR

AOR stands for Address of Record.

It tells Asterisk where an endpoint can be reached. It can also store contact information learned through SIP registration.

```ini
[7000]
type=aor
max_contacts=1
```

## How These Objects Work Together

Think of the three objects this way:

| Object | Responsibility |
|---|---|
| Endpoint | Defines the device and its communication settings |
| Auth | Handles authentication |
| AOR | Stores contact information for reaching the device |

These objects are linked together using their configuration names.

## Checking PJSIP Status

Asterisk provides useful CLI commands for checking endpoint information.

List configured endpoints:

```bash
asterisk -rx "pjsip show endpoints"
```

Check registered contacts:

```bash
asterisk -rx "pjsip show contacts"
```

Inspect a specific endpoint:

```bash
asterisk -rx "pjsip show endpoint 7000"
```

Check available transports:

```bash
asterisk -rx "pjsip show transports"
```

## Troubleshooting Tips

If an endpoint is not registering, check the following:

1. Is the Asterisk service running?
2. Is the SIP transport configured and active?
3. Are the username and password correct?
4. Does the endpoint reference the correct authentication and AOR objects?
5. Is the device using the correct server IP and SIP port?
6. Is a firewall blocking SIP traffic?

For troubleshooting, the Asterisk CLI is particularly useful:

```bash
asterisk -rvvv
```

You can then enable SIP message logging:

```text
pjsip set logger on
```

Disable it when finished:

```text
pjsip set logger off
```

Always review logs before sharing them publicly, as they may contain IP addresses, usernames and other sensitive information.
