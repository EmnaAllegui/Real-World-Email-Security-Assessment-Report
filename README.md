# Real-World Email Security Assessment Report

---

## Objective

The objective of this assessment is to evaluate the email security posture of multiple real-world domains by analyzing their SPF, DKIM, and DMARC configurations.

The scenario focuses on identifying misconfigurations, weak authentication mechanisms, and potential spoofing risks.

---

## Skills Learned

- Understanding how SPF, DKIM, and DMARC work together to protect email communication
- Identifiying common misconfigurations such as excessive DNS lookups and multiple DNS records   
- Learning how DMARC enforcement depends on SPF and DKIM alignement
- Analyzing emails using dig tool  
- Understanding weaknesses in email authentication

---

## Environment
- Kali Linux  
- Tools: dig, nslookup  

---

## Tasks

### SPF Analysis
- Count DNS lookups (limit: 10)  
- Identify misconfigurations  

### DMARC Analysis
- Check policy enforcement (reject/quarantine)  
- Verify reporting configuration  

### DKIM Validation
- Check multiple selectors  
- Confirm key presence  

### Correlation
- Evaluate spoofing possibility  
- Identify weakest mechanism  

### Report Output
- Findings  
- Risk level  
- Recommendations  

---


## Introduction

Email remains one of the primary vectors for phishing and spoofing attacks.  
This report evaluates the email authentication posture of multiple domains by analyzing SPF, DKIM, and DMARC configurations for a given domains. The analysis identified:

- Excess of DNS lookup limit  
- Malformed SPF record  
- Use of an outdated SPF version  


---

## 1. Target Analysis

### 1.1 Google (google.com, gmail.com)

#### SPF Analysis
The analysis of google.com SPF record reveals:
• 2 DNS lookups: one include mechanism containing SPF record lookup. This indicates that the SPF record is properly configured and does not exceed the DNS lookup limit (10).
<img width="945" height="103" alt="image" src="https://github.com/user-attachments/assets/2a0716bc-e8fc-40be-afdc-0d97f5c2a20b" />

#### DMARC Analysis
The analysis of google.com and gmail.com DMARC indicates:
• The reject policy is enforced for google.com domain, indicating that emails failing DMARC authentication are blocked  
• The quarantine policy is enforced for gmail.com subdomain  
• Aggregate reporting email address is configured for google domain and subdomain   
<img width="945" height="132" alt="image" src="https://github.com/user-attachments/assets/4595c7fb-56ea-4d76-9fda-bb1425619169" />

#### DKIM Validation
DKIM validation confirms that:
• The public key is published in the DNS TXT record and successfully retrieved
<img width="945" height="107" alt="image" src="https://github.com/user-attachments/assets/e03abda9-0b19-4327-b453-aa6ec2a78393" />

---

### 1.2 Microsoft (microsoft.com, outlook.com)

#### SPF Analysis
The analysis of microsoft.com SPF record reveals:
• 8 DNS lookups, which is within the recommended limit (10)
<img width="945" height="563" alt="image" src="https://github.com/user-attachments/assets/14ef3ce2-f239-43a7-a821-e20ce27b24f5" />

#### DMARC Analysis
The DMARC analysis indicates that:
• The reject policy is enforced, ensuring that all emails failing DMARC authentication are blocked  
• Aggregate and forensic reports are configured  
• Forensic reports are generated if SPF or DKIM FAIL   
<img width="945" height="71" alt="image" src="https://github.com/user-attachments/assets/28a148e4-5d45-4de5-a59f-20716d906c90" />

#### DKIM Validation
DKIM validation confirms that:
• The public key is published in the DNS TXT record and successfully retrieved   
<img width="945" height="148" alt="image" src="https://github.com/user-attachments/assets/9c05b4c5-97b7-4255-a6b5-324d5f841e6b" />

---

### 1.3 Facebook (facebook.com)

