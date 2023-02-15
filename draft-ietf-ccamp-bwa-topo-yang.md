---
title: "A YANG Data Model for Bandwidth Availability Topo"
abbrev: "BWA Topo YANG Model"
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
This document defines a YANG data model to describe bandwidth availability for a link in a network topology.

--- middle

# Introduction

This document defines a YANG data model to describe bandwidth availability for a link.  It is an important characteristic of links with variable bandwidth, where each level of bandwidth can be associated with a certain level of availability.  An example of such a link is microwave radio link, where the bandwidth can be dynamically adapted to changing signal conditions, impacted by interference & fading, in order to guarantee the required quality of the link at every single moment.  {{?RFC8330}} defines a mechanism to report bandwidth-availability information through OSPF-TE, but it could also be useful for a controller to access such bandwidth-availability information as part of the topology model when performing a path/route computation.  The model augments "YANG Data Model for Traffic Engineering (TE) Topologies" defined in {{!RFC8795}}, which is based on "A YANG Data Model for Network Topologies" defined in {{!RFC8345}}.

The bandwidth availability model is expected to be used between a Provisioning Network Controller (PNC) and a Multi Domain Service Coordinator(MDSC) {{?RFC8453}}.  Examples of use cases that can be supported are:

1. Propagation of relevant characteristics of a link, including bandwidth availability, to higher topology layers, where it e.g. could be used as a criterion when configuring and optimizing a path for a connection/service through the network end to end.
2. A link could dynamically adjust its bandwidth according to changes in the signal conditions. {{?RFC8330}} defines a mechanism to report bandwidth-availability information through OSPF-TE, but it could also be useful for a controller to access such bandwidth-availability information as part of the topology model when performing a path/route computation.

## Terminology and Definitions
The following acronyms are used in this document:

PNC Provisioning Network Controller

MDSC Multi Domain Service Coordinator

## Tree Structure
A simplified graphical representation of the data model is used in chapter 3.1 of this document.  The meaning of the symbols in these diagrams is defined in {{?RFC8340}}.

# Requirements Language
The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in BCP 14 {{!RFC2119}} {{!RFC8174}} when, and only when, they appear in all capitals, as shown here.

# Bandwidth Availability Topology YANG Data Model

## YANG Tree
~~~~ yangtree
{::include ./trees/bw.tree}
~~~~
{: artwork-name="bw.tree"}

## Bandwidth Availability Topology YANG Data Module
~~~~ yang
{::include ./ietf-bandwidth-availability-topology.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-bandwidth-availability-topology.yang"}

# Security Considerations

   The YANG module specified in this document defines schemas for data
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

   The YANG module specified in this document imports and augments the
   ietf-network and ietf-network-topology models defined in {{!RFC8345}}.
   The security considerations from {{!RFC8345}} are applicable to the
   module in this document.

   There are a several data nodes defined in this YANG module that are
   writable/creatable/deletable (i.e., config true, which is the
   default).  These data nodes may be considered sensitive or vulnerable
   in some network environments.  Write operations (e.g., edit-config)
   to these data nodes without proper protection can have a negative
   effect on network operations.  These are the data nodes and their
   sensitivity/vulnerability:

   In the "ietf-bandwidth-availability-topology" module:

   - availability: A malicious client could attempt to modify the
      availability level which could modify the intended behavior.

   - link-bandwidth: A malicious client could attempt to modify the
      link bandwidth which could either provide more or less link
      bandwidth at the indicated availability level, changing the
      resource allocation in unintended ways.

# IANA Considerations

   IANA is asked to assign a new URI from the "IETF XML Registry"
   {{!RFC3688}} as follows:

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

# Examples of the application of the Bandwidth Availability Topology Model {#examples}

   This appendix provides some examples and illustrations of how the
   Bandwidth Availability Topology Model can be used.  There is one
   extended tree to illustrate the model and a JSON based instantiation
   for a small network example.

## A tree for a the Bandwidth Availability Topilogy Model

   The tree below shows the leafs for the Bandwidth Availability Model
   including the augmented Network Topology Model defined in
   {{!RFC8345}} and Traffic Engineering (TE) Topologies model defined
   in {{!RFC8795}}.

~~~~ yangtree
{::include ./trees/full-bw.tree}
~~~~
{: artwork-name="full-bw.tree"}

## A JSON example
~~~~ json
{::include ./json/exampleBwa.json}
~~~~
{: artwork-name="exampleBwa.json"}
{: sourcecode-markers="false" sourcecode-name="exampleBwa.json"}
