# Suspicious Recruitment Email Investigation – Growth Hub

## Overview

I received an email inviting me to attend a job interview with an organization claiming to be Growth Hub. At first glance, the email looked like a normal recruitment invitation. It included an interview location, an assessment/registration link, and instructions to reply to confirm my availability.

However, a few things caught my attention. The email requested that I bring my National Identification Number (NIN), the sender’s identity was not independently verified, and the phone number included in the message had a suspicious reputation on Truecaller.

Rather than responding immediately, I decided to investigate the email using different cybersecurity and OSINT tools to understand whether the recruitment opportunity was legitimate.

This project documents my investigation, the tools I used, the findings, and the security concerns I identified.

## Objectives

- Examine the sender’s email address and authentication results.
- Investigate the assessment link included in the email.
- Check the reputation of associated URLs and IP addresses.
- Investigate the domains associated with the organization.
- Identify possible signs of impersonation or social engineering.
- Assess the risks involved and recommend appropriate security measures.

## Investigation and Findings

### 1. Initial Email Review

The email contained the following:

- An invitation to attend a physical interview.
- An assessment/registration link to be completed before the interview.
- A request to reply to confirm availability.
- Instructions to bring my NIN.
- A contact telephone number.

The request for sensitive identification information, combined with the unverified recruitment process, made me suspicious.

### 2. Email Header Analysis

I examined the email headers to understand how the message was delivered and whether it passed standard email authentication checks.

| **Authentication** | **Result** |
|--------------------|------------|
| SPF                | PASS       |
| DKIM               | PASS       |
| DMARC              | PASS       |

All three authentication checks passed.

However, passing these checks does not automatically establish that an email is legitimate. They authenticate aspects of the sending domain and email delivery, not the identity or intentions of the person behind the account.

The sender’s email address was:

`growthhubcrmltd@gmail.com`

Since this was a Gmail address, I could not use it alone to establish that the sender was officially affiliated with Growth Hub.

### 3. URL Investigation – VirusTotal

I submitted the assessment/registration URL to VirusTotal to check whether it had been flagged by security vendors.

**Result:** The URL was reported as clean at the time of investigation.

A clean result does not guarantee that a website is safe. Newly created or previously unreported malicious URLs may not yet be detected.

I therefore treated this result as one part of the investigation rather than proof of legitimacy.

### 4. IP Reputation Analysis – AbuseIPDB

I investigated an associated IP address using AbuseIPDB.

The results showed:

| **Attribute**          | **Result**                                 |
|------------------------|--------------------------------------------|
| Abuse Confidence Score | 31%                                        |
| Classification         | Elevated                                   |
| ISP                    | Internet Utilities Europe and Asia Limited |
| Usage Type             | Content Delivery Network                   |
| ASN                    | AS13335                                    |
| Hostname               | lovable-app-cd1-4.p.l5e.io                 |
| Domain                 | netutils.io                                |
| Country                | United States                              |
| Abuse Reports          | 203                                        |
| Distinct Reporters     | 62                                         |

Some of the abuse reports referenced phishing and crypto-drainer activity.

One important detail was that the IP address was identified as belonging to CDN infrastructure. Since CDN IP addresses can be shared by multiple websites, the abuse reports cannot automatically be attributed to the recruitment website.

The relationship between the IP address and the investigated URL still needs to be established before making a direct attribution.

### 5. DNS Investigation – DNSDumpster

I used DNSDumpster to investigate the domains associated with the organization.

#### thegrowthhub.africa

The investigation returned the following records:

| **Record** | **Result**                                        |
|------------|---------------------------------------------------|
| A          | 159.198.67.178                                    |
| MX         | eforward1.registrar-servers.com                   |
| MX         | eforward2.registrar-servers.com                   |
| NS         | dns1.registrar-servers.com                        |
| NS         | dns2.registrar-servers.com                        |
| TXT        | SPF record referencing Namecheap email forwarding |

These results showed that the domain had publicly configured DNS infrastructure.

However, the existence of the domain does not establish that it belongs to the person who sent the recruitment email.

