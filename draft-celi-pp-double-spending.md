---
title: Double Spending in Privacy Pass
abbrev: TODO - Abbreviation
docname: draft-celi-pp-double-spending-latest
category: info

ipr: trust200902
area: General
keyword: Internet-Draft

stand_alone: yes
pi: [toc, sortrefs, symrefs]

author:
 -  ins: S. Celi
    name: Sofía Celi
    org: Cloudflare
    city: Lisbon
    country: Portugal
    email: cherenkov@riseup.net
 -
    ins: A. Davidson
    name: Alex Davidson
    city: Lisbon
    country: Portugal
    email: alex.davidson92@gmail.com

normative:
  RFC2119:
  RFC8446:
  draft-davidson-pp-protocol:
    title: "Privacy Pass: The Protocol"
    target: https://tools.ietf.org/html/draft-davidson-pp-protocol-00
    author:
      ins: A. Davidson
      org: Cloudflare Portugal

informative:



--- abstract

Privacy Pass is a protocol that aims to provide an anonymity-preserving
mechanism for authorization of clients with servers. The protocol is
detailed in {{?I-D.ietf-privacypass-protocol}} and is intended for use in
the application-layer.

Privacy Pass requires a protection against double-spending: a mechanism
for checking that tokens sent by clients have not been spent before.
All issuing servers should implement this robust storage-query mechanism.

This document specifies the needs and protection that such mechanism should
have, and the attacks that can be exercised upon in.

--- middle

# Introduction

Note that this draft has not received significant security review and should
not be the basis for production systems.

Needs:

* Tokens need to be checked for each server individually.
* All servers must perform global double-spend checks to avoid clients from
  exploiting the possibility of spending tokens more than once against
  distributed token checking systems
* The storage needs to have a quick update time. While an update is occurring
  it may be possible for a malicious client to spend a token more than once.
* The storage should be parameterized to live as long as the server keypair
  that is in use.

Attacks:

* There could be double-spending during the update
* A malicious redeemer could induce the double-spending storage to store large
  numbers of tokens, possibly causing denial-of-service due to consuming
  storage space.
* An attacker can compromise the double-spending storage and remove used
  tokens, so token can be re-accepted at a later time.

# Conventions and Definitions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this
document are to be interpreted as described in BCP 14 {{RFC2119}} {{!RFC8174}}
when, and only when, they appear in all capitals, as shown here.


# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.



--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
