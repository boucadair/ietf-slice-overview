---
title: "An Overview of IETF Network Slicing Efforts"
abbrev: "IETF Network Slicing"
category: info

docname: draft-boucadair-teas-ietf-slicing-overview-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
workgroup: "Traffic Engineering Architecture and Signaling"
keyword:
 - slice specifications
 - slice coordination

author:
 -
    fullname: Mohamed Boucadair
    organization: Orange
    city: Rennes
    code: 35000
    country: France
    email: mohamed.boucadair@orange.com


normative:

informative:

--- abstract

This document lists a set of slicing-related specifications that are being development within the IETF. This document is meant to provide an overview of slicing activities in the IETF to hopefully ease coordination and ensure that specifications that are developed in many WGs are consistent.

--- middle

# Introduction

Various slicing efforts are being conduced within various IETF WGs (e.g., teas, idr, spring, ccamp, mpls, opsawg, 6man, and ippm) and areas (e.g., rtg, int, tsv, and ops). All these efforts are referring to the IETF framework that is developed by the teas WG ({{slice-fr}}), however there is a lack of a global visibility about these efforts and their interdependency.

Also, there is a lack of cross-WG communications in some cases when a slicing-related specification is candidate for adoption or adopted by a WG. This lack of global view at the IETF level and lack of early cross-WG communications may induce some inconsistency. For example, some proposals argue in favor of specifying extensions to convey specific identifiers in packets. However, distinct identifiers are being proposed: slice identifier, NRP Selector, NRP identifier, VTN identifier, VTN resource identifier, etc. The need and relationship between these identifiers are worth to be discussed independent of the channels that are used to convey these identifiers.

This document provides an overview of slicing activities in the IETF to hopefully ease coordination and ensure that specifications that are developed in many WGs are consistent, e.g.:

* Position the various concepts: network slice, network resource partition, virtual transport network, etc.
* Clarify the need of the various identifiers introduced so far and soften redundant/duplicate uses.
* Harmonize the definition of relevant identifiers (length, encoding, usage, etc.) rather than having the specification of the same identifier repeated in many places. For example, current specifications  use distinct encoding length of the same attribute (variable, 16-bit, 32-bit).
* Clarify the relationship and co-existence of identifiers if more than one is needed.

Future versions of this document many include recommendations.

# Reference Framework and Architecture {#slice-fr}

{{?I-D.ietf-teas-ietf-network-slices}} is the authoritative IETF framework for Network Slices. It provides definitions for a slice-related core terms and specifies a framework for the provision
of Network Slice services over networks that are deployed using technologies that are owned by the IETF (IP, MPLS, etc.). The document refers to such slices as IETF Network Slice.

{{?I-D.ietf-teas-ietf-network-slices}} provides a clear distinction between:

* the "IETF Network Slice service" which is the service delivered to the customer and which is agnostic to the technologies and mechanisms
   used by the service provider, and
* the "IETF Network Slice" which is the realization of the service in the service provider's network achieved by partitioning network resources and by applying a set of mechanisms within the network.

The IETF Network Slice service is specified in terms of:

* a set of Service Demarcation Point (SDP),
* a set of one or more connectivity constructs between subsets of these SDPs, and
*  a set of service objectives for each SDP sending to each connectivity construct.

The service objectives can be expressed as Service Level Objectives (SLOs) or Service Level Expectations (SLEs).

In some deploymenets, the underlying network can be customized to select a subset of resources that are suitable for the delivery of an IETF Network Slice service. Such a customization can be achieved by creating a set of Network Resource Partitions (NRPs).

In other deployments, IETF Network Slices can be hosted directly on the underlay network (i.e., without requiring any NRP).

IETF Network Slices can be realized using existing tools ({{no-extension}}). The extensions listed in {{cp-ext}} or {{dp-ext}} are not required in such a case.

{{?I-D.ietf-teas-ietf-network-slices}} does not provide any recommendation about the technological means to realize an IETF Network Slice service. These considerations are deployment specific.

# Models for Realizing Network Slices

## Using Current IP/MPLS Technologies {#no-extension}

{{?I-D.srld-teas-5g-slicing}} describes a model for the realization of IETF Network Slices for 5G networks. This realization model reuses many building blocks that are commonly used in service provider networks, specifically:

* L2VPN/L3VPN service instances for logical separation,
* Fine-grained resource control at the PE,
* Coarse resource control at the transit, and
* Capacity planning/management for efficient usage of provider network resources.

## Using Network Resource Partitions and Slice-Flow Aggregates {#flow-agg}

