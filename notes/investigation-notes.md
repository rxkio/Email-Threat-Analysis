# Growth Hub – Investigation Notebook

These are my working notes from investigating a recruitment email that raised security and personal safety concerns. I used this file to keep track of the checks I performed, the observations I made, and questions that came up during the investigation.

## Investigation Log

### 01 – Reviewing the Email

**What caught my attention?**

- The invitation was for a physical interview.
- I was expected to complete an assessment through an external link.
- I was asked to reply to confirm whether I could attend.
- The email instructed me to bring my NIN.
- A telephone number was provided.
- The sender used `growthhubcrmltd@gmail.com`.

**My initial concern:** I wanted to establish whether this was a genuine recruitment process before sharing information or attending the proposed location.

**Evidence:** E01-original-email.png

### 02 – Checking the Email Headers

**What I wanted to establish:** Whether the email passed authentication checks and what infrastructure was involved in delivering it.

**Checks performed:**

- SPF
- DKIM
- DMARC
- Received headers

**What I found:**

- SPF passed.
- DKIM passed.
- DMARC passed.
- The message appeared to have travelled through Google's infrastructure.

**My observation:** The authentication results were successful, but that did not answer the more important question: was the person behind the email actually connected to Growth Hub?

**Evidence:** E02-email-header.png

### 03 – Investigating the Assessment Link

**Tool:** VirusTotal

I submitted the assessment link from the email to VirusTotal.

**Result:** No malicious detections were returned at the time I checked it.

**Question I considered:** Does a clean VirusTotal result mean the link is safe?

**My conclusion:** No. A URL can be new, unreported, or used for targeted social engineering without being detected by security vendors.

**Evidence:** E03-virustotal.png

### 04 – Checking the Associated IP

**Tool:** AbuseIPDB

I checked an associated IP address to see whether it had a history of abuse reports.

**Results recorded:**

- Abuse confidence score: 31%.
- Total reports: 203.
- Distinct reporters: 62.
- Usage type: Content Delivery Network.
- ISP: Internet Utilities Europe and Asia Limited.
- ASN: AS13335.

Some reports mentioned phishing websites and crypto drainers.

**Something important I noticed:** The IP was associated with CDN infrastructure. This means multiple websites could share the same IP address.

**My conclusion:** The reputation score was worth investigating, but I could not assume that all the reports related to the Growth Hub assessment link.

**Evidence:** E04-abuseipdb.png

### 05 – Looking Into the Company's Website

**Tool:** DNSDumpster

I identified `thegrowthhub.africa` as a website associated with the Growth Hub name. Since the organization appeared to have an existing online presence, I decided to investigate its DNS records.

**What I found:**

- A record for `www.thegrowthhub.africa`.
- IP address: `159.198.67.178`.
- Hosting network associated with Namecheap.
- MX records associated with Registrar Servers.
- Nameservers associated with Registrar Servers.
- An apparent SPF TXT record.

**Why I checked this:** I wanted to understand whether the company had a publicly configured domain and what infrastructure it used.

**My observation:** Having an active website and DNS records does not prove that the Gmail sender was affiliated with the organization.

**Evidence:** E05-dns-thegrowthhub-africa.png

### 06 – Investigating the .crm Reference

**Tool:** DNSDumpster

After checking the `.africa` domain, I also searched for `growthhub.crm` to see whether it returned any DNS records.

**Result:** No A, AAAA, MX, NS, or TXT records were returned.

I then checked the IANA Root Zone Database.

**Additional finding:** `.crm` was not listed as a delegated public top-level domain.

**My observation:** I could not verify this domain reference through the checks performed.

**Evidence:** E06-dns-growthhub-crm.png

### 07 – Checking the Similar Domain

**Tool:** DNS Twister

I used DNS Twister to look for similar domain names.

**Result:** `growthhub.com` appeared among the similar-domain results.

**Question:** Was this domain connected to the company or the recruitment email?

**Finding:** I could not establish any verified ownership or affiliation.

**Evidence:** E07-dns-twister.png

### 08 – Checking the Telephone Number

**Tool:** Truecaller

I searched the telephone number included in the recruitment email.

**Result:** Truecaller displayed the label "Job scammer".

**My observation:** This was concerning, but I treated it cautiously because Truecaller labels can be based on community reports and are not official confirmation.

**Evidence:** E08-truecaller.png

---

## Things I Need to Be Careful About

During the investigation, I identified a few things that could easily lead to incorrect conclusions:

1. Passing SPF, DKIM, and DMARC checks does not mean an email is legitimate.
2. A clean VirusTotal result does not guarantee a URL is safe.
3. An IP with abuse reports may be shared by unrelated websites.
4. A company's website does not automatically authenticate someone claiming to represent it.
5. Similar domain names do not establish common ownership.
6. A Truecaller warning is an indicator, not proof.

## Questions That Guided My Investigation

- Who actually controls the sender's Gmail account?
- Is the recruiter genuinely affiliated with the organization?
- What information does the assessment link request?
- Is the telephone number officially associated with the company?
- Can the proposed interview and location be independently verified?

These questions helped me avoid relying on one tool or one finding to make a decision.

## Evidence Checklist

- [ ] E01 – Original recruitment email
- [ ] E02 – Email header
- [ ] E03 – VirusTotal results
- [ ] E04 – AbuseIPDB results
- [ ] E05 – DNSDumpster `.africa` results
- [ ] E06 – DNSDumpster `.crm` results
- [ ] E07 – DNS Twister results
- [ ] E08 – Truecaller results

## Final Personal Takeaway

The biggest lesson from this investigation was that suspicious emails should not be judged by appearance alone.

The email passed authentication checks, and the assessment link did not receive malicious detections on VirusTotal. However, those findings did not establish that the recruitment invitation was genuine.

Looking at the technical indicators alongside the actual requests made in the email helped me identify why further verification was necessary.
