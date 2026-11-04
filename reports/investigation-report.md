# GROWTH HUB RECRUITMENT EMAIL INVESTIGATION REPORT

**Investigation Type:** Suspicious Recruitment Email / Potential Social Engineering  
**Investigation Category:** Email Security Analysis  
**Analyst:** Security Analyst  
**Status:** Completed  
**Verdict:** Suspicious – Potential Recruitment-Based Social Engineering

---

## 1. Executive Summary

This investigation was conducted after I received a recruitment email claiming to represent an organization called Growth Hub. The email invited me to attend a physical interview at a specified location and included an assessment link that I was expected to complete before attending.

The sender also requested that I reply to confirm my availability, provided a telephone number, and instructed me to bring my National Identification Number (NIN) to the interview.

Although the email appeared to follow a normal recruitment process, certain aspects raised concerns. These included the use of a free Gmail address, the request for sensitive personal identification, the assessment link, and the need to verify the sender's relationship with the organization.

I conducted an investigation using email authentication checks, VirusTotal, AbuseIPDB, DNSDumpster, DNS Twister, and Truecaller.

The assessment link did not return malicious detections on VirusTotal at the time of checking. However, the associated IP reputation lookup on AbuseIPDB returned a 31% abuse confidence score, with reports from multiple users. The IP was identified as belonging to shared CDN infrastructure, meaning the reports could not automatically be attributed to the recruitment website.

Further domain investigation identified DNS records for `thegrowthhub.africa`, while the `growthhub.crm` reference returned no DNS records. I was unable to establish a verified connection between the Gmail sender, the identified company website, and the recruitment invitation.

The email was therefore classified as suspicious, with potential recruitment-based social engineering. The available evidence was insufficient to conclusively establish that the sender was a scammer.

## 2. Incident Overview

I received an email claiming to be from Growth Hub inviting me to attend an interview at a physical location.

The email contained the following elements:

- An invitation to attend a physical interview.
- An assessment link that I was expected to complete.
- A request to reply to the email to confirm whether I would be available to attend.
- A telephone number for further communication.
- An instruction to bring my National Identification Number (NIN).

The sender's email address was:

`growthhubcrmltd@gmail.com`

The combination of an unfamiliar recruitment invitation, a physical meeting location, an assessment link, and a request for sensitive identification information prompted further investigation before taking any action.

## 3. Scope and Methodology

The investigation focused on determining whether the recruitment email and its associated indicators could be trusted.

The following areas were examined:

1. Email sender and authentication details.
2. Assessment URL reputation.
3. Associated IP address reputation.
4. Organization-related domain and DNS records.
5. Similar domain names.
6. Telephone number reputation.
7. Potential social engineering indicators.

### Tools Used

| Tool | Purpose |
|---|---|
| Email client / Header analysis | Examine sender details and email authentication |
| VirusTotal | Check the assessment URL for malicious detections |
| AbuseIPDB | Investigate the reputation of an associated IP address |
| DNSDumpster | Examine DNS records for identified domains |
| DNS Twister | Identify similar domain names |
| Truecaller | Check the reputation associated with the telephone number |

## 4. Email Header Analysis

The email header was examined to understand how the message was sent and whether its authentication checks passed.

### 4.1 Sender Information

The sender address identified in the email was:

`growthhubcrmltd@gmail.com`

The use of a free Gmail address for an organization conducting formal recruitment raised a question about whether the sender was officially associated with the company.

However, using a Gmail address does not, by itself, prove that an email is fraudulent.

### 4.2 Email Authentication Results

The email authentication results showed:

- **SPF:** PASS
- **DKIM:** PASS
- **DMARC:** PASS

The email also appeared to have travelled through Google's email infrastructure.

These results indicate that the message passed the authentication checks reported by the receiving mail system. However, successful authentication does not establish that the sender is a legitimate recruiter or that the organization is genuine.