{{?I-D.ietf-teas-ns-ip-mpls}} proposes a model that is inspired from the Diffserv model for the realization of Network Slices over IP/MPLS networks. Specifically, this model introduces the concept of Slice-Flow Aggregate which is defined as a collection of packets that are mapped to an NRP and are given the same forwarding treatment in a shared network. An aggregate can group flows from of one or more IETF Network Slice services.

{{?I-D.ietf-teas-ns-ip-mpls}} also introduces the notion of NRP Policy that is used to trigger the creation of NRPs that will support a given Slice-Flow Aggregate. In some deployment schemes, packets that belong to a Slice-Flow Aggregate are forwarded by intermediate node along the appropriate NRP by processing an NRP Selector that is carried by these packets.

## Optical Transport Networks (OTN) Slicing

{{?I-D.ietf-ccamp-yang-otn-slicing}} defines Optical Transport Networks (OTN) slice as an OTN virtual network topology connecting a number of OTN endpoints using a set of shared or dedicated OTN network resources to satisfy specific SLOs. OTN slices are considered as a technology-specific realization of an IETF Network Slice in the OTN domain.

## VPN+

{{?I-D.ietf-teas-enhanced-vpn}} describes a framework for providing enhanced VPN services based upon VPN and Traffic Engineering (TE) technologies. Enhanced VPN (VPN+) can be used for the realization of IETF network slices. This document introduces the concept of Virtual Transport Network (VTN), which is a virtual underlay network consisting of a subset of network resources allocated from the physical underlay network, and is associated with a customized network topology.

## Instantiation in Service Providers Networks

{{?I-D.barguil-teas-network-slices-instantation}} focuses on the instantiation of the IETF Network Slice services in service provider networks using available data models. In particular, this document describes the relationship between service models for managing the IETF Network Slice services and Network Models (e.g., the Layer-3 Network Model (L3NPM, {{?RFC9182}}), the Layer-2 Network Model (L2NM {{?RFC9291}})) used for the realization of the slices.

## Structuring Network Slice Controllers

{{?I-D.contreras-teas-slice-controller-models}} proposes an approach for structuring the IETF Network Slice Controller as well as how to use different data models being defined for IETF Network Slice Service provision.

## SR-based Hierarchical Network Slices

{{?I-D.gong-teas-hierarchical-slice-solution}} proposes a hierarchical approach for realizing IETF Network Slices in Segment Routing domain. The approach involves two levels:

* Level 1 Network Slices are realized using Flex-Algo.
* Level 2 forwarding paths are restricted in the Level 1 topology by using SR Policy and NRP-ID in the data plane.

## Realization of Composite Network Slices

{{?I-D.li-teas-composite-network-slices}} investigates a set of scenarios for realizing composite IETF Network Slices (that basically involve other slices).  The document defines a new identifier, called Inter-Domain Network Resource Partition Identifier (Inter-domain NRP ID).

# Applicability and Mapping Scenarios

## 3GPP 5G End-to-End Network Slices

{{?I-D.ietf-teas-5g-network-slice-application}} focuses on the application of IETF Network Slices in the context of the 3GPP 5G slices.

## Abstraction and Control of Traffic Engineered Networks (ACTN)

{{?I-D.ietf-teas-applicability-actn-slicing}} describes the applicability of ACTN to Network Slicing.

## Mobility-Aware Transport Network Slicing

{{?I-D.ietf-dmm-tn-aware-mobility}} discusses a mapping of 5G slices to IETF Network Slices when the transport network is separated from the networks in which the 5G network functions are deployed (e.g., 5G functions distributed across data centers). This document zooms into the use of UDP source port number in GTP-U outer header and LAN to map between a 5G slice and corresponding IETF Network Slice segments that is listed in {{?I-D.ietf-teas-5g-network-slice-application}}.

## DetNet

{{?I-D.sw-detnet-network-slice-mapping-yang}} describes the applicability of DetNet to IETF Network Slice, particularly to provide deterministic services. The document describes how to use DetNet flow aggregation as the Slice-Flow Aggregates over an underlying NRP following the approach in {{flow-agg}}.


# Orchestration and Data Models

{{model-overview}} provides an example of the various data models that can be invoked in the context of Network Slicing.