#### SPF Analysis
The analysis of facebook.com SPF record reveals:
• 2 DNS lookups: one redirect mechanism containing another SPF record. This is within the recommended limit (10) 
<img width="944" height="106" alt="image" src="https://github.com/user-attachments/assets/46127b1e-e978-4777-923e-4e6f4c70a824" />

#### DMARC Analysis
The DMARC analysis indicates that:
• The reject policy is enforced  
• Aggregate and forensic reports are configured  
• No alignment tags (aspf, adkim), default relaxed alignment used    
<img width="945" height="70" alt="image" src="https://github.com/user-attachments/assets/288459c1-19e9-421f-a3ed-ac058e624dc1" />

#### DKIM Validation
DKIM validation confirms that:
• The public key is published in DNS TXT record and successfully retrieved   
<img width="945" height="96" alt="image" src="https://github.com/user-attachments/assets/5a50bab9-9f25-4f76-b73a-3d581c190980" />

---

### 1.4 Amazon (amazon.com, aws.amazon.com)

#### SPF Analysis
The analysis of amazon.com SPF record reveals:
• Multiple SPF records detected  
• Outdated SPF version: SPF2.0/pra  
• 5 DNS lookups in total including nested includes  
• No SPF record for subdomains
<img width="945" height="561" alt="image" src="https://github.com/user-attachments/assets/5ff46f5a-dd25-48c3-b944-de69ac301feb" />

#### DMARC Analysis
The DMARC analysis reveals that:
• The quarantine policy is enforced  
• Aggregate and forensic reports are configured  
• DMARC not fully enabled for subdomains 
<img width="944" height="43" alt="image" src="https://github.com/user-attachments/assets/eb608132-2d55-4efb-a581-1b4e24aa36a0" />

#### DKIM Validation
DKIM validation confirms that:
• The public key is published in DNS TXT record and successfully retrieved   
<img width="945" height="105" alt="image" src="https://github.com/user-attachments/assets/fc93b348-ef05-4cac-866d-65b9329c0019" />

---

### 1.5 Netflix (netflix.com)

#### SPF Analysis
The SPF analysis reveals:
• 8 DNS lookups in total including includes  
• Within recommended limit (10)
<img width="945" height="563" alt="image" src="https://github.com/user-attachments/assets/f616589e-d8e2-4ee8-a71b-a72a04066c9b" />

#### DMARC Analysis
The DMARC analysis reveals:
• The reject policy is enforced  
• Aggregate and forensic reports configured  
• Forensic reports generated if SPF and DKIM FAIL  
<img width="945" height="88" alt="image" src="https://github.com/user-attachments/assets/0ac44c4c-397e-4298-a572-5ee0e6acf76d" />

#### DKIM Validation
DKIM validation confirms:
• Public key is published in DNS TXT record and successfully retrieved 
<img width="945" height="94" alt="image" src="https://github.com/user-attachments/assets/f6e102af-1b68-4a6d-a3e0-8317ea97d82a" />

---

### 1.6 X (x.com)

#### SPF Analysis
The SPF analysis reveals:
• 7 DNS lookups in total including include and exists mechanisms  
• Within recommended limit  
<img width="945" height="420" alt="image" src="https://github.com/user-attachments/assets/29d06fc1-0c55-49d8-8f9d-a6f324539910" />

#### DMARC Analysis
The DMARC analysis reveals:
• The reject policy is enforced  
• Aggregate reports configured 
<img width="945" height="69" alt="image" src="https://github.com/user-attachments/assets/37a42710-8203-40cf-8aff-14fd005628fc" />

#### DKIM Validation
DKIM validation confirms:
• Public key is published and successfully retrieved 
<img width="945" height="79" alt="image" src="https://github.com/user-attachments/assets/81718cd3-0002-4f20-8031-f72fea3abe82" />

---

### 1.7 PayPal (paypal.com)