An attacker can also use a properly authenticated email account to send fraudulent messages.

### 4.3 Initial Assessment

Although the authentication results were successful, I did not treat them as proof of legitimacy.

The sender's identity and relationship with Growth Hub still needed to be independently verified.

## 5. URL Investigation – VirusTotal

The assessment link included in the recruitment email was investigated using VirusTotal.

The purpose was to determine whether the URL had been identified by security vendors as malicious, phishing-related, or otherwise suspicious.

### Findings

The URL did not return malicious detections on VirusTotal at the time of investigation.

### Assessment

A clean VirusTotal result does not guarantee that a URL is safe.

A newly created malicious website, a compromised legitimate website, or a URL used for targeted social engineering may not have been reported or detected by security vendors.

The result was therefore treated as an indicator to consider alongside the other findings, rather than confirmation that the assessment link was legitimate.

## 6. IP Reputation Analysis – AbuseIPDB

An associated IP address identified during the investigation was checked using AbuseIPDB to determine whether it had previously been reported for suspicious or malicious activity.

### 6.1 AbuseIPDB Results

The lookup returned the following information:

| Attribute | Result |
|---|---|
| Abuse Confidence Score | 31% |
| Abuse Classification | Elevated |
| ISP | Internet Utilities Europe and Asia Limited |
| Usage Type | Content Delivery Network |
| ASN | AS13335 |
| Hostname | `lovable-app-cd1-4.p.l5e.io` |
| Domain Name | `netutils.io` |
| Country | United States |
| City | San Francisco, California |
| Total Reports | 203 |
| Distinct Reporters | 62 |
| First Reported | July 5, 2025 |
| Most Recent Report | 3 days before the lookup |

Some recent reports included descriptions relating to crypto drainers and phishing websites.

### 6.2 Assessment

The 31% abuse confidence score and the number of reports indicated that the IP address had a history of abuse reports.

However, the IP was identified as belonging to Content Delivery Network infrastructure. CDN IP addresses can be shared by multiple websites and services.

This is important because reports against a shared IP may relate to other websites hosted on the same infrastructure.

Therefore, the AbuseIPDB findings could not independently establish that the Growth Hub assessment link or website was malicious.

The relationship between this IP address and the recruitment email's assessment URL also needed to be considered carefully. An IP reputation result alone does not prove that the email sender controlled or used the reported infrastructure.

## 7. Domain and DNS Investigation

During the investigation, I identified that Growth Hub appeared to be an existing company with an online presence at `thegrowthhub.africa`.

To establish whether this domain had a verifiable technical footprint, I used DNSDumpster to examine its publicly available DNS records.

The aim was to gather more information about the domain's hosting and email infrastructure and determine whether it could provide useful context about the recruitment email.

### 7.1 Investigation of `thegrowthhub.africa`

The DNSDumpster lookup returned the following results:

- **A Record:** `www.thegrowthhub.africa` resolved to `159.198.67.178`.
- **Hosting Network:** The IP address was associated with Namecheap, Inc. (ASN 22612).
- **MX Records:** The domain used Registrar Servers email-forwarding infrastructure.
- **Nameservers:** `dns1.registrar-servers.com` and `dns2.registrar-servers.com`.
- **TXT Record:** An SPF record appeared to reference Registrar Servers' email-forwarding service.

These results showed that `thegrowthhub.africa` had publicly configured DNS records.

However, the presence of DNS records does not independently prove that the Gmail address used to send the recruitment email was operated by, or officially connected to, the company.

### 7.2 Investigation of `growthhub.crm`

After examining `thegrowthhub.africa`, I also investigated `growthhub.crm`.

This was done because the `.crm` reference appeared during the email investigation, and I wanted to determine whether it had any publicly available DNS records or other verifiable technical information.

The DNSDumpster lookup returned no:

- A records
- AAAA records
- MX records
- NS records
- TXT records


This raised further questions about the validity of the domain reference in the email.