~~~
                              +---------------+
                               |   Customer    |
                               +-------+-------+
               Customer Service Model  |
               e.g., slice-svc, ac-svc,| and bearer-svc
                               +-------+-------+
                               |    Service    |
                               | Orchestration |
                               +-------+-------+
                Network Model          |
  e.g., l2vpn-ntw, l3vpn-ntw, sap, and | ac-ntw
                               +-------+-------+
                               |   Network     |
                               | Orchestration |
                               +-------+-------+
         Network Configuration Model   |
                           +-----------+-----------+
                           |                       |
                  +--------+------+       +--------+------+
                  |    Domain     |       |     Domain    |
                  | Orchestration |       | Orchestration |
                  +---+-----------+       +--------+------+
       Device         |        |                   |
       Configuration  |        |                   |
       Model          |        |                   |
                 +----+----+   |                   |
                 | Config  |   |                   |
                 | Manager |   |                   |
                 +----+----+   |                   |
                      |        |                   |
                      | NETCONF/CLI..................
                      |        |                   |
                    +--------------------------------+
      +----+ Bearer |                                | Bearer +----+
      |CE#1+--------+            Network             +--------+CE#2|
      +----+   AC   |                                |   AC   +----+
                    +--------------------------------+
       Site A                                                  Site B
~~~
{: #model-overview title="Overview of Data Models used for Network Slicing" artwork-align="center"}

## Common Models

{{?RFC9181}} specifies a set of reusable types and groupings to manage VPN services. Note that VPNs are used for the realization of Network Slices.

{{?I-D.boro-opsawg-teas-common-ac}} specifies a set of reusable types and groupings to manage Attachment Circuits (ACs).

## Service Models

### Attachment Circuit as a Service (ACaaS) Data Model

{{?I-D.boro-opsawg-teas-attachment-circuit}} specifies YANG data models for managing 'Attachment Circuits'-as-a-Service (ACaaS) and also bearers. These ACs and bearers are used to identify where to deliver a slice service.

### Network Slice Service Data Model

{{?I-D.ietf-teas-ietf-network-slice-nbi-yang}} defines a YANG data model for manaing IETF Network Slice Services.

## Network Models

### Service Attachment Points (SAPs) {#sap}

{{?I-D.ietf-opsawg-sap}} defines a YANG data model for representing an abstract
   view of the provider network topology that contains the points from
   which its services can be attached (e.g., basic connectivity, VPN,
   network slices).  Also, the model can be used to retrieve the points
   where the services are actually being delivered to customers
   (including peer networks).

A SAP network topology can be used for one or multiple service types ('service-type'). Setting this data node to 'network-slice' allows a controller to expose where IETF Network Slices services are being delivered. It can also be used to check where IETF Network Slice services can be delivered.

### AC-augmented SAPs

{{?I-D.boro-opsawg-ntw-attachment-circuit}} augments the SAP model with more details for managing ACs at the network level.

### Network Slice Topology

{{?I-D.liu-teas-transport-network-slice-yang}} specifies a YANG model for IETF Network Slice Topology.

The need for such a model is yet to be justified as the current scope is redundant with what can be already achieved using the SAP model ({{sap}}).

### NRP

{{?I-D.wdbsp-teas-nrp-yang}} specifies a YANG data model for managing NRPs.

### Network Slice Mapping

{{?I-D.dhody-teas-ietf-network-slice-mapping}} specifies an IETF Network Slice Service mapping YANG model. The model supports the following mappings:

   *  L3NM {{?RFC9182}}
   *  L2NM {{?RFC9291}}
   *  TE {{?I-D.ietf-teas-te-service-mapping-yang}}
   *  NRP

# Control Plane Extensions {#cp-ext}

## NRP

### BGP Flowspec

{{?I-D.ietf-idr-flowspec-network-slice-ts}} specifies a BGP Flowspec extension for NRP traffic steering.

### BGP-LS Filters in SR

{{?I-D.drake-teas-bgp-ls-filter-nrp}} specifies new BGP-LS attributes, called BGP-LS Filters, for NRPs in SR networks. A BGP-LS Filter provides a description of a subset of the links and nodes in an underlay network. Ingress PE selects a path to an egress PE from the topology defined by the BGP-LS Filters it has imported for a given VPN.

### SR Policies Extensions

#### BGP

{{?I-D.dong-idr-sr-policy-nrp}} and {{?I-D.liu-idr-bgp-network-slicing}} define extensions to BGP in order to advertise NRP ID in an SR Policy. The NRP ID is encoded in 4 octets.

#### BGP-LS

{{?I-D.chen-idr-bgp-ls-sr-policy-nrp}} specifies SR Policy extensions for NRP in BGP-LS. The NRP ID is encoded in 4 octets.

### PCEP Extensions

{{?I-D.dong-pce-pcep-nrp}} specifie Path Computation Element Communication Protocol (PCEP) extensions for NRP. The NRP ID is encoded in 4 octets.

## Virtual Transport Networks (VTNs)

### IS-IS MT

{{?I-D.ietf-lsr-isis-sr-vtn-mt}} specifies how to use IS-IS Multi-Topology (MT) for SR-based VTNs.

### BGP-LS

{{?I-D.ietf-idr-bgpls-sr-vtn-mt}} describes a mechanism to distribute the information of SR-based VTNs to the  network controller using BGP-LS with Multi-Topology.

# Data Plane Extensions {#dp-ext}

## Slice Identifier in the MPLS Entropy Label

{{?I-D.decraene-mpls-slid-encoded-entropy-label-id}} proposes an approach to encode slice identifiers in a portion of the MPLS Entropy Label (EL). The number of bits to be used for encoding the slice identifier in the EL is policy-based. Transit LSRs uses the slice identifier in the EL to apply per-slice policies.

## Slice Identifier in IPv6 Flow Label

{{?I-D.filsfils-spring-srv6-stateless-slice-id}} proposes to encode slice identifers in a portion of the IPv6 Flow Label. Slice identifiers are used by intermediate IPv6 routers to process the packet according to
a network slice policy.

## Slice Identifier in the Source Address of Encapsulated SRH

When an ingress SR router encapsulates a packet in an IPv6 packet with an SRH, {{?I-D.cheng-spring-srv6-encoding-network-sliceid}} suggests to use the least significant bits of the outer IPv6 source address to encode a slide identifier. SLID Presence Indicator (SPI) is used to indicate the presence of a slice identifier. The number of bits used to encode slice identifiers is local to an SR domain.

## VTN Resource ID in an IPv6 Extension Header

{{?I-D.ietf-6man-enhanced-vpn-vtn-id}} describes a mechanism to carry an identifier, called VTN resource ID, in the IPv6 Hop-by-Hop extension header. The document claims that "VTN resource ID" is equivalent to NRP-ID, but does motivate why another yet ID is thus needed rather than using "NRP-ID".

The length of the VTN ID depends on the context type. When CT=0, the VTN ID is a 4-octet ID.

## NRP

### Resource-aware Segments

An NRP can be represented in SR networks using a set of NRP-specific resource-aware segments {{?I-D.ietf-spring-resource-aware-segments}}
{{?I-D.ietf-spring-sr-for-enhanced-vpn}}.

### NRP ID in SRv6

{{?I-D.liu-spring-nrp-id-in-srv6-segment}} specifies an approach to encode the NRP ID in the SRH. This ID is used by intermediate IPv6 routers to identify the NRP to be used for forwarding. The encoding of the NRP ID in an IPv6 address is variable; an instruction is thus needed to help identifyint the NRP-ID position (e.g., low 16 bits).

### NRP Selector in MPLS Network Actions

As mentioned in {{flow-agg}}, packets that are associated with a Slice-Flow Aggregate may carry an NRP Selector (NRPS). This selector is intended to be conveyed in the packet's network layer header to identify the flow aggregate to which a packet belongs. {{?I-D.li-mpls-mna-nrp-selector}} investigates a set of options to use MPLS Network Actions (MNA) to carry the NRPS:

* 13-bit NRP Selector (NRPS13) Action
* 20-bit NRP Selector (NRPS20) Action
* 20-bit Entropy and NRP Selector (ENRPS20) Action

# OAM

## LSP Ping/Traceroute Extensions

{{?I-D.liu-mpls-lsp-ping-nrp}} specifies extenstions to the LSP Ping/Traceroute to convey NRP-ID in SR domains.

The NRP-ID is a encoded as a 4-octet field.

## Precision Availability Metrics for SLO-Governed End-to-End Services

{{?I-D.ietf-ippm-pam}} introduces a new set of metrics, called Precision Availability Metrics (PAM). These metrics are used to assess whether a service (e.g., Network Slice service) is provided in compliance with its
specified SLOs.

# Misc

## Scalability Considerations for NRP

{{?I-D.ietf-teas-nrp-scalability}} discusses a set of scenarios for the deployment of NRP with a focus on scalability implications. The document reasons about the increase of requested IETF Network Slice services that would require NRPs. Such an increase of slices is speculative at this stage.

# Security Considerations

Security considerations of the mechanisms listed in the document are discussed in the relevant documents that specify these mechanisms.

# IANA Considerations {#IANA}

This document does not make any request to IANA.

--- back

# Acknowledgments
{:numbered="false"}

Thanks to TBC.
