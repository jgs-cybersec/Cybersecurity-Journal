# SOC Metrics and Objectives

## MTTD(Mean Time To Detect)

 average time it takes for an organization to identify a security threat, incident, or a technical problem.

## MTTR(Mean Time To Response)

average time between the initial alert and response to it.

## MTTA(Mean Time To Acknowledge)

average time taken to notice and formally accept ownership of an alert after it is triggered.

 ## SLA (Service Level Agreement)
 
 A document signed between a service provider (SOC team) and its customer defining the uptime and quality requirements. MTTD, MTTA, MTTR will be mentioned in this document while signing it.

 <img width="1342" height="415" alt="image" src="https://github.com/user-attachments/assets/2ba551c8-863c-4833-984b-211fe115916f" />


 ## Core Metrics


 <img width="1572" height="425" alt="image" src="https://github.com/user-attachments/assets/d3b1d4b8-2931-4435-b660-f7d0c552e914" />

1. Alert Count:

   Having a large number of alert is overwhelming and also having no alerts at all for a week is highly serious situation.
   Having low count of alerts may indicate an issue in the SIEM or lack of visibility, leading to undetected breaches.

   **5 to 30 alerts per day per L1 analyst is a good metric.**

2. False Positive Rates:

   75 out of 80 alerts are being False Positives is a bad signal. This means there are more noise than the actual alert which may make the analysts to suspect a real threat as a spam alert.
   A False Positive rate of **0% is an unachievable ideal**, but **80% or higher is a serious problem, usually fixed by a tool and detection rules tuning**, often called "False Positive Remediation".

3. Alert Escalation Rate:

   The alert escalation rate comes in handy to evaluate how experienced and independent the L1 analysts are and how often they decide to escalate the alert. It is usually aimed to be below 50%, or even better below 20%.

4. Threat Detection Rate:
   The threat detection rate should always be at 100% since every missed threat can have devastating consequences, such as ransomware infection and data exfiltration.

