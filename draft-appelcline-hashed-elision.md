---
v: 3

title: "Hashed Data Elision: Problem Statement and Areas of Work"
abbrev: "HashedElision"
docname: draft-appelcline-hashed-elision-latest
category: info
stream: IETF

ipr: trust200902
area: Applications and Real-Time
workgroup: Network Working Group
keyword: Internet-Draft

pi: [toc, sortrefs, symrefs]

venue:
  github: BlockchainCommons/WIPs-IETF-draft-hashed-elision

author:
 -
    name: Shannon Appelcline
    organization: Blockchain Commons
    email: shannon.appelcline@gmail.com
 -
    name: Wolf McNally
    organization: Blockchain Commons
    email: wolf@wolfmcnally.com
 -
    name: Christopher Allen
    organization: Blockchain Commons
    email: christophera@lifewithalacrity.com

normative:

informative:
    RFC6973: Privacy
    RFC8280: Human Rights
    GordianEnvelope: I-D.mcnally-envelope

--- abstract

This document discusses the privacy and human rights benefits of data minimization via the methodology of hashed data elision and how it can help protocols to fulfill the guidelines of RFC 6973: Privacy Considerations for Internet Protocols and RFC 8280: Research into Human Rights Protocol Considerations. Additional details discuss how the extant Gordian Envelope draft can provide further benefits in these categories.

--- middle

# Introduction

IETF released guidelines for privacy considerations in 2013 with {{RFC6973}} and then expanded upon that with human-rights considerations in 2017 with {{RFC8280}}. Both RFCs provide thoughtful ideas for how privacy can be improved in internet protocols, and how that can support human rights on the internet.

However, as generalized guidelines these RFCs don’t provide the specifics that might be required to incorporate these guidelines into new protocols. This leads to privacy threats such as correlation, secondary use, and unnecessary disclosure of data. This document suggests more specific areas of work based in part on the Data Minimization suggestions of §6.1 of RFC 6973, and expands them to also support some of the Human Rights Guidelines outlined in §6.2 of RFC 8280. It does so through the advancement of a hashed data elision methodology, which allows for the optional removal of data while maintaining hashes of that data to ensure data integrity.

# Problem Statement

## Correlation, Secondary Use, and Disclosure All Threaten Privacy

Digital data transmission often operates on an all-or-nothing basis: sharing data means full disclosure. There is no standard methodology for minimizing data nor for eliding parts of a data packet. This can threaten privacy in multiple ways:

- Correlation can combine data from different sources, unintentionally revealing comprehensive individual data, significantly more than was intended. This is highlighted as a problem in §5.2.1 of RFC 6973.
- Secondary Use permits data acquirers to repurpose it beyond its original intent. This is highlighted as a problem in §5.2.3 of RFC 6973.
- Disclosure of any sort can reveal more data than was required for a use, and that extra data can then create prejudice or otherwise disadvantage the individual whose data has been disclosed. This is highlighted as a problem in §5.2.4 of RFC 6973.

Methodologies for minimizing the amount of data shared at any one time can reduce all of these privacy dangers.

## Data Minimization through Anonymity or Pseudonymity is Insufficient

§6.1 of RFC 6973 lists anonymity and pseudonymity as two methodologies for creating data minimization. This means removing uniquely identifying data and/or reducing the amount of personal data that is transmitted.

Though anonymity and pseudonymity are minimal requirements for improving the privacy of digital data, they are insufficient. To best address privacy requires reducing the amount of all data found in any disclosure to the bare minimum required for a specific disclosure.

## Simplistic Data Minimization Can Hinder Other Humans Rights Solutions

Simplistic data minimization focuses on cutting out unnecessary content that is not required for a specific task. Though minimization is a general requirement to improve privacy through data minimization, doing so in a simplistic manner is not sufficient.

This is because simplistic data minimization excises everything about data, which can cause problems for the Integrity and potentially the Authenticity of the original data set. These are needed per the Guidelines for Human Rights, as outlined in §6.2.16 and §6.2.17 of RFC 8280.

A better solution for data minimization is required that does not ignore other Human Rights needs as it improves privacy. Hashed data elision can provide such a solution.

## Any Data Can Be Too Much Data

A more nuanced data minimization system can solve many problems. However, there are also situations where a party doesn’t need to know any specific data, but instead requires proof that a general data precept is true. The traditional example is proof whether someone is 21 or older, for buying alcohol in the United States. With data minimization, the person's precise age would still be provided, even though all that's actually needed is an affirmation that the person was born more than 21 years ago.

