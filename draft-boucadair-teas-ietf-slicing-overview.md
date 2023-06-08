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

This document provides an overview of documents that are being XXX. This document is meant to
catalog slice-related specification within the IETF and ease coordinating the efforts and XXX.

--- middle

# Introduction

TBC.

Some proposals argue in favor of specifyting extensions to convey specific identifiers in packets. However,
distinct identifiers are being proposed: slice identifier, NRP identifier, VTN identifier, VTN resource identifier, etc.

TBC.


# Reference Framework and Architecture

{{?I-D.ietf-teas-ietf-network-slices}} is the authoritative IETF framework for Network Slices. This document provides definitions for a set of core terms and specifies a framework for the provision
of Network Slice Services over networks that are deployed using technologies that are owned by the IETF (IP, MPLS, etc.). The document refers to such slices as IETF Network Slice.

{{?I-D.ietf-teas-ietf-network-slices}} provides a clear distinction between:

* the "IETF Network Slice service" which is the service delivered to the customer and which is agnostic to the technologies and mechanisms
   used by the service provider, and
* the "IETF Network Slice" which is the realization of the service in the service provider's network achieved by partitioning network resources and by applying a set of mechanisms within the network.

The IETF Network Slice service is specified in terms of:

* a set of Service Demarcation Point (SDP),
* a set of one or more connectivity constructs between subsets of these SDPs, and
*  a set of service objectives for each SDP sending to each connectivity construct.

Optionally, the underlying network can be customized to select a subset of resources that are suitable for the delivery of an IETF Network Slice service. Such a customization can be achieved by creating a set of Network Resource Partitions (NRPs). Note that IETF Network Slices could be hosted directly on the underlay network (i.e., without requiring any NRP).

{{?I-D.ietf-teas-ietf-network-slices}} does not provide any recommendation about the technological means to realize an IETF Network Slice service. These considerations are deployment specific.

# Models for Realizing Network Slices

## Using Current IP/MPLS Technologies

{{?I-D.srld-teas-5g-slicing}}:
A Realization of IETF Network Slices for 5G Networks Using Current IP/ MPLS Technologies

## New XXXX

{{?I-D.ietf-teas-ns-ip-mpls}}: Realizing Network Slices in IP/MPLS Networks

## OTN Slicing

{{?I-D.ietf-ccamp-yang-otn-slicing}}: Framework and Data Model for OTN Network Slicing (note that this doc also specif data models)

## VPN+

   {{?I-D.ietf-teas-enhanced-vpn}} describes the framework and the
   candidate component technologies for providing enhanced VPN (VPN+)
   services based on VPN and Traffic Engineering (TE) technologies.
   Enhanced VPN (VPN+) can be used for the realization of IETF network
   slices.

## Instantiation in Service Providers Networks

{{?I-D.barguil-teas-network-slices-instantation}}: Instantiation of IETF Network Slices in Service Providers Network

## Network Slice Controllers

{{?I-D.contreras-teas-slice-controller-models}}: IETF Network Slice Controller and its associated data models

## SR-based 2-Level Hierarchical Network Slices

{{?I-D.gong-teas-hierarchical-slice-solution}}: Segment Routing based Solution for Hierarchical IETF Network Slices

This document describes a Segment Routing based solution for two-
   level hierarchical IETF network slices. Level-1 network slice is
   realized by associating Flex-Algo with dedicated sub-interfaces, and
   level-2 network slice is realized by using SR Policy with additional
   NRP-ID on data plane.

## Realization of Composite Network Slices

{{?I-D.li-teas-composite-network-slices}}: Realization of Composite IETF Network Slices

   This document first describes the possible use cases of composite
   IETF network slices, then it provides considerations about the
   realization of composite IETF network slices.  For the interaction
   between IETF network slices with 5G network slices, the identifiers
   of the 5G network slice may be introduced into IETF networks.  For
   the multi-domain IETF network slices, the Inter-Domain Network
   Resource Partition Identifier (Inter-domain NRP ID) is defined.  For
   the hierarchical IETF network slices, the structure of the NRP ID is
   discussed.  These network slice-related identifiers may be used in
   the data plane, control plane and management plane of the network for
   the instantiation and management of composite IETF network slices.
   This document also describes the management considerations of
   composite network slices.

