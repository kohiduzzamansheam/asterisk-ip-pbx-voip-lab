# Asterisk Dialplan Guide

## Introduction

The dialplan is where Asterisk decides what to do when someone dials an extension.

It controls how calls are handled, where they go and what happens next.

The main dialplan configuration file is:

```text
/etc/asterisk/extensions.conf
```

## Understanding the Dialplan Structure

A dialplan is organized into three main parts:

- **Context:** Groups related dialplan rules.
- **Extension:** Defines which dialed number or pattern should match.
- **Priority:** Determines the order in which instructions execute.

A basic example:

```ini
[from-internal]
exten => 7000,1,Answer()
 same => n,Playback(hello-world)
 same => n,Hangup()
```

Here is what each part means:

| Part | Meaning |
|---|---|
| `[from-internal]` | Context name |
| `7000` | Extension number |
| `1` | First priority |
| `Answer()` | Answers the call |
| `Playback()` | Plays an audio file |
| `Hangup()` | Ends the call |
| `same => n` | Continues at the next priority |

The `n` means next priority, so you don't have to manually number every line.

## How Asterisk Processes a Call

When someone dials an extension:

1. Asterisk receives the call.
2. It checks the endpoint's assigned context.
3. It looks for a matching extension.
4. It executes the instructions in priority order.
5. The call continues, transfers or ends depending on the dialplan.

## Common Dialplan Applications

| Application | Purpose |
|---|---|
| `Answer()` | Answers a call |
| `Dial()` | Calls another endpoint |
| `Playback()` | Plays an audio file |
| `Background()` | Plays audio while waiting for input |
| `Read()` | Collects user input |
| `Queue()` | Sends a call to a queue |
| `VoiceMail()` | Sends a caller to voicemail |
| `Hangup()` | Ends a call |

## Example: Calling Another Extension

```ini
[from-internal]
exten => 7000,1,Dial(PJSIP/7000,20)
 same => n,Hangup()
```

This tells Asterisk to try calling endpoint 7000 for up to 20 seconds and then end the call when the dial operation finishes.

## Checking the Dialplan

To view the available dialplan:

```bash
asterisk -rx "dialplan show"
```

To inspect a particular context:

```bash
asterisk -rx "dialplan show from-internal"
```

To reload the dialplan after making changes:

```bash
asterisk -rx "dialplan reload"
```

## A Practical Note

The dialplan is one of the most important parts of Asterisk. A phone can register successfully and still fail to make calls if the dialplan is missing or incorrectly configured.

Understanding contexts, extensions and priorities makes call routing much easier to manage and troubleshoot.
