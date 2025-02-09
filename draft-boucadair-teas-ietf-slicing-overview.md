---
title: "An Overview of Network Slicing Efforts in The IETF"
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

# Reference Framework and Architecture {#slice-fr}

{{?RFC9543}} is the authoritative IETF framework for Network Slices. It provides definitions for a slice-related core terms and specifies a framework for the provision
of Network Slice Services over networks that are deployed using technologies that are owned by the IETF (IP, MPLS, etc.). The document refers to such slices as IETF Network Slice or "the term "RFC 9543 Network Slice".

{{?RFC9543}} provides a clear distinction between:

* the "RFC 9543 Network Slice Service" which is the service delivered to the customer and which is agnostic to the technologies and mechanisms
   used by the service provider, and
* the "RFC 9543 Network Slice" which is the realization of the service in the service provider's network achieved by partitioning network resources and by applying a set of mechanisms within the network.

The RFC 9543 Network Slice Service is specified in terms of:

* a set of Service Demarcation Point (SDP),
* a set of one or more connectivity constructs between subsets of these SDPs, and
* a set of service objectives for each SDP sending to each connectivity construct.

The service objectives can be expressed as Service Level Objectives (SLOs) or Service Level Expectations (SLEs).

In some deploymenets, the underlying network can be customized to select a subset of resources that are suitable for the delivery of an RFC 9543 Network Slice Service. Such a customization can be achieved by creating a set of Network Resource Partitions (NRPs).

In other deployments, RFC 9543 Network Slices can be hosted directly on the underlay network (i.e., without requiring any NRP).

RFC 9543 Network Slices can be realized using existing tools ({{no-extension}}). The extensions listed in {{cp-ext}} or {{dp-ext}} are not required in such a case.

{{?RFC9543}} does not provide any recommendation about the technological means to realize an RFC 9543 Network Slice Service. These considerations are deployment specific.

# Models for Realizing Network Slices

## Using Current IP/MPLS Technologies {#no-extension}

{{?I-D.ietf-teas-5g-ns-ip-mpls}} describes a model for the realization of RFC 9543 Network Slices for 5G networks. This realization model reuses many building blocks that are commonly used in service provider networks, specifically:

* L2VPN/L3VPN service instances for logical separation,
* Fine-grained resource control at the PE,
* Coarse resource control at the transit, and
* Capacity planning/management for efficient usage of provider network resources.

## Using Network Resource Partitions (NRPs) and Slice-Flow Aggregates {#flow-agg}

{{?I-D.ietf-teas-ns-ip-mpls}} proposes a model that is inspired from the Diffserv model for the realization of Network Slices over IP/MPLS networks. Specifically, this model introduces the concept of Slice-Flow Aggregate which is defined as a collection of packets that are mapped to an NRP and are given the same forwarding treatment in a shared network. An aggregate can group flows from of one or more RFC 9543 Network Slice Services.

{{?I-D.ietf-teas-ns-ip-mpls}} also introduces the notion of NRP Policy that is used to trigger the creation of NRPs that will support a given Slice-Flow Aggregate. In some deployment schemes, packets that belong to a Slice-Flow Aggregate are forwarded by intermediate node along the appropriate NRP by processing an NRP Selector that is carried by these packets.

## Optical Transport Networks (OTN) Slicing

{{?I-D.ietf-ccamp-yang-otn-slicing}} defines Optical Transport Networks (OTN) slice as an OTN virtual network topology connecting a number of OTN endpoints using a set of shared or dedicated OTN network resources to satisfy specific SLOs. OTN slices are considered as a technology-specific realization of an RFC 9543 Network Slice in the OTN domain.

## VPN+

{{?I-D.ietf-teas-enhanced-vpn}} describes a framework for providing enhanced VPN services based upon VPN and Traffic Engineering (TE) technologies. Enhanced VPN (VPN+) can be used for the realization of Network Slices. This document introduces the concept of Virtual Transport Network (VTN), which is a virtual underlay network consisting of a subset of network resources allocated from the physical underlay network, and is associated with a customized network topology.

## Instantiation in Service Providers Networks