#### growthhub.crm

I also investigated growthhub.crm.

DNSDumpster returned no IP addresses, MX records, NS records, or other DNS records.

This raised a significant concern about the validity of the domain address, assuming it was accurately represented in the original email.

### 6. Domain Investigation – DNS Twister

I used DNS Twister to identify potentially similar domains.

During the search, I found growthhub.com, but no growthhub.crm.

The discovery of growthhub.com was worth investigating further, but the result alone did not establish that it was the official website of the organization or that it was connected to the recruitment email.

Its ownership and relationship with thegrowthhub.africa remain unverified.

### 7. Phone Number Investigation – Truecaller

I checked the telephone number included in the recruitment email using Truecaller.

The number displayed the label:

**“Job scammer”**

This added another reason to be cautious.

However, Truecaller labels are user-generated and cannot independently prove that a number is being used for fraudulent activity.

### Evidence

The screenshots collected during this investigation are available in the Evidence folder.

The folder contains:

* Original recruitment email
* Email header analysis
* VirusTotal URL investigation
* AbuseIPDB IP reputation results
* DNSDumpster domain investigation
* DNS Twister similar-domain results
* Truecaller telephone number lookup

## Summary of Findings

| **Investigation**    | **Finding**                                          |
|----------------------|------------------------------------------------------|
| Email authentication | SPF, DKIM and DMARC passed                           |
| Sender identity      | Gmail account; organizational affiliation unverified |
| VirusTotal           | Assessment URL reported clean                        |
| AbuseIPDB            | 31% abuse confidence score                           |
| DNSDumpster          | DNS records found for thegrowthhub.africa            |
| DNSDumpster          | No DNS records found for growthhub.crm               |
| DNS Twister          | growthhub.com identified as a similar domain         |
| Truecaller           | Phone number labelled “Job scammer”                  |

## Security Risks Identified

Based on the findings, I identified several potential risks:

- **Identity theft:** The request for NIN could expose sensitive personal information.
- **Social engineering:** The recruitment process could be used to gain the trust of job seekers.
- **Malicious links:** The assessment link could potentially be used for credential harvesting or other malicious activity.
- **Physical safety:** Attending an unverified interview location could expose applicants to personal safety risks.

These are potential risks identified during the investigation, not confirmed attack outcomes.

## Recommendations

1. Do not provide NIN or other sensitive personal information to unverified recruiters.
2. Investigate assessment links before opening or submitting information.
3. Verify the organization through independent sources, including the Corporate Affairs Commission where applicable.
4. Confirm the interview location and interviewer through independently obtained contact details.
5. Preserve suspicious emails and their full headers for further investigation.
6. Avoid relying on a single threat-intelligence platform when assessing URLs and IP addresses.
7. Do not attend an unverified physical interview until the organization and venue have been independently confirmed.

## Final Assessment

The email contained several warning signs that justified further investigation.

Although SPF, DKIM and DMARC passed, the sender’s organizational identity remained unverified. The request for NIN, the Truecaller reputation result, the unusual domain findings, and the proposed physical interview raised concerns about possible recruitment-based social engineering.

The VirusTotal result did not identify the assessment URL as malicious, while the AbuseIPDB findings required additional investigation because the associated IP address was classified as CDN infrastructure.

I could not conclusively establish that the sender was a scammer or that the assessment link was malicious. However, I also could not independently verify the legitimacy of the recruitment invitation.

**Verdict: Suspicious recruitment email – potential social engineering, pending further verification.**

## Tools Used

- [VirusTotal](https://www.virustotal.com/)
- [AbuseIPDB](https://www.abuseipdb.com/)
- [DNSDumpster](https://dnsdumpster.com/)
- [DNS Twister](https://dnstwister.report/)
- [Truecaller](https://www.truecaller.com/)

## Disclaimer

This investigation was conducted for educational and defensive cybersecurity purposes. The findings represent information available at the time of analysis. No individual or organization is being declared guilty of fraudulent activity based solely on these findings.