In these cases, privacy threats can be reduced even more by providing no data, simply the proof that a general precept is true. This can offer very strong protection against Correlation (§5.2.1 of RFC 6973) and obviously minimizes Disclosure (§5.2.4 of RFC 6973).

Though some systems such as BBS+ Signatures and other Zero Knowledge Proofs system can support superior anti-correlation with “proof of knowledge of the undisclosed signature”, a more simple salted hashed data elision often can provide easier solutions for many classes of “inclusion” proofs.

# Areas of Work

## Core Areas of Work

This section tries to identify and structure areas of work to address the aforementioned topics by turning the guidelines of RFC 6973 and RFC 8280 into more precise specifications or requirements. It focuses on hashed data elision as a core area of work, but in a section on optional areas of work discusses other advancements that can further support RFC 6973 and especially RFC 8280.

### Support Data Minimization

As suggested by RFC 6973, Data Minimization is a prime methodology for improving privacy and reducing problems such as Correlation, Secondary Use, and Disclosure.

To fully support Data Minimization, a specification MUST:

1. Allow for the elision of some content from a larger package of data.
2. Allow for the holder of that data to do that elision, rather than restricting it to only issuers.

Elision is the obvious requirement for data minimization: it's the removal of data. The question of who can elide data becomes more important when data is signed as an authentication means, such as for credentials of various sorts. In these situations, elision is often restricted to the issuer of the credential, which effectively denies the holder from doing so. To support data minimization requires the holder to be able to do so as well, while maintaining any signatures.

### Incorporate Deterministic Hashing

As noted in §2.3, above, simplistic Data Minimization can cause other human rights problems such as a lack of Authenticity or Integrity checking. This can be resolved in a specification by requiring a fingerprint that can be used to verify elided data. It MUST:

1. Allow elided data to be verified with a fingerprint. 
2. Ensure that the fingerprint is unidirectional, so that the fingerprint can prove the existence of the data, but the data cannot be derived from the fingerprint.
3. Maintain the validity of authenticity checks such as signatures through the fingerprint.

A fingerprint that is generated through a hash function such as SHA-256 or a newer function such as BLAKE3 will generally meet the first two requirement.

The third requirement is designed to support the requirements for Data Minimization in §3.1.1, above. If data is hashed, but any signature is applied to the hash rather than the original data, then a holder can choose to elide the data or not, as they see fit, but the signature still remains valid. 

### Enable Inclusion Proofs

Because data does not always need to be shared to provide the verification required by a validator, support of data proofs can provide additional privacy and human rights benefits. To support this, a specification MUST:

1. Allow for the revelation of specific fingerprints.
2. Support the easy creation of an inclusion proof that demonstrate how specific data can be hashed to create that specific fingerprint.
3. Enable any holder to create that inclusion proof, not just an issuer.

Through this methodology, a holder can create a proof for a specific bit of data, such as their residence in a specific country or state, demonstrate that proof’s creation, and show that it matches the hash of elided data. However, the holder does so only if and when they wish: the data is never known unless they do so.

Though other methodologies exist for proving the content of data, such as Zero-Knowledge Proofs and BBS+ Signatures, inclusion proofs based on hashes provide a much easier solution that is pragmatically more likely to be implemented and thus is more accessible and useable today.

### Facilitate Herd Privacy

Support for inclusion proofs can also allow for the use of herd privacy, where data about a specific user is contained within a much larger hash of data, which can be widely published without danger. This puts all the agency for data revelation in an individual user’s hand, and does it without any need to “phone home”, meaning that not even the original publisher of the data would know when that data were being checked.

To ensure that inclusion proofs can be extended to herd privacy, a specification MUST:

1. Use a branching structure for data storage such as a Merkle Tree where hashes can be further hashed together at high levels in a well-known, regularized way.
2. Allow for the publication of top-level or high-level hashes.
3. Enable individual holders to reveal paths that connect their individual data up to the top-level or high-level hash through any number of branches.
4. Build that structure in such a way that a minimum of other hashes are revealed when a user reveals a path to their own data; or else ensure that any other hashes revealed are worthless without knowledge of secret data, such as a salt.
5. Otherwise support the creation of inclusion proofs for proving their low-level individual data.