### 7.3 Similar Domain Search

I used DNS Twister to search for domains with names similar to the ones identified during the investigation.

The search returned `growthhub.com` as a similar domain.

However, the investigation did not establish any ownership or affiliation between `growthhub.com`, `thegrowthhub.africa`, and the Gmail sender.

### 7.4 Domain Investigation Assessment

The investigation confirmed that `thegrowthhub.africa` had publicly configured DNS records, while the `growthhub.crm` reference could not be verified through the DNS checks performed.

Although Growth Hub appeared to have an existing online presence, I could not establish a direct connection between the company, the Gmail sender address, and the recruitment invitation.

Therefore, the existence of the company and its website was not sufficient to establish the authenticity of the email.

## 8. Telephone Number Reputation Investigation

The telephone number included in the recruitment email was checked using Truecaller.

### Findings

Truecaller displayed the label:

**"Job scammer"**

### Assessment

This result raised an additional concern about the telephone number associated with the recruitment invitation.

However, Truecaller labels can be based on user-submitted reports and community feedback. They are not official confirmation that a person or organization is involved in fraudulent activity.

The result was therefore treated as a supporting indicator rather than conclusive evidence.

## 9. Indicators Identified

The investigation produced the following indicators and observations.

### 9.1 Technical Indicators

| Indicator | Observation |
|---|---|
| Sender email | `growthhubcrmltd@gmail.com` |
| Assessment URL | Submitted to VirusTotal; no malicious detections returned at the time of checking |
| Associated IP | AbuseIPDB score of 31% |
| IP reputation | 203 reports from 62 distinct reporters |
| IP usage type | Content Delivery Network |
| Domain investigated | `thegrowthhub.africa` |
| Additional domain reference | `growthhub.crm` |
| Similar domain identified | `growthhub.com` |

### 9.2 Social Engineering Indicators

- Recruitment invitation from an unfamiliar sender.
- Use of a free Gmail address for organizational recruitment.
- Request to complete an assessment through an external link.
- Request to confirm attendance by replying to the email.
- Request to bring a sensitive personal identification document (NIN).
- Telephone number associated with a negative Truecaller community label.
- No independently verified connection between the sender and the identified company website.

These observations do not individually prove malicious intent. Their combination justified treating the email with caution.

## 10. Risk Assessment

Based on the investigation, the email presented several potential risks.

| Risk | Explanation | Assessment |
|---|---|---|
| Identity theft | NIN could potentially be misused if collected by an untrustworthy party | High concern |
| Phishing | Assessment link could potentially be used to collect personal information | Requires caution |
| Social engineering | Interview invitation could be used to manipulate the recipient into taking an unsafe action | High concern |
| Physical safety | Attending an unverified interview location could expose the recipient to physical harm | High concern |
| Email impersonation | Sender's relationship with the organization could not be independently verified | Unresolved |

### Overall Risk Assessment

**Suspicious – Potential Recruitment-Based Social Engineering**

The combination of an unverified sender, request for sensitive identification, external assessment link, and physical interview invitation justified a cautious approach.

However, the available findings did not conclusively establish that the sender was a scammer or that the assessment link was malicious.

## 11. Recommended Defensive Actions

Based on the findings, the following actions are recommended:

1. Do not submit personal information, especially NIN details, through an unverified assessment link.
2. Independently contact the organization through contact details obtained from its verified website or other trusted sources.
3. Do not attend an unfamiliar interview location until the recruiter, organization, and appointment have been independently verified.
4. Avoid replying to suspicious emails or providing additional personal information.
5. Do not download or open unexpected attachments.
6. Continue monitoring suspicious URLs and IP addresses using reputable threat intelligence platforms.
7. Preserve the original email, full headers, screenshots, and investigation results as evidence.
8. Report suspected recruitment fraud to the appropriate authorities or relevant platform.

## 12. Investigation Limitations

Some limitations affected the investigation:

