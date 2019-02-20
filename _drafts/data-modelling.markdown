---
layout: post
title: Data modelling
featured: true
---

### Introduction
By codifying KYC collection, verification and conditions for KYC exchange, we aim to achieve 100% KYC automation. 

Automation of KYC is necessary to remove the distortions in the financial system caused by it while achieving its goal of preventing financial crime, yet achieving it without gross reduction of privacy and commercial confidentiality.

Distortions in financial system are:


 - Urgent problem of derisking, demarketing in 19 world regions
 - Off-boarding customers due to high hurdle rates, leaving customers underserved
 - Inability to serve the whole customer groups, increasing financial exclusion
 - Gross inefficiencies (useless repetitive actions that stop the business)
 - The anticompetitive incentives, e.g. corporates are forced to have smaller number of banking relationships, some have reduced it to just one bank
 - Outdated account-based vs. services-based model
 - High barrier to entry for innovation
 - Over-governance, leading to high risk for internal innovation

KYC is expensive and extremely inconvenient for the customers of financial institutions. One way to improve it is to share the burden between financial institutions, to achieve KYC portability. To achieve portability we will have to fix many other aspects of KYC. Today KYC portability is limited by several factors:

 1. Collection of KYC is not digitized, thus it is not portable
 - But even if it was digitized, will it be understood if exchanged, as it is not standardized?
 - And if it is standardized, will then jurisdictional and company-specific policies work?
 - And even if it was standardized and thus understood if exchanged, can it be trusted?
 - And even if it was trusted, will exchanging sensitive KYC not violate customers privacy and confidentiality?
 - And if it was privacy preserving, how can regulators be persuaded to allow [controlled] reuse of KYC verifications, as reuse may create a house of cards effect, i.e. one mistake undetected, reused over and over by many.

### Problem analysis

 1. We need to be able to codify what was verified, how it was verified, based on what sources and with what level of confidence. We also need to capture and store all evidentiary documents. 


 - Documents will need their own data models, as passport has different fields from the driver license, and the data collected from the documents must be preserved for future 
analysis. 


 - Different documents and other objects have very specific aspects that can be verified, i.e. ‘what was being verified’, e.g. the address exists and was verified by visiting it, personal info for presence on sanctions lists. Documents are verified for authenticity, and photo ID documents are verified on their ownership.

 - Verifications may have multiple sources. Verified by the in-person examination, verified via digital scanning, verified by calling customer’s number, by visiting the customer’s location, by witnessing customer sign in my presence, etc.


 - Allow customers to share only some documents and their verifications, but not the others (e.g. driver license, but not the passport).


 - Allow provider to intelligently query customer for data, minimizing the amount of interactions with the customer. Queries can be arbitrarily complex and reflect the business rules and compliance policies of the provider, yet protect customer’s privacy (see the design document for this). Example:

Please provide PersonalInfo, as verified based on required documents, e.g. swiss passport, or EU passport, but only if the person was EU born, or lives in the EU for over 10 years, and only if verified by another Tier 1 bank, and only if it was done based on Onfido or Au10tix, and only in the last 2 years (as before that they were very sloppy). Otherwise ask customer to scan the same ID document again.

### Hierarchy of proofs

Evidentiary documents will have their own corresponding forms. Forms like PersonalInfo, which go together with supporting documents, will be sent together with one of those evidentiary document forms, but neither will point to the other (no backlinks/forward links in the object body). Verifications for supporting documents will point to supporting documents. Verifications for PersonalInfo will point to PersonalInfo, but "sources" will be verifications for supporting documents.  

    the UI flows:
    simple:
      Aviva: 'give us PersonalInfo'

      customer UI:
        please fill out PersonalInfo or share one of these 10 combinations you already had verified:
          PersonalInfo as verified by Johnny Cash Company based on Passport
          PersonalInfo as verified by Led Zeppelin Company based on Driver's License
          ...
    slightly more complex:
      1: customer already has PersonalInfo verified with Passport by Paul McCartney
        Aviva: 'give us PersonalInfo with Passport or Driver's License
        customer UI: please fill out PersonalInfo...or share as verified by Paul
      2: customer only has PersonalInfo with Social Security Card
        Aviva: 'give us PersonalInfo with Passport or Driver's License
        customer UI: please fill out PersonalInfo...
          customer clicks, is asked to scan a Passport or Driver's License