{{?I-D.ietf-teas-ns-models-applicability}} focuses on the instantiation of the RFC 9543 Network Slice Services in service provider networks using existing data models. In particular, this document describes the relationship between service models for managing the RFC 9543 Network Slice Services and network models (e.g., the Layer-3 Network Model (L3NPM, {{?RFC9182}}), the Layer-2 Network Model (L2NM {{?RFC9291}})) used for the realization of the slices.

## Structuring Network Slice Controllers

{{?I-D.ietf-teas-ns-controller-models}} proposes an approach for structuring the RFC 9543 Network Slice Controller as well as how to use different data models being defined for RFC 9543 Network Slice Service provision.

## SR-based Hierarchical Network Slices

{{?I-D.gong-spring-hierarchical-slice-solution}} proposes a hierarchical approach for realizing RFC 9543 Network Slices in Segment Routing domain. The approach involves two levels:

* Level 1 Network Slices are realized using Flex-Algo.
* Level 2 forwarding paths are restricted in the Level 1 topology by using SR Policy and NRP-ID in the data plane.

## Realization of Composite Network Slices

{{?I-D.li-teas-composite-network-slices}} investigates a set of scenarios for realizing composite RFC 9543 Network Slices (that basically involve other slices).  The document defines a new identifier, called Inter-domain NRP ID.

## AAA for Hierarchical Network Slices

{{?I-D.zhang-rtgwg-aaa-hierarchical-network-slices}} describes an authentication, authorization, and accounting process for hierarchical Network Slices. The document
suggest adding NRP-ID to accounting meesages, but lacks a discussion whether any protocol extension is needed.

# Applicability and Mapping Scenarios

## 3GPP 5G End-to-End Network Slices

{{?I-D.ietf-teas-5g-network-slice-application}} focuses on the application of RFC 9543 Network Slices in the context of the 3GPP 5G slices.

## Enforcement of 5G End-to-End Network Slice QoS

{{?I-D.cbs-teas-5qi-to-dscp-mapping}} documents an example of possible mapping of 5QI values
to DSCP markings with a focus on 5G Network Slices. The document groups different 5QI types in classes based
on their SLOs.

## Encoding 3GPP Slices for Interactive Media Services

{{?I-D.jiang-tsvwg-slice-media-service}} explores how IETF schemes (DSCP and UDP options) can be used to expose some QoS-related metadata for specific flows to 5GS. The document focuses on the Extended Reality & multi-modality communication (XRM) service.

## Abstraction and Control of Traffic Engineered Networks (ACTN)

{{?I-D.ietf-teas-applicability-actn-slicing}} describes the applicability of ACTN to Network Slicing.

## Mobility-Aware Transport Network Slicing

{{?I-D.ietf-dmm-tn-aware-mobility}} discusses a mapping of 5G slices to RFC 9543 Network Slices when the transport network is separated from the networks in which the 5G network functions are deployed (e.g., 5G functions distributed across data centers). This document zooms into the use of UDP source port number in GTP-U outer header and LAN to map between a 5G slice and corresponding RFC 9543 Network Slice segments that is listed in {{?I-D.ietf-teas-5g-network-slice-application}}.

The document specifies an ACaaS extension {{?I-D.ietf-opsawg-teas-attachment-circuit}} to support a layer 3 GTP-U (or UDP encapsulated GTP) bearer as an attachment circuit.

## DetNet

{{?I-D.sw-detnet-network-slice-mapping-yang}} describes the applicability of DetNet to RFC 9543 Network Slice, particularly to provide deterministic services. The document describes how to use DetNet flow aggregation as the Slice-Flow Aggregates over an underlying NRP following the approach in {{flow-agg}}.


# Orchestration and Data Models

{{model-overview}} provides an example of the various data models that can be invoked in the context of Network Slicing.

~~~ aasvg
                                .-------------.
                               |   Customer    |
                                '------+------'
               Customer Service Model  |
               e.g., slice-svc, ac-svc,| and bearer-svc
                                .------+------.
                               |    Service    |
                               | Orchestration |
                                '------+------'
                Network Model          |
  e.g., l2vpn-ntw, l3vpn-ntw, sap, and | ac-ntw
                                .------+------.
                               |   Network     |
                               | Orchestration |
                                '------+------'
         Network Configuration Model   |
                           .-----------+-----------.
                           |                       |
                   .-------+-----.         .-------+-----.
                  |    Domain     |       |     Domain    |
                  | Orchestration |       | Orchestration |
                   '--+----------'         '-------+-----'
       Device         |        |                   |
       Configuration  |        |                   |
       Model          |        |                   |
                  .---+---.    |                   |
                 | Config  |   |                   |
                 | Manager |   |                   |
                  '---+---'    |                   |
                      |        |                   |
                      NETCONF/CLI..................
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

