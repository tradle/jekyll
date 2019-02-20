---
layout: post
title: Document scanning and biometrics
image: "/content/images/2017/01/print.jpg"
---


*Confidential - do not distribute outside of your organization*
### Introduction

A person getting access to financial services needs to pass through the KYC process. This is applicable to simple retail banking, trading, wealth management, and also to those who own the business or is an ultimate beneficial owner of the business (UBO), a director of the business. 

To onboard a person in the above capacities a government issued document, photo ID, is required. This could be a passport, ID card, driving license, possibly in combination with travel visa, and residence permits. 
  
Such photo ID documents can be authenticated automatically with the following methods:


 1. Image analysis and Optical Character Recognition (OCR) for data extraction
 2. MRZ zone on passports, visas, and ID cards (see more technical info on MRZ)
 3. Barcodes (e.g. 2D barcode on the back side of US driving licenses)
 4. NFC chips on documents

After document is scanned, the person could take a selfie, which could then be matched to a photo in the document.

Device cameras, both rear and front, have greatly improved in recent years, yet scanning with your mobile’s camera present numerous challenges compared to stationary equipment. Inconsistent lighting, reflective surface of the document, angle and contrast of the surface, and the possibility of fraud in this self-service environment need to be addressed. See for example one of the newly emerged techniques, called multi-frame integration.

### Document scanning
Tradle focuses on providers that do fully automatic scanning of documents, as opposed to using teams of people to analyze the documents. Automatic scanning is faster, thus offering a much better user experience, and if server can be installed on-premises, it avoids shipping data oversees, which is great for data locality compliance.

Document scanning does OCR of data printed on the document, compares it to MRZ, barcode, NFC chip data and detects possible alterations or any other forgery of the document. 
#### We integrated with the following providers
 1. Onfido - elaborate and very complex API for scanning documents and background checking. Falls back to human teams if software fails to credible scan the documents. API published on their web site. Provides the sandbox for testing, but it returns canned responses, does not process live documents, which makes testing much harder, and demoing impossible.
 2. Au10tix - just software, no human team. Automatic detection of document type (e.g. passport, driving license). Much simpler API, but it is not public and not documented as well. Provides API keys for testing. Provides real-life document scanning in sandbox. About 5-10 seconds to analyze the document. 
#### Planning to integrate with
Paycasso. Paycasso is quite advanced, but no public API, no established partnership program with software vendors, so engagement is extremely complicated (had 2 meetings already with the CEO, but still no access to API for testing).
IDScan - in addition to other capabilities, reads NFC and supposedly checks the hologram. Supposedly the most mature solution on the market, but company policy is direct sales, does not allow software vendors to resell. We are trying to get them to make an exception for us.

### On-device document scanning and data extraction

What we have learned is that to achieve high quality of document scanning it is imperative to scan documents on the device. 

On-device software can provide instant feedback for the user with real-time recognition, which means that instead of taking a picture, which is later analyzed on the server, the software is processing a video stream locally and only takes the picture, when it is good enough to extract the data. This is especially important on lower end devices with less sophisticated cameras. On-device scanning helps:

 1. To take picture in focus, with less glare, with better lighting, higher enough contrast to recognize document edges, perspective (not too much tilted), etc.
 2. To instantly pre-fill online forms with data extracted from the document. This also serves as the indication that document could be recognized.
 3. Detect that the type of document, avoiding the need to ask the user this question, and to be able to guide the use to scan the back side of the document, by detecting the front side (e.g. US licenses have back tide, but UK do not).
 4. With preserving privacy, as can support offline mode without server connection

Having software on the device also allows to read NFC chip on modern documents (this only works on Android Phones at the moment as Apple does not publish an API to the NFC chips in iPhones). 

Note: In order to read the data on NFC chip it is necessary to first to read the MRZ zone, the data from which is used to decode the NFC chip’s contents. 

NFC chip has customer’s data that is more reliable than could be obtained via optical character recognition (OCR) of the document. In fact it can be cross-checked with the OCR and with the MRZ zone. 

NFC chip also contains a high-quality image, which can later be used for face recognition.
#### We tested the following providers
Providers below offer mobile apps for testing, which we used to evaluate their solutions.


 1. Anyline MRZ - extremely fast MRZ reading. Does not read UK driving licenses, as they do not have MRZ, nor any barcodes.
 2. BlinkID - reads MRZ reliably, if slowly. Very dependent on lighting conditions, and surface contrast to the document. Limited coverage of driver licenses (US, UK).
 3. MRZ Recognition by Russian company Smart Engines
 4. ReadID - scans MRZ and NFC. NFC reading is tricky, UK passports can be read on the cover. US passport needs to be open, scanning can be done only by putting the phone on top of the backside of the page that has a photo.

