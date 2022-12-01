---
title: "A YANG Data Model for Bandwidth Availability"
abbrev: "Bandwidth Availability YANG Model"
docname: draft-ietf-ccamp-bwa-topo-yang-latest
category: std
ipr: trust200902
area: Routing
workgroup: ccamp
keyword: Internet-Draft
stand_alone: yes
pi: [toc, sortrefs, symrefs]
consensus: true

author:
 -
   ins: J. Ahlberg
   name: Jonas Ahlberg
   organization: Ericsson
   email: jonas.ahlberg@ericsson.com
 -
   ins: S. Mansfield
   name: Scott Mansfield
   organization: Ericsson
   email: scott.mansfield@ericsson.com
 -
   ins: M. Ye
   name: Min Ye
   organization: Huawei Technologies
   email: amy.yemin@huawei.com
 -
   ins: I. Busi
   name: Italo Busi
   organization: Huawei Technologies
   email: italo.busi@huawei.com
 -
   ins: X. Li
   name: Xi Li
   organization: NEC Laboratories Europe
   email: xi.li@neclab.eu
 -
   ins: D. Spreafico
   name: Daniela Spreafico
   organization: Nokia - IT
   email: daniela.spreafico@nokia.com

normative:

informative:

--- abstract
This document defines the YANG data model for bandwidth availability for a link.

--- middle

# Introduction

This document defines a YANG data model for bandwidth bandwidth availability for a link.  It is an important characteristic of a microwave radio link, but it could also be applicable for other types of links. The model augments "YANG Data Model for Traffic Engineering (TE) Topologies" defined in {{!RFC8795}}, which is based on "A YANG Data Model for Network Topologies" defined in {{!RFC8345}}.

## Terminology and Definitions
The following acronyms are used in this document:

PNC Provisioning Network Controller

MDSC Multi Domain Service Coordinator

## Tree Structure
A simplified graphical representation of the data models is used in chapters 3.1, 4.1, and 5.1 of this document.  The meaning of the symbols in these diagrams is defined in {{?RFC8340}}.

# Requirements Language
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all capitals, as shown here.

## Model applicability to other technology
TBD

#Bandwidth Availability Topology YANG Data Model

## YANG Tree
~~~~ yangtree
{::include ./bw.tree}
~~~~
{: artwork-name="bw.tree"}

## Bandwidth Availability Topology YANG Data Module
~~~~ yang
{::include ./ietf-bandwidth-availability-topology.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-bandwidth-availability-topology.yang"}

## Applicability of the Data Model for Traffic Engineering (TE) Topologies
Since microwave is a point-to-point radio technology providing connectivity on L0/L1 over a radio link between two termination points and cannot be used to perform cross-connection or switching of the traffic to create network connectivity across multiple microwave radio links, a majority of the leafs in the Data Model for Traffic Engineering (TE) Topologies augmented by the microwave topology model are not applicable.

More specifically, admin-status and oper-status are recommended to be reported for links only.  Status for termination points can be used when links are inter-domain and when the status of only one side of link is known, but since microwave is a point-to-point technology where both ends normally belong to the same domain it is not expected to be applicable in normal cases.  Furthermore, admin-status is not applicable for microwave radio links.  Enable and disable of a radio link is instead done in the constituent carriers.

# Security Considerations

   The YANG modules specified in this document define schemas for data
   that is designed to be accessed via network management protocols such
   as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}.  The lowest NETCONF layer
   is the secure transport layer, and the mandatory-to-implement secure
   transport is Secure Shell (SSH) {{!RFC6242}}.  The lowest RESTCONF layer
   is HTTPS, and the mandatory-to-implement secure transport is TLS
   {{!RFC8446}}.

   The NETCONF access control model {{!RFC8341}} provides the means to
   restrict access for particular NETCONF or RESTCONF users to a
   preconfigured subset of all available NETCONF or RESTCONF protocol
   operations and content.

   The YANG modules specified in this document import and augment the
   ietf-network and ietf-network-topology models defined in {{!RFC8345}}.
   The security considerations from {{!RFC8345}} are applicable to the
   modules in this document.

   There are a several data nodes defined in these YANG modules that are
   writable/creatable/deletable (i.e., config true, which is the
   default).  These data nodes may be considered sensitive or vulnerable
   in some network environments.  Write operations (e.g., edit-config)
   to these data nodes without proper protection can have a negative
   effect on network operations.  These are the subtrees and data nodes
   and their sensitivity/vulnerability:

   In the "ietf-bandwidth-availability-topology" module:

   -  availability: A malicious client could attempt to modify the
      availability level which could modify the intended behavior.

   -  link-bandwidth: A malicious client could attempt to modify the
      link bandwidth which could either provide more or less link
      bandwidth at the indicated availability level, changing the
      resource allocation in unintended ways.

# IANA Considerations

   IANA is asked to assign a new URI from the "IETF XML Registry" {{!RFC3688}} as follows:

~~~~
URI: urn:ietf:params:xml:ns:yang:ietf-bandwidth-availability-topology
Registrant Contact: The IESG
XML: N/A; the requested URI is an XML namespace.
~~~~

   It is proposed that IANA should record YANG module names in the "YANG
   Module Names" registry {{!RFC6020}} as follows:

~~~~
    Name: ietf-bandwidth-availability-topology
    Maintained by IANA?: N
    Namespace:
    urn:ietf:params:xml:ns:yang:ietf-bandwidth-availability-topology
    Prefix: bwavtopo
    Reference: RFC XXXX
~~~~

--- back

