# Investigation 03 — Windows Process Creation Monitoring

## Overview

**Platform:** Windows 11  
**Monitoring tool:** Wazuh  
**Windows Event ID:** 4688  
**Event type:** Process creation  
**Outcome:** Successful validation in a controlled home lab

## Objective

Configure Windows to record process creation and command-line information, then verify that the events are collected and searchable in Wazuh.

## Lab Configuration

Windows process-creation auditing was initially disabled. I enabled successful process-creation auditing using the Windows `auditpol` utility.

I then enabled the Windows policy setting for including command-line information in process-creation events.

## Procedure

1. Checked the existing process-creation audit policy.
2. Enabled successful process-creation auditing.
3. Enabled command-line capture for process-creation events.
4. Executed standard diagnostic commands on my Windows virtual machine.
5. Searched Wazuh for the resulting Windows Security events.

## Findings

Wazuh received Windows Security Event ID `4688` events for processes including:

- `whoami.exe`
- `ipconfig.exe`
- `tasklist.exe`

The event details included the process image path. After command-line capture was enabled, a subsequent `whoami.exe` event also included the command-line field.

This confirmed that process-creation events and command-line information were being forwarded to and displayed in Wazuh.

## Analyst Assessment

Process-creation monitoring can help analysts investigate which programs were launched and, when available, what command-line arguments were used.

In a real incident, an analyst could use this information to identify unusual execution paths, investigate suspicious commands, and correlate a process with other endpoint events.

However, a process appearing in the logs is not inherently malicious. Commands such as `whoami`, `ipconfig` and `tasklist` are legitimate administrative utilities. Their significance depends on the account, execution context, timing and surrounding activity.

## Security Considerations

Command-line logging can expose sensitive information when applications place passwords, tokens or other secrets in command-line arguments. Log access should be controlled, and sensitive information should not be deliberately entered into test commands.

## Recommended Follow-up

- Correlate process creation with authentication and other endpoint events.
- Review unusual executable paths and unexpected command-line arguments.
- Establish normal administrative activity as a baseline.
- Investigate suspicious activity using multiple sources of evidence rather than relying on a single event.

## Skills Demonstrated

- Windows audit policy configuration
- Security Event ID 4688 analysis
- Command-line logging
- SIEM event validation
- Endpoint monitoring and investigation documentation

## Conclusion

This investigation validated Windows process-creation monitoring and command-line capture in the home SOC lab. It demonstrated how endpoint telemetry can support investigations while highlighting the importance of context and careful handling of sensitive log data.