Ensuring herd privacy in part focuses upon empowering the user, but it also depends on a thoughtful creation of the hash tree structure, such that other information can’t be guessed from the revelation of hashes.

## Optional Areas of Work

Using hashed data elision as a foundation would improve the privacy of almost any IETF protocol.

The Gordian Envelope Internet-Draft {{GordianEnvelope}} is one example of a specification that supports hashed data elision. It could be used to enable all of the Core Areas of Work. It also goes further, incorporating additional functionality that can provide better support for RFC 6973 and RFC 8280 through additional features, including the following.

### Extend Support to Encryption & Compression

A hashed data elision system can be expanded to support both encryption and compression functions, as encrypted and compressed data can also be represented by their hashes without revealing any information about the original data.

Incorporating encryption into a data specification offers the highest level of privacy and of data minimization possible, as data can only be viewed by select individual with the decryption key. This is especially important for Confidentiality, which is referenced in §6.2.15 of RFC 8280.

Hashing encryption primarily improves Authenticity, per §6.2.17 of RFC 8280. As with other sorts of elided data, signatures will remain valid even following compression, provided the signatures are applied to the data hash, not the original data.

### Address Additional Human Rights Threats

As currently imagined, the Gordian Envelope Internet Draft also offers support for several other Guidelines for Human Rights Considerations that are listed in §6.2 of RFC 8280:

- Privacy (§6.2.2). Besides the obvious privacy benefits of data minimization, Gordian Envelope also improves privacy through optional usage of metadata, which can be used to document the sensitivity of contents, retention limits, etc.
- Accessibility (§6.2.11). Metadata can also be used to ensure accessibility and internationalization of data through inclusions of references with a variety of localizations.
- Censorship Resistance (§6.2.6). Gordian Envelope is built to support SCIDs, or self-certifying identifiers, which can be used to avoid reuse of existing identifiers that might be associated with persons or content.
- Open Standards (§6.2.7). As an Internet Draft, Gordian Envelope represents an open standard. It can support interoperable exchange of data, which is vital for human rights.
- Heterogeneity Support (§6.2.8), Adaptability (§6.2.18). Gordian Envelope builds its data format on triples: assertions of subjects, predicates, and objects. This format can easily be adapted to a wide variety of data formatting styles.
- Localization (§6.2.12), Decentralization (§6.2.13). As an open standard that solely utilizes other open standards such as well-known hashing and encryption algorithms, Gordian Envelope is built to avoid decentralization. This is further supported by Gordian Envelope’s Heterogeneity Support, its Adaptability, and its Reliability.
- Reliability (§6.2.14), Integrity (§6.2.16). Gordian Envelope is built on CBOR, which means that data is self-describing. It is also hashed. This improves its Reliability and Integrity, while the self-description also makes data stored in Gordian Envelope more interoperable, and thus less subject to centralization.

### Keep It Simple

Support for privacy and for human rights has another requirement: it needs to be kept simple so that it finds actual use.

Gordian Envelope {{GordianEnvelope}} is a fundamentally simple data format that only achieves complexity through iterative structure design.

# Privacy Considerations

As outlined, the concept of hashed data elision and, more specifically the Gordian Envelope specification, provide a wide variety of privacy advancements.

The biggest remaining privacy concern is of accidental correlation that can arise if different parties have different versions of the same data, which has been elided in different ways. This is currently seen as an acceptable side-effect of an elision system that allows for Authenticity and Integrity in the system, and can be offset by careful creation of Envelope structures, such as gathering small groups of data into distinct, elided branches.

However, the question also remains open as to whether there might be more expansive and more automated solutions.

# Security Considerations

Hashed data elision itself is intended to strengthen communication security, primarily by enhancing confidentiality (through elision) while also maintaining data integrity (through hashing). Supporting it with a signature system, as Gordian Envelope does, also allows for peer entity authentication, creating a strong foundation for overall communication security.

However, that security depends onthe strength of hashing algorithms (and encryption/signature algorithms if they’re used). Strong, unbroken hashes are required. Potential threats to hashes and encryption such as quantum computing would also result in threats to any hashed data elision system.

# IANA Considerations

This document has no IANA actions. Gordian Envelope has already been assigned CBOR tag #200 by IANA.

--- back

# Acknowledgments

The authors are grateful for the support of the CBOR working group in discussions of Gordian Envelope and general guidance within the IETF.