#### SPF Analysis
The SPF analysis reveals:
• 10 DNS lookups including nested includes  
• Malformed SPF record detected in 3ph4._spf.paypal.com  
• ~all indicates emails failing SPF are forwarded to spam  
<img width="945" height="471" alt="image" src="https://github.com/user-attachments/assets/deb25ab7-80bc-46f0-83d3-63f0e14dd06a" />
<img width="945" height="201" alt="image" src="https://github.com/user-attachments/assets/8a90b398-5a8d-41c9-bcf2-9352c03d8e3c" />

#### DMARC Analysis
The DMARC analysis reveals:
• The reject policy is enforced  
• Aggregate and forensic reports configured  
<img width="945" height="69" alt="image" src="https://github.com/user-attachments/assets/ecc89948-8f72-4320-8f66-37c8ef2f7d26" />

#### DKIM Validation
DKIM validation confirms:
• Public key is published in DNS TXT record and successfully retrieved  
<img width="945" height="78" alt="image" src="https://github.com/user-attachments/assets/7a8d0410-90c3-499f-a512-e2ebdb4203b6" />

---

### 1.8 Shopify (shopify.com)

#### SPF Analysis
The SPF analysis reveals:
• 5 DNS lookups including nested includes  
• ~all indicates emails failing SPF are sent to spam  
<img width="945" height="340" alt="image" src="https://github.com/user-attachments/assets/cacc2ef0-a3ba-47e4-b2c7-b6e8741d722a" />

#### DMARC Analysis
The DMARC analysis reveals:
• The reject policy is enforced  
• Aggregate and forensic reports configured  
<img width="945" height="70" alt="image" src="https://github.com/user-attachments/assets/724eea86-c88e-4969-a8b7-bdd0d12742b1" />

#### DKIM Validation
DKIM validation confirms:
• Public key is published in DNS TXT record and successfully retrieved
<img width="945" height="80" alt="image" src="https://github.com/user-attachments/assets/ced800a8-110d-4b8c-93fc-f188d8eeb190" />

---

### 1.9 Dropbox (dropbox.com)

#### SPF Analysis
The SPF analysis reveals:
• 8 DNS lookups including nested include mechanisms  
• ~all indicates emails failing SPF are forwarded to spam  
<img width="945" height="380" alt="image" src="https://github.com/user-attachments/assets/1a6f4af0-01a2-45c7-9f88-676be626e256" />

#### DMARC Analysis
The DMARC analysis reveals:
• The reject policy is enforced  
• Aggregate reports configured  
<img width="945" height="73" alt="image" src="https://github.com/user-attachments/assets/35431eb3-5e7f-4e96-a537-7b12bb77d624" />

#### DKIM Validation
DKIM validation confirms:
• Public key is published and successfully retrieved  
<img width="945" height="96" alt="image" src="https://github.com/user-attachments/assets/20919789-c8e5-4616-964c-3013b2087505" />

---

### 1.10 GitHub (github.com)

#### SPF Analysis
The SPF analysis reveals:
• 11 DNS lookups (exceeds recommended limit)  
• Multiple include mechanisms and nested includes  
• ~all indicates emails failing SPF are forwarded to spam  
<img width="945" height="443" alt="image" src="https://github.com/user-attachments/assets/c1b5478b-5e43-433f-8eec-8814c982f1be" />

#### DMARC Analysis
The DMARC analysis reveals:
• Quarantine policy for domain  
• Reject policy for subdomains  
• Aggregate and forensic reports configured  
<img width="945" height="73" alt="image" src="https://github.com/user-attachments/assets/e60f152d-07ff-4e0a-bf74-98211ae708d8" />
#### DKIM Validation
DKIM validation confirms:
• Public key is published in DNS TXT record and successfully retrieved  
<img width="945" height="81" alt="image" src="https://github.com/user-attachments/assets/4bdac53a-4d99-42d7-9684-163c57ac2753" />


---

## 2. Findings
## Findings