- A clean VirusTotal result does not guarantee that a URL is safe.
- AbuseIPDB reports against shared CDN infrastructure cannot automatically be attributed to one website.
- The exact relationship between the associated IP address and the assessment URL was not independently established.
- SPF, DKIM, and DMARC passing does not prove that the sender is a legitimate recruiter.
- DNS records establish technical configuration but do not prove company ownership or sender affiliation.
- Truecaller reputation labels are user-generated and may not be accurate.
- No independent confirmation was obtained from the organization establishing that the recruitment invitation was genuine.

These limitations were considered when reaching the final verdict.

## 13. Final Investigation Conclusion

The investigation began after I received a recruitment email claiming to represent Growth Hub. The message invited me to attend a physical interview, complete an assessment through an external link, confirm my availability by replying, and bring my NIN.

Although the email passed SPF, DKIM, and DMARC authentication checks, this did not establish the legitimacy of the sender.

The assessment URL returned no malicious detections on VirusTotal at the time of checking. However, the associated IP address had an AbuseIPDB abuse confidence score of 31%, with 203 reports from 62 distinct reporters. Since the IP was associated with shared CDN infrastructure, these reports could not be directly attributed to the recruitment website.

The domain investigation identified publicly configured DNS records for `thegrowthhub.africa`, but the `growthhub.crm` reference returned no DNS records and was not listed as a delegated public top-level domain in the IANA Root Zone Database.

The telephone number also received a negative community reputation label on Truecaller.

Taken together, these findings raised sufficient concerns to treat the recruitment email as suspicious. The request for NIN information and the invitation to attend a physical location made independent verification particularly important.

**Final Verdict: Suspicious Recruitment Email – Potential Social Engineering.**

The available evidence was not sufficient to confirm that the email was a scam. However, there was also insufficient evidence to establish that the sender was genuinely affiliated with Growth Hub.

The appropriate security decision was to avoid sharing sensitive information or attending the proposed interview until the invitation and sender could be independently verified.

## 14. Lessons Learned

This investigation reinforced several important lessons about email security and social engineering:

- Email authentication is not the same as sender legitimacy.
- A clean URL reputation result does not guarantee that a website is safe.
- IP reputation results must be interpreted carefully, especially when shared hosting or CDN infrastructure is involved.
- DNS records can provide useful technical information but cannot independently establish ownership or affiliation.
- Similar domain names should be investigated without assuming they belong to the same organization.
- Requests for sensitive identification during recruitment should be treated carefully.
- Physical interview invitations from unverified recruiters can introduce risks beyond ordinary email phishing.

Most importantly, the investigation demonstrated the value of examining an email beyond its appearance and considering both technical indicators and the real-world actions requested from the recipient.

## 15. Evidence Collection

The following screenshots and supporting materials should be included in the GitHub repository.

| Evidence ID | Evidence Description |
|---|---|
| E01 | Original recruitment email |
| E02 | Email header and authentication results |
| E03 | VirusTotal assessment URL results |
| E04 | AbuseIPDB IP reputation results |
| E05 | DNSDumpster results for `thegrowthhub.africa` |
| E06 | DNSDumpster results for `growthhub.crm` |
| E07 | DNS Twister similar-domain results |
| E08 | Truecaller telephone number result |


## 16. References and Investigation Resources

- VirusTotal – https://www.virustotal.com/
- AbuseIPDB – https://www.abuseipdb.com/
- DNSDumpster – https://dnsdumpster.com/
- DNS Twister – https://dnstwister.report/
- Truecaller – https://www.truecaller.com/

## 17. Disclaimer

This report documents a personal defensive security investigation conducted for educational and portfolio purposes.

The findings are based on the information and tool results available at the time of analysis. The report does not constitute a formal attribution of criminal activity to any individual or organization.

The investigation's verdict reflects the available indicators and the need for caution, not a confirmed determination of fraud.