{{?I-D.ietf-opsawg-teas-common-ac}} specifies a set of reusable types and groupings to manage Attachment Circuits (ACs).

## Service Models

### Attachment Circuit as a Service (ACaaS) Data Model

{{?I-D.ietf-opsawg-teas-attachment-circuit}} specifies YANG data models for managing 'Attachment Circuits'-as-a-Service (ACaaS) and also bearers. These ACs and bearers are used to identify where to deliver a slice service.

### Network Slice Service Data Model

{{?I-D.ietf-teas-ietf-network-slice-nbi-yang}} defines a YANG data model for manaing RFC 9543 Network Slice Services.

## Network Models

### Service Attachment Points (SAPs) {#sap}

{{?RFC9408}} defines a YANG data model for representing an abstract
   view of the provider network topology that contains the points from
   which its services can be attached (e.g., basic connectivity, VPN,
   network slices).  Also, the model can be used to retrieve the points
   where the services are actually being delivered to customers
   (including peer networks).

A SAP network topology can be used for one or multiple service types ('service-type'). Setting this data node to 'network-slice' allows a controller to expose where RFC 9543 Network Slices services are being delivered. It can also be used to check where RFC 9543 Network Slice Services can be delivered.

### AC-augmented SAPs

{{?I-D.ietf-opsawg-ntw-attachment-circuit}} augments the SAP model with more details for managing ACs at the network level.

### Network Slice Topology

{{?I-D.liu-teas-transport-network-slice-yang}} specifies a YANG model for RFC 9543 Network Slice Topology with on exposing a customized topology that contains a topology intent with required SLO/SLEs to express the customer’s intent for resource reservation.

The need for such a model is yet to be justified as the current scope is redundant with, e.g., what can be already achieved using {{?I-D.ietf-teas-actn-vn-yang}}. The authors should motivate why {{?I-D.ietf-teas-actn-vn-yang}} is not sufficient.

### Network Resource Partitions (NRPs)

{{?I-D.ietf-teas-nrp-yang}} specifies a YANG data model for managing NRPs.

### Network Slice Mapping

{{?I-D.dhody-teas-ietf-network-slice-mapping}} specifies an RFC 9543 Network Slice Service mapping YANG model. The model supports the following mappings:

   *  L3NM {{?RFC9182}}
   *  L2NM {{?RFC9291}}
   *  TE {{?I-D.ietf-teas-te-service-mapping-yang}}
   *  NRP

# Control Plane Extensions {#cp-ext}

## BGP Classful Transport Planes

{{?I-D.ietf-idr-bgp-ct}} specifies mechanisms for classifying underlay routes into a set of classes, called Transport Classes, and mapping service-specific routes to a specific Transport Class. For example, {{?I-D.ietf-idr-bgp-ct}} can be used to create a customized topology for Network Slices. These topologies (Transport Classes) will be typically created to satisfy certain TE characteristics. A new Transport Class Route Target Extended Community is defined for this purpose. A Transport Class is identified by a 4-octet identifier: Transport Class ID.

## BGP Color-Aware Routing (CAR)

{{?I-D.ietf-idr-bgp-car}} specifies a new BGP SAFI called BGP Color-Aware Routing (BGP CAR). Colors are defined to characterize an objective (e.g., low latency). To satisfy Network Slice requirements, CAR may be used to establish paths that address specific objectives. These paths will be associated with a Color.

The proposal leverages the BGP Color Extended Community defined in {{?RFC9012}} and builds upon the Color concept defined in {{?RFC9256}}. In addition, a new Extended Community, called Local-Color-Mapping (LCM) Extended Community, is defined to address cases where the granularity of the exposed colors differs when crossing domains.

## Network Resource Partitions (NRPs)

### BGP Flowspec

{{?I-D.ietf-idr-flowspec-network-slice-ts}} specifies a BGP Flowspec extension for NRP traffic steering.