jsonQuery(personalInfo.verifications[what = ‘authenticity’] && personalInfo.verifications[how.documentType = ‘passport’]

### Verifications modeling
Verifications specify what was verified and how it was verified (method). The what is the verifiable aspects: validity, authenticity, etc., and how it was verified.

Because different documents have different verifiable aspects, the document model needs to list what the verifiable aspects are. For example, a Passport's 'ownership' can be verified, but a MortgageLoanDetail form's cannot be.

There are a couple ways to model the limitations on choice of "what" and "how" for a specific document model. A Verifiable interface with the verifiableAspects property can be introduced, and the model implementing it can set the acceptable values. This is a little weird because typically resources have values for interface properties not models.

##### Verifiable interface

    {
    id: tradle.Verifiable,
    isInterface: true,
    properties: {
      verifiableAspects: {
        "type": "array"
      }
    }
    }

    Form model
        {
        id: tradle.Form,
        interfaces: [
          "tradle.Verifiable"
         ]
        }

##### Photo ID document model

    {
    id: tradle.PhotoID,
    interfaces: [
      "tradle.Verifiable"
    ],
    verifiableAspects: [
      authenticity: {
        methods: [
          tradle.VisualVerificationMethod,
          tradle.APIVerificationMethod
        ]
      },
      faceMatching: {
        methods: [
          tradle.VisualVerificationMethod
        ]
      },
      validity: {
        methods: [
          tradle.VisualVerificationMethod,
          tradle.ContactAuthorityVerificationMethod
        ]
      },
      age: {
        methods: [
          tradle.MicrosoftFaceAPI
        ]
      }
      gender: {
        methods: [
          tradle.MicrosoftFaceAPI
        ]
      }
    ],
    properties: {
    }
    }

The other way would be to have an enum of the valid values, e.g.

    {
    _t: 'tradle.VerificationAspectAndMethod',
    for: tradle.PhotoID,
    verifiableAspects: [
      authenticity: {
        methods: [
          tradle.VisualVerificationMethod,
          tradle.APIVerificationMethod
        ]
      },
      ownership: {
        methods: [
          tradle.VisualVerificationMethod
        ]
      },
      validity: {
        methods: [
          tradle.VisualVerificationMethod,
          tradle.ContactAuthorityVerificationMethod
        ]
      },
      cuteness: {
        methods: [
          tradle.VisualVerificationMethod
        ]
      }
    ]
    } 


A sample verification:

  `{
    _t: 'tradle.Verification',
    document: {
      ...
    },
    method: {
      _t: tradle.VisualVerificationMethod,
      documentPresence: 'selfie',
      ownerPresence: 'selfie' 
    },
    what: 'ownership'
  }`



misc:
  `additional verification methods:
    phone call
    site visit
    web search
    news archive
    court records`

===
Interface Verifiable {
   verifiableAspects: Array // what can be verified
   evidentiaryDocuments: Array of Document Types
}

Class PersonalInfo implements Verifiable {
   evidentiaryDocuments: [Passport, Visa, License, IDCard, ResidencePermit]
}

Class PhotoID implements Verifiable {
   verifiableAspects: {‘Athenticity’: {Algorithmic, InPerson}, ‘Facial similarity’: {Algorithmic, InPerson}, ‘Address validity’: {Visit, PostCard, UtilityBill} }
}

Class Verification {
   object: Verifiable;
   aspect: Enum; // one of the verifiableAspects
   method: 
}
Object Verification1 {
   aspect: ‘Athenticity’;
   method: {who verified, when verified, location where } // assuming this was an InPerson
}


Document scanning flow
Variant 1.
In case the server requests a specific document eg. Passport or Visa. 
User clicks on the Form Request like it is done today. 
If the form contains one editable property like ‘image’ then document scanner component is invoked presenting Camera View and returning a json object with al extracted fields from the document and image itself. App will prefill the Passport properties from the json object and will open the resource view to let user to preview and submit.

Variant 2.
Form request comes for the PhotoID
User clicks on it in chat 
Form displayed with those fields:
document type (passport, id card, driving license, visa, etc.) 
Country
Scan
Selfie
Customer enters document type and country, taps scan, camera control appears (this control can be powered by BlinkID or something else, worst case just a simple camera)
After camera control completes scanning, the same resource will appear with scanned image(s) and a block of fields that were extracted from the scanned document. This block of fields is a json object that is displayed as a group of properties.
Camera control appears again, this time for selfie property.
After the above step is completed, form can be submitted.

Notes: all of this is done as a normal form today plus several innovations
New property range is introduced, a property with the type Json. 
 “extractedFields”: {“type”: “object”, “ref”: “tradle.Json”}
Resource viewer today requires every property to be in the model, new viewer will just take whatever fields are in json and will display them.

This allows to hold extracted fields from the document image, e.g. passport number, date of issue, etc. By using json, we can relax the need to model upfront all properties that could be extracted. It allows us to avoid over-classifying documents into US Passport, UK Passport, Swiss Passport, UK Driver License, US Driver License, etc. etc.
New property range annotation, component. This will allow to experiment with different mobile document scanners, like BlinkID
“image”: {“type”: “object”, “ref”: “tradle.Photo”, “component”: “BlinkID”}
Later we could implement showing camera without needed user to tap on the scan and selfie properties
Later we will allow a form request from the server to come with the prefilled filed - e.g. documentType: Passport
This will allow a bank to ask for a specific document type, instead of letting user choose.z




















{
  "id": "tradle.PhotoID",
  "type": "tradle.Model",
  “subClassOf”: “tradle.Form”,
  "interfaces": [
    "tradle.Message"
  ],
  “properties”: {
     “documentType”: {
        "type": "object",
        "ref": “tradle.DocumentType”
     },
     “Country”: {
        "type": "object",
        "ref": “tradle.Country”
     },
     “scan”: {
        “type”: “array”,
        “range”: “photo”,
        “items”: {
           “ref”: “tradle.Photo”
        }
     },
     “selfie”: {
        “type”: “array”,
        “range”: “photo”,
        “items”: {
           “ref”: “tradle.Photo”
        }
     } 
  }
}


Questions
Onfido as a provider, temporarily UBS will sign Onfido’s verification, UBS charges more as at the top of the pyramide 
Ellen? Remediation - all data will be signed by UBS, on behalf of the customer?
Flattening verification sources
Inine and not inline, if it has a root hash, then it was chained
Versioning tracking for several resources not individually
Mark: Faker.js vs. Re-onboarding integration endpoint.
Double edit - aggregate verification needs update on any subordinate.
Automatic mode for issuing verifications can’t work anymore as it needs to first collect the onfido
Q. Onboarding. How does a bot know when it is finally ok to issue the aggregate verification?
A. PersonalInfo will have all the aspects that need to be verified. E.g. not on sanctions list, not pep, identity confirmed, tied to a person


