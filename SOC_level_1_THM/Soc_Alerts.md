# SOC Alerts

## How An Event becomes an Alert?

Occurence of an **Event** ------> Systems **logs** the Event---------> Attention needing Logs are given to a security Solution as **Alerts**

## Alert properties

1. Alert Time == Shows alert creation time. Alert usually triggers a few minutes after the actual event.
2. Alert Name == Provides a summary of what happened,based on the detection rule's name.
3. Alert Severity == Defines the urgency of the alert,initially set by detection engineers,but can be altered by analysts if needed.
4. Alert Status == Informs if somebody is working on the alert or if the triage is done.
5. Alert Verdict == Also called alert classification, explains if the alert is a real threat or noise.
6. Alert Assignee == Shows the analyst that was assigned or assigned themselves to review the alert.
7. Alert Description == Explains what the alert is about, usually in three sections on the right.
8. Alert Fields == Provides SOC analysts' comments and values on which the alert was triggered.



## Picking the Right Alert

- Start with critical alerts, then high, medium, and finally low. 

- Start with the oldest alerts and end with the newest ones. 

## Alert Triage

<img width="1576" height="570" alt="image" src="https://github.com/user-attachments/assets/7ba9c44c-da9f-42b6-8b3a-dc2e6af78177" />

To support L1 analysts with this step, some teams develop **Workbooks** (also known as playbooks or runbooks) - instructions on how to investigate the specific category of alerts.