### BGP-LS Filters in SR

{{?I-D.drake-teas-bgp-ls-filter-nrp}} specifies new BGP-LS attributes, called BGP-LS Filters, for NRPs in SR networks. A BGP-LS Filter provides a description of a subset of the links and nodes in an underlay network. Ingress PE selects a path to an egress PE from the topology defined by the BGP-LS Filters it has imported for a given VPN.

{{?I-D.chen-idr-bgp-ls-transport-slice}} adds new BGP-LS attribute TLVs to encode information such as NRP-ID.

### SR Policies Extensions

#### BGP

{{?I-D.ietf-idr-sr-policy-nrp}} and {{?I-D.liu-idr-bgp-network-slicing}} define extensions to BGP in order to advertise NRP ID in an SR Policy. The NRP ID is encoded in 4 octets.

#### BGP-LS

{{?I-D.ietf-idr-bgp-ls-sr-policy-nrp}} specifies SR Policy extensions for NRP in BGP-LS. The NRP ID is encoded in 4 octets.

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

## Network Resource Partitions (NRPs)

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

### SRv6 Resource Programming

{{?I-D.gong-spring-srv6-nrp-flavor}} defines a new SRv6 Endpoint behavior {{?RFC8986}} to associate a SID with a set of NRPs.

### BGP Extensions

{{?I-D.dong-idr-bgp-nrp-policy}} specifies extensions to BGP to advertise NRPs to the network nodes involved in the NRP.

### BGP Link State Extensions

{{?I-D.dong-idr-bgp-ls-scalable-nrp}} specifies extensions to BGP Link-State (BGP-LS) to advertise NRPs to network controllers.

# OAM

## LSP Ping/Traceroute Extensions

{{?I-D.liu-mpls-lsp-ping-nrp}} specifies extenstions to the LSP Ping/Traceroute to convey NRP-ID in SR domains.

The NRP-ID is a encoded as a 4-octet field.

## Precision Availability Metrics (PAM)

{{?RFC9544}} introduces a new set of metrics, called Precision Availability Metrics (PAM). These metrics are used to assess whether a service (e.g., Network Slice Service) is provided in compliance with its specified SLOs.

{{?I-D.clemm-opsawg-pam-ipfix}} specifies a set of new IP Flow Information Export (IPFIX) Information Elements to export precision availability data associated with Flows. These Information Elements are specifically designed to indicate compliance of a Flow with an SLO.

## IPFIX Information Elements for NRP

{{?I-D.liu-opsawg-ipfix-network-slice}} explores how to use IPFIX to export NRP IDs. However, there is currently no one single stable/authoritative specification of NRP-ID. This identifier is being proposed as data plane and control plane extensions. These proposals do not share the same ID format.

The initial version of {{?I-D.liu-opsawg-ipfix-network-slice}} does explain which plan is used, in which layer the ID was exported, etc. Defining an IPFIX IE is useful for network observability, however there is no stable specification yet of the ID to be exported.

## PAM-based Path Computation

{{?I-D.contreras-pce-pam}} specifies a new PCEP object (PRECISION METRIC) for
path calculation with performance requirements expressed as SLOs. The new
PCEP object uses the attributes defined in {{?RFC9544}}.

# Misc

## Scalability Considerations for NRP

{{?I-D.ietf-teas-nrp-scalability}} discusses a set of scenarios for the deployment of NRP with a focus on scalability implications. The document reasons about the increase of requested RFC 9543 Network Slice Services that would require NRPs. Such an increase of slices is speculative at this stage.

## Deployment Considerations

{{?I-D.ma-teas-ietf-network-slice-deployment}} reports a set of "deployments" from various network operators and identifies some considerations for operating Network Slices (e.g., scalability and automation). Most of these reported cases rely upon SRv6. The document does not provide enough details whether these "deployments" are for testing purposes or reflect setups to carry customers' traffic.

# Security Considerations

Security considerations of the mechanisms listed in the document are discussed in the relevant documents that specify these mechanisms.

# IANA Considerations {#IANA}

This document does not make any request to IANA.

--- back

# Acknowledgments
{:numbered="false"}

Thanks to Kaliraj Vairavakkalai for the comments.
