## **Executive Summary/Overview** 

In this project, I architected an automated continuous compliance monitoring and real-time alerting system within AWS. The core objective was to proactively detect and notify administrators of severe security misconfigurations, specifically the dangerous exposure of Amazon S3 storage buckets to the public internet. By integrating intelligent AWS monitoring services, I established a robust security guardrail that drastically reduces the mean time to detect data exposure risks, ensuring the organization maintains a secure, compliant, and highly visible cloud environment. 

## **Core Technologies/Applied Technologies** 

- AWS Config (Continuous Monitoring & Resource Tracking) 

- Amazon Simple Notification Service (SNS) (Pub/Sub Messaging) 

- Amazon Simple Storage Service (S3) 

- AWS Identity and Access Management (IAM) 

## **Situation** 

Cloud environments are highly dynamic, and a simple human error—such as misconfiguring a storage bucket—can instantly expose sensitive corporate data to the public internet. The organization faced the challenge of maintaining strict visibility and control over its AWS infrastructure. Without an automated monitoring mechanism, identifying unsecure or non-compliant S3 buckets relied entirely on periodic manual audits, leaving a dangerous window of opportunity for threat actors to exploit data breaches or trigger severe compliance violations. 

## **Task** 

My responsibility was to engineer a proactive, automated security alert pipeline to eliminate manual oversight gaps. I was assigned to configure AWS continuous monitoring tools to automatically evaluate S3 bucket configurations against strict internal security baselines. Furthermore, I needed to implement a real-time communication channel that would immediately push an email notification to the security team the moment any S3 bucket was made public, unsecure, or non-compliant. 

## **Actions** 

- I activated and configured AWS Config as the primary recording engine to continuously track resource changes across the AWS environment, assigning a dedicated IAM role and S3 bucket to securely store configuration history. _![Configuring the AWS Config recording strategy](images/aws-config-recording.png)_ 

- I engineered a dedicated communication pipeline using Amazon Simple Notification Service (SNS), establishing a "SecurityAlertsTopic" and subscribing the necessary administrative email endpoints to receive instant security bulletins. 

   - _![Creating the Amazon SNS topic and email subscription](images/sns-topic-setup.png)_ 

- I implemented a strict, automated security guardrail by deploying the s3-bucket-public-read-prohibited managed rule within AWS Config, effectively linking this rule's evaluation state directly to the SNS topic for automated dispatch. 

   - _![Linking compliance rule to SNS](images/linking-rule-to-sns.png)_ 

- I validated the system's efficacy by intentionally provisioning a test S3 bucket and modifying its JSON bucket policy and block access settings to simulate a catastrophic public data exposure event. 

   - _![Modifying S3 permissions for non-compliance](images/s3-non-compliance-test.png)_ 

- I successfully verified the end-to-end alerting workflow by observing the AWS Config dashboard transition to a non-compliant state and confirming the immediate receipt of the targeted security alert in my email inbox, before properly securing the bucket to restore compliance. 

   - _![Real-time non-compliant email alert](images/email-alert-receipt.png)_ 

## **Result** 

The project was a resounding success, culminating in a fully functional, zero-touch security monitoring pipeline. Qualitatively, the implementation eliminated the reliance on manual infrastructure audits, providing the security team with high-fidelity, real-time visibility into unauthorized environment changes. Quantitatively, the solution reduced the time required to detect a public S3 bucket exposure from potentially weeks to mere minutes, demonstrating a 100% success rate in triggering automated email alerts during the break-and-fix testing phase. 

## **Frameworks & Standards** 

- **Nigeria Data Protection Act (NDPA):** This act mandates that organizations implement appropriate technical measures to prevent unauthorized access or accidental disclosure of personal data. By deploying automated guardrails that instantly detect and alert on publicly accessible S3 buckets, I ensured that any infrastructure misconfiguration potentially exposing Nigerian citizens' data is immediately flagged and remediated, aligning directly with NDPA data security requirements. 

- **NIST Cybersecurity Framework (CSF):** The "Detect" core function of NIST CSF requires continuous monitoring to identify cybersecurity events promptly. I achieved this standard by configuring AWS Config to continuously record configuration changes and evaluate them against strict baseline rules, ensuring an exposed bucket is detected the moment its state changes. 

- **ISO/IEC 27001:** This international standard emphasizes continuous monitoring and strict access control over sensitive information assets. My implementation achieved this by integrating automated policy enforcement and real-time SNS alerting, fulfilling the standard's requirements for proactive incident management and secure configuration tracking. 

## **Organizational Benefits** 

This project provided the organization with a robust, automated safety net that significantly 

minimizes the financial and reputational risks of data breaches caused by human error. By shifting from reactive audits to proactive, real-time compliance monitoring, the business dramatically improved its security posture while reducing the manual operational overhead on the engineering team. 