# Applicability and Mapping Scenarios

## 3GPP 5G End-to-End Network Slices

{{?I-D.ietf-teas-5g-network-slice-application}}: IETF Network Slice Application in 3GPP 5G End-to-End Network Slice


## ACTN

{{?I-D.ietf-teas-applicability-actn-slicing}}: Applicability of Abstraction and Control of Traffic Engineered Networks (ACTN) to Network Slicing

## Mobility-Aware Transport Network Slicing

{{?I-D.ietf-dmm-tn-aware-mobility}}: This document describes mapping of 5G slices to IP or Layer 2
   transport network slices when the IP transport network (slice
   provider) is separated from the networks in which the 5G network
   functions are deployed (for example, 5G functions distributed across
   data centers).

## DETNET

{{?I-D.sw-detnet-network-slice-mapping-yang}}: YANG Data Model for DetNet Mapping with Network Slice


# Orchestration and Data Models

## Common Models

{{?I-D.boro-opsawg-teas-common-ac}}: A Common YANG Data Model for Attachment Circuits


## Service Models

### Attachment Circuit as a Service Data Model

{{?I-D.boro-opsawg-teas-attachment-circuit}}: YANG Data Models for 'Attachment Circuits'-as-a-Service (ACaaS)


### Network Slice Service Data Model

{{?I-D.ietf-teas-ietf-network-slice-nbi-yang}}: A YANG Data Model for the IETF Network Slice Service


## Network Models

### Service Attachment Points (SAPs)

### AC-augmented SAPs

{{?I-D.boro-opsawg-ntw-attachment-circuit}}: A Network YANG Data Model for Attachment Circuits

### Network Slice Topology

{{?I-D.liu-teas-transport-network-slice-yang}}: IETF Network Slice Topology YANG Data Model

### NRP

{{?I-D.wdbsp-teas-nrp-yang}}: A YANG Data Model for Network Resource Partitions (NRPs)

### Network Slice Mapping

{{?I-D.dhody-teas-ietf-network-slice-mapping}}: IETF Network Slice Service Mapping YANG Model


   Currently following mapping are supported:

   *  L3NM: The L3 network model (L3NM) describes a L3VPN Service in the
      Service Provider Network.  It contains information of the Service
      Provider network and might include allocated resources.  It can be
      used by network controllers to manage and control the L3VPN
      Service configuration in the Service Provider network.  This model
      maps an IETF network slice to a L3VPN ID.

   *  L2NM: The L2 network model (L2NM) describes a L2VPN Service in the
      Service Provider Network.  It contains information of the Service
      Provider network and might include allocated resources.  It can be
      used by network controllers to manage and control the L2VPN
      Service configuration in the Service Provider network.  This model
      maps an IETF network slice to a L2VPN ID.

   *  TE: The TE mapping is specified in
      [I-D.ietf-teas-te-service-mapping-yang].  The mapping can be done
      to the following TE resouces:

      -  Virtual Networks (VN) [RFC8453]

      -  TE-Tunnels

      -  TE-Topology

   *  NRP: [I-D.ietf-teas-ietf-network-slices] defines IETF network
      slice services that provide connectivity coupled with network
      resources commitment between a number of endpoints over a shared
      network infrastructure and, for scalability concerns, defines NRP
      to host one or a group of network slice services according to
      characteristics including SLOs and SLEs.  Along with mapping to
      VPN, this model maps an IETF network slice to a NRP ID.



# Control Plane Extensions

## NRP

### BGP Flowspec

{{?I-D.ietf-idr-flowspec-network-slice-ts}}: BGP Flowspec for IETF Network Slice Traffic Steering

### BGP-LS Filters

{{?I-D.drake-teas-bgp-ls-filter-nrp}}: Using BGP-LS Filters to Instanted Network Resource Partitions

