---
layout: post
title: Pre-workshop report
image: "/content/images/2017/01/board.jpg"
---

*Confidential - do not distribute outside of your organization*

#### Introduction
This documents outlines Tradle’s recent development activities undertaken for the PoC and other developments that directly and indirectly benefit the PoC.
#### Document scanning and biometrics
The technology for document scanning and matching to customer’s faces has matured to be reliably used in the KYC, onboarding and authentication processes.

Tradle continuously evaluates service providers in this area, based on quality of service, features completeness, regional coverage, readiness to partner, ability to run on bank’s premises, complexity of integration, performance characteristics, and other criteria.

See the [report on this subject.](/p/c2b7c9d2-f968-40f5-adde-63e41735a2f5/)

#### Data Modeling 
See separate report for this

1. New verifications structure

 - More structured Verifications: what was verified, how it was done, based on what sources, and with what level of confidence, nested verifications
 - Evidentiary document models instead of images
 - Extracted data from scanned documents
 - Verification(s) per evidence document, not just per form
 - Choice of sharing for one (or more) evidentiary documents, not all
2. Wealth CV
#### Re-onboarding
1. Customer logs in and Scans the QR code (implemented via Demo Account + Use Script)
2. Download KYC data into the app and allow customer to view them (implemented by simulating a call to the bank’s back end)
3. Support viewing more structured and nested verifications, and the evidentiary documents
#### Third-party verifications, e.g. Tax Advisors
 1. Forwarding request to Tax advisor
 2. Sharing results back with the bank
 3. Coming up: user’s onboarding with the Tax advisor, potentially utilizing UBS-verified KYC.
#### Programmability of KYC policy
KYC codification allows to finally digitize business rules. Business rules will be executed partially on the server side and partially on the client side. Client-side execution may preserve privacy, by reducing the amount of information that would otherwise be shared with the provider. 

Client-side execution also potentially creates a much better user experience, with better interactivity, asking less questions to the client, making use of device sensors, not requiring constant connectivity (offline support). 

It is also allowing to reduce load on the server, and is in line with the trend of big data processing moving to the edge of the network. 
But it has its challenges, which we are working on to overcome, described in a separate report.
#### Digital Signatures and global interoperability 
Swiss Federal Electronic Signatures Act (ESA) is equivalent to eIDAS in that it recognized qualified signatures as equal to handwritten ones, and supports advanced signatures.

But there are challenges for cross-border KYC portability.
See separate report on this.
#### Real-time Regulatory Supervision 
See separate report on this

 1. Confidentiality and cyber-security with partial sharing
 2. Supervision report with real-time updates
 3. Applicability to correspondent banking, insurers-bank, broker-bank, family office-bank, bank-bank (like when UBS is providing investment analytics to another bank)

#### Planned development
 - Capture handwritten signatures
 - Use case 3 - source of wealth
 - Use case 4 - qualified investor
 - Increase privacy by masking identity when sharing between providers
 - Developing with the FCA the KYC portability conditions and cross-checks
 - Document scanning and face recognition: support more providers and perform comparative testing
 - Authentication with face-recognition
 - Login with mobile
 - Restoring lost devices onto new ones, based on prior pairing
 - Programmable KYC policy (bots / scripts / smart contracts)
 - Improve performance of end to end encryption so it can be used on mobiles (replacing OTR with Axolotl
 - Disposable (masked) identities - discuss with Mark
 - UBS Badges? - need to discuss Paul’s idea
 - Public launch of developer tools (possibly by Feb 10th). Tradle already has mobile and server-side Integration APIs and dev tools, but they are not yet public.
 - Longer term: AI / deep learning for detecting KYC data anomalies
#### Timestamping and anti-tampering with the blockchain
In Estonia a company Guardtime emerged with unique technology for tamper-proofing large numbers of database records. It is now used by all Estonian government databases (X-Road) and recently for public health records. The technology is marketed as blockchain-based, but in reality it is a proprietary closed source product, with the nodes run just by the Guardtime (they claim Erikson will be running the nodes too, which at best will make it a less secure version of the private blockchain). Recently a scalable open source variant with similar capabilities was created, called [Open Timestamps](https://petertodd.org/2016/opentimestamps-announcement "target="_blank), and is truly based on the blockchain, while being extremely scalable. 

Tradle is already proving the validity of signatures for individual items. But there is another problem, to prove the completeness of sequences of data, especially useful when sharing partial data with the regulators and counterparties. Tradle is planning to employ Open Timestamps or a similar principle for that.
#### Questions
Abandoned onboarding sessions

 1. Can client still use the received verifications?
 2. Forget me - should it keep the copy for the regulators? Even for abandoned sessions?

#### Consortium
Pricing, including pricing for sub-providers, like Onfido, Thomson Reuters
Interoperability inside the country, between the countries