Issues that need to be addressed

- None of the providers above do automatic document type detection, so a user needs to specify the which document they are scanning

- None of the providers above do automatic detection on whether the document is one sided or two-sided. For example UK driving license is one-sided, and US is two-sided. Same with EU ID Cards, some one, others are two-sided. This means we unfortunately have to ask the user to scan both sides, even when it is not needed.
- For NFC customer needs instructions on how to scan it, and they depend on the country of passport issue and even possibly the year of issue. 
- NFC reading takes about 10 seconds, so customer needs to be told to hold still, otherwise the reading fails.

Based on the above we need to build a database of all types of documents and give customers instructions on how to do the scanning properly to increase customer conversion.
#### Face recognition
Facial recognition has entered the mainstream. Pioneered in mass by Facebook to suggest friend’s faces in photos for tagging, it is now followed by Google and recently by Apple. Microsoft offers several Face APIs for developers, from face matching, detecting faces in images (useful for passports), age and emotion detection. Google is offering similar APIs.

NEC Neoface - supposedly highest quality and performance, but extremely difficult to integrate with at the moment.
Daon - used by the Mastercard.
MS Face API - tested by Uber for driver authentication (along with other providers, likely Daon as well, none in production at Uber)

#### Planning to test
[Facetec](https://facetec.com/ "target="_blank)  
[Hypr](hypr.com)  
Liveness detection
This is the term used to detect a video/photograph/3D model instead of a live face (face spoofing detection). There are several mechanisms in development, but they have not reached a production level yet.
Low level components
These components can be used to build full document scanning and face matching capabilities:


Edge detection and perspective correction
MRZ zone OCR
Another barcode reader
Face matching using MS Face API (in React native)
http://jmrtd.org/

Face matching to document
Face matching requires an ability to detect a picture on the image of the document and extract it to enroll the person. Then this picture can be used to match with the selfie taken by the person on their device (mobile or webcam). The problem here is that the photo in the document is usually small (unless extracted from the NFC chip), and has laminate and holograms on top, which cause the glare. Another problem, photo needs to be automatically extracted from the document.
We are preparing to test with the following providers
Neither so far gave us the API key to perform this type of testing. 
Onfido
Au10tix
And later with those providers
Paycasso
Microsoft Face API (does not extract a photo from the document, need to implement it ourselves)
Google API (same issue as with MS)

Note: One of the important considerations for financial industry whether the provider can work on-premises. Neither Microsoft nor Google provide that option. Given the choices, we will have to explore if we can build our own solution, out of the smaller, focused components.

Sanctions and other background checks
It is not enough to verify the documents themselves, and that they match a person. Documents can be revoked, and the person may be on sanctions lists (there are a number of lists published by different countries) or a politically exposed person (PEP) who needs special treatment. PEP lists are especially difficult as there is no official lists like with sanctions. And bad press is much harder to automate as it is completely unstructured data.
We are planning to test with the following providers
ComplyAdvantage, claims to have 4M PEP records, compared to TR WorldCheck, see below, which has 1.2M records.
Onfido uses ComplyAdvantage for sanctions and PEP scanning
Other providers in this area
Thomson Reuters WorldCheck - the staple of sanctions and PEP checking. Only recently added an API.
KYC3 - a startup that is combining machine reading of news (for bad press) cross-matched with the sanctions lists. Claims to greatly reduce the amount of manual checking that normally needs to be done based on news archives. Has archives for only 3 years, so for prior years resells other archives, like TR and Factiva.
Accuity. No API, data is provided in the form of CSV files for processing on premises. Has advantage in data locality, but some disadvantage in the need to perform refreshes and build your own searching capabilities. 
Factiva. Provides news articles archives for bad press checking.

Address verification

Address verification can be done in several ways:

Unverified customer’s statement, but if customer is aware that they go on record (on blockchain), it has higher value.
Utility bill (unreliable, 18% fraud rate is cited)
Verification by the Post Office. The challenge here is how to collect this verification from Post Office electronically, as opposed to just a snapshot of the paper document.
Verification by Notary (may be Tax advisor can perform this as well?)
Letter sent by provider to the customer with the number to be entered online. Onfido provides this services, and it is costly ($2.5-3 per letter. if purchased at volume prices). This approach also creates several day delay which may cost the loss of customer.
Electronic integration with the Gas/Electric/Broadband utility. This approach could give best results. It would be important to find a way to identify utility’s customer, and to collect their consent. It can be achieved by asking customer to log into utility’s web site and scan a QR code.

Business registrations
For the source of wealth purposes, the Articles of Incorporation and other business documents, like the sale of the business, will need to be verified for authenticity (they also need to be OCR-ed for document searching in the future). 
 
TBD