### SR Policies Extensions

#### BGP

{{?I-D.dong-idr-sr-policy-nrp}}: BGP SR Policy Extensions for Network Resource Partition

{{?I-D.liu-idr-bgp-network-slicing}}: This document defines extensions to BGP in order to advertise NRP-ID
   in SR policy.

#### BGP-LS

{{?I-D.chen-idr-bgp-ls-sr-policy-nrp}}: SR Policies Extensions for NRP in BGP-LS


### PCEP Extensions

{{?I-D.dong-pce-pcep-nrp}}: Path Computation Element Communication Protocol (PCEP) Extensions for Network Resource Partition (NRP)

### LSP Ping/Traceroute Extensions

{{?I-D.liu-mpls-lsp-ping-nrp}}: LSP Ping/Traceroute for SR-MPLS NRP SIDs

# Data Plane Extensions

## Slice Identifier in the Source Address

{{?I-D.cheng-spring-srv6-encoding-network-sliceid}}: Encoding Network Slice Identification for SRv6

xx
   When an SR domain enables network slicing, the ingress PE should
   reserve least significant bits in a local IPv6 address for slicing
   use. The number of bits used to encode SLID is governed by local
   policy and uniform within the SR domain.

   When a packet enters the SR domain from an ingress PE, the ingress
   PE encapsulates the packet in an outer IPv6 header and optional SRH
   as defined in [RFC8754]. The ingress PE MAY also classify the packet
   into a slice and set the slice identifier as follows:

   o Write this SLID in the least significant bits of source address
      of the outer IPv6 header.

   o Set the SLID Presence Indicator (SPI) in the outer IPv6 header.
xx


## Slice Identifier in IPv6 Flow Label

The Slice Identifier (SLID) is a value encoded within the IPv6 packet
   that allows transit routers to process the packet according to
   network slice-based policy.

{{?I-D.filsfils-spring-srv6-stateless-slice-id}} proposes to encode the SLID in a portion of the IPv6
Flow Label.

## VTN Resource ID in an IPv6 Extension Header

   {{?I-D.ietf-6man-enhanced-vpn-vtn-id}} describes the mechanism of
   carrying the VTN resource ID (which is equivalent to NRP-ID) of a
   network domain in the IPv6 Hop-by-Hop (HBH) extension header.

## Slice Identifier in the MPLS Entropy Label

{{?I-D.decraene-mpls-slid-encoded-entropy-label-id}}: Using Entropy Label for Network Slice Identification in MPLS networks.


This document encodes the slice identifier in a portion of the MPLS
   Entropy Label (EL) defined in [RFC6790].




## NRP

### Resource-aware Segments

In SR networks, an NRP can be established and represented using either
a set of NRP-specific resource-aware segments {{?I-D.ietf-spring-resource-aware-segments}}
{{?I-D.ietf-spring-sr-for-enhanced-vpn}}.

### NRP ID in SRv6

{{?I-D.liu-spring-nrp-id-in-srv6-segment}}: NRP ID in SRv6 segment

### MPLS Network Actions

{{?I-D.li-mpls-mna-nrp-selector}}: MPLS Network Actions for Network Resource Partition Selector

# spec/target WG

# Misc

## Scalability Considerations for NRP

{{?I-D.ietf-teas-nrp-scalability}}

## Virtual Transport Networks

### IS-IS MT

Using IS-IS Multi-Topology (MT) for Segment Routing based Virtual Transport Network
{{?I-D.ietf-lsr-isis-sr-vtn-mt}}

### BGP-LS

BGP-LS with Multi-topology for Segment Routing based Virtual Transport Networks
{{?I-D.ietf-idr-bgpls-sr-vtn-mt}}

This document describes a
   mechanism to distribute the information of SR based VTNs to the
   network controller using BGP-LS with Multi-
   Topology.


# Security Considerations

TBC.

# IANA Considerations {#IANA}

This document does not make any request to IANA.

--- back

# Acknowledgments
{:numbered="false"}

Thanks to TBC.
