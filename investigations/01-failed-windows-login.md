# Investigation 01 — Failed Windows Login

## Overview

**Platform:** Windows 11  
**Monitoring tool:** Wazuh  
**Windows Event ID:** 4625  
**Wazuh rule ID:** 60122  
**Wazuh alert level:** 5  
**Outcome:** Expected activity from a controlled lab test

## Objective

Test whether a failed Windows login attempt was recorded and reported by Wazuh, and review the resulting security alert.

## Procedure

1. Generated a controlled failed login attempt on my own Windows virtual machine.
2. Reviewed the associated Windows Security event in Wazuh.
3. Examined the alert rule, severity level and event details.
4. Assessed the event in the context of the known lab activity.

## Findings

Windows Event ID `4625` recorded the failed logon attempt.

Wazuh generated alert `60122`, described as **"Logon Failure - Unknown user or bad password"**, with alert level 5.

This confirmed that the failed authentication event was collected and matched a Wazuh detection rule.

## Analyst Assessment

The event was expected because I deliberately generated the failed login as part of the lab test. On its own, a failed login does not establish that an account has been compromised or that an attacker is present.

In a real environment, I would consider the account involved, the frequency of failures, the source of the activity, any related successful logins and whether the activity matched normal user behaviour.

## Recommended Follow-up

- Check for repeated failed logins against the same account.
- Correlate failures with successful authentication events.
- Investigate unexpected source addresses or account names.
- Escalate activity when the surrounding evidence supports further investigation.

## Skills Demonstrated

- Windows authentication event analysis
- Wazuh alert review
- Basic security-event triage
- Evidence-based assessment
- Security investigation documentation

## Conclusion

This test confirmed that Wazuh could detect a controlled failed Windows login through Windows Security event collection. It provided a baseline for investigating more complex authentication patterns in subsequent lab exercises.
