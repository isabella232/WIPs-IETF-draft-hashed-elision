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
    GordianEnvelope: I-D.mcnally-envelope
    BCSwiftDCBOR:
        author:
            name: Wolf McNally
        title: "Deterministic CBOR (dCBOR) for Swift."
        target: https://github.com/BlockchainCommons/BCSwiftDCBOR

--- abstract

This document discusses the privacy and human rights benefits of data minimization via the methodology of hashed data elision and how it can help protocols to fulfill the guidelines of RFC 6973: Privacy Considerations for Internet Protocols and RFC 8280: Research into Human Rights Protocol Considerations. Additional details discuss how the extant Gordian Envelope draft can provide additional benefits in these categories.

--- middle

# Introduction

Current IETF guidelines for privacy and human rights considerations {{RFC6973}} in internet protocols lack the specificity needed for practical implementation, leading to privacy threats such as correlation, secondary use, and unnecessary disclosure of data.

IETF released guidelines for privacy considerations in 2013 with RFC 6973 and then expanded upon that with human-rights considerations in 2017 with RFC 8280. Both RFCs provide thoughtful ideas for how privacy can be improved in internet protocols, and how that can support human rights on the internet.

However, as generalized guidelines the RFCs don’t provide the specifics that might be required to incorporate these guidelines into new protocols. This document suggests more specific areas of work based in part on the Data Minimization suggestions of §6.1 of RFC 6973, and expands them to also support some of the Human Rights Guidelines outlined in §6.2 of RFC 8280.

## Conventions and Definitions

{::boilerplate bcp14-tagged}

# Problem Statement

Forthcoming.

# Security Considerations

Forthcoming.

# IANA Considerations

Forthcoming.

--- back

# Acknowledgments
{:numbered="false"}

Forthcoming.