| Domain       | SPF protocol                                             | DKIM protocol        | DMARC protocol      | Weak mechanisms                               | Is spoofing possible                          |
|-------------|----------------------------------------------------------|----------------------|---------------------|----------------------------------------------|----------------------------------------------|
| Google.com  | Within the recommended DNS lookups limit                 | Properly configured  | Strong DMARC        | No weak mechanism                             | Protected from spoofing attacks              |
| Microsoft.com | Within the recommended DNS lookups limit              | Properly configured  | Strong DMARC        | No weak mechanism                             | Protected from spoofing attacks              |
| Facebook.com | Within the recommended DNS lookups limit                | Properly configured  | Relaxed DMARC       | No weak mechanism                             | Protected against spoofing                   |
| Amazon.com   | More than one SPF per TXT / Outdated SPF version / Within DNS lookup limit | Properly configured | Properly configured | Weak SPF mechanism                            | Possible spoofing attacks if DKIM FAIL       |
| Netflix.com  | Within the recommended DNS lookups limit               | Properly configured  | Strong DMARC        | No weak mechanism                             | Protected from spoofing attacks              |
| x.com        | Within the recommended DNS lookups limit               | Properly configured  | Properly configured | No weak mechanism                             | Possible SPF attacks                         |
| Paypal.com   | Within the recommended DNS lookups limit / Malformed SPF record / Not fully protected (~all) | Properly configured | Strong DMARC        | Weak SPF mechanism                            | Possible spoofing attacks if DKIM FAIL       |
| Shopify.com  | Within the recommended DNS lookup limit / Not fully protected (~all) | Properly configured | Strong DMARC        | Weak SPF mechanism                            | Possible spoofing attacks if DKIM FAIL       |
| Dropbox.com  | Within the recommended DNS lookups limit / Not fully protected (~all) | Properly configured | Strong DMARC        | Weak SPF mechanism                            | Possible spoofing attacks if DKIM FAIL       |
| Github.com   | Exceeds the recommended DNS lookup limit / Not fully protected (~all) | Properly configured | Strong DMARC        | Weak SPF mechanism                            | Possible spoofing attacks if DKIM FAIL       |
---

## 3. Risk Level

| Domain              | SPF Protocol                         | DKIM Protocol            | DMARC Protocol | Risk Level  |
|--------------------|--------------------------------------|--------------------------|----------------|------------|
| Google.com         | DNS lookup < 10                     | Properly configured      | p=reject       | Low level  |
| Microsoft.com      | DNS lookup < 10                     | Properly configured      | p=reject       | Low level  |
| Facebook.com       | DNS lookup < 10                     | Properly configured      | p=reject       | Low level  |
| Amazon.com         | Misconfiguration / DNS lookup < 10  | Properly configured      | p=quarantine   | Medium level |
| Netflix.com        | DNS lookup < 10                     | Properly configured      | p=reject       | Low level  |
| X.com              | DNS lookup < 10                     | Properly configured      | p=reject       | Low level  |
| Paypal.com         | DNS lookup = 10 / ~all              | Properly configured      | p=reject       | Low level  |
| Shopify.com        | DNS lookup < 10 / ~all              | Properly configured      | p=reject       | Low level  |
| Dropbox.com        | DNS lookup < 10 / ~all              | Properly configured      | p=reject       | Low level  |
| Github.com         | DNS lookup > 10 / ~all              | Properly configured      | p=quarantine   | Medium level  |

---

## 4. Recommendations
- Reduce DNS lookups (≤ 10)  
- Avoid multiple SPF records  
- Remove unused mechanisms  
- Avoid outdated SPF versions  
- Enforce strict SPF policies  
- Enforce DMARC reject policy everywhere  
- Limit authorized mail servers  

---

## Conclusion

The assessment of the analyzed domains reveals that SPF is the weakest mechanism for some organizations. It should be properly configured and in accordance with the best recommended practices.
SPF plays a crucial role in the overall email security posture, as DMARC authentication relies on both SPF and DKIM authentication. If Both authentication FAIL, DMARC authentication also FAIL increasing the likelihood of successful spoofing attacks.
