---
coding: utf-8

title: A YANG Data Model for Ethernet TE Topology
abbrev: "ETH Topology Transport YANG Model"
category: info

docname: draft-ietf-ccamp-eth-client-te-topo-yang-04
submissiontype: IETF
v: 3
workgroup: CCAMP Working Group

stand_alone: yes
pi: [toc, sortrefs, symrefs, comments]

author:
  -
    name: Chaode Yu
    org: Huawei Technologies
    email: yuchaode@huawei.com
  -
    name: Haomian Zheng
    org: Huawei Technologies
    street: H1, Huawei Xiliu Beipo Village, Songshan Lake
    city: Dongguan
    region: Guangdong
    code: 523808
    country: China
    email: zhenghaomian@huawei.com
  -
    name: Aihua Guo
    org: Futurewei
    email: aihuaguo@futurewei.com
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    name: Yunbin Xu
    org: CAICT
    email: xuyunbin@caict.ac.cn
  -
    name: Yang Zhao
    org: China Mobile
    email: zhaoyangyjy@chinamobile.com
  -
    name: Xufeng Liu
    org: Alef Edge
    email: xufeng.liu.ietf@gmail.com

contributor:
  -
    name: Yanlei Zheng
    org: China Unicom
    email: zhengyanlei@chinaunicom.cn
  -
    name: Zhe Liu
    org: Huawei Technologies
    email: liuzhe123@huawei.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Yingxi Yao
    org: Shanghai Bell
    email: yingxi.yao@nokia-sbell.com
  -
    name: Giuseppe Fioccola
    org: Huawei Technologies
    email: giuseppe.fioccola@huawei.com

normative:
  ITU_G.8021:
    title: Generic protection switching - Linear trail and subnetwork protection
    author:
      org: ITU-T Recommendation G.808.1
    date: May 2014
    seriesinfo: ITU-T G.808.1

--- abstract

This document describes a YANG data model for Ethernet networks when used either as a client-layer network of an underlay transport network (e.g., an Optical Transport Network (OTN)) or as a transport network technology.

--- middle

# Introduction

To be added

   A transport network is a server-layer network designed to provide
   connectivity services for a client-layer network to carry the client
   traffic transparently across the server-layer network resources.

A transport network typically utilizes several different transport technologies such as the Optical Transport Networks (OTN) or packet transport such as provided by the MPLS-Transport Profile (MPLS-TP).

An Ethernet network can be either a client-layer network of an underlay transport network or a transport network technology.

This document describes a YANG data model for Ethernet networks when used either a client-layer network of an underlay transport network (e.g., an Optical Transport Network (OTN)) or a transport network technology.

The YANG model defined in this document augments from the TE topology YANG model defined in {{!RFC8795}}, and imports from the generic Ethernet types defined in {{!I-D.ietf-ccamp-client-signal-yang}}.

The YANG data model in this document conforms to the Network Management Datastore Architecture defined in {{!RFC8342}}.

## Terminology and Notations

The following terms are defined in {{!RFC7950}} and are not redefined
here:

- client

- server

- augment

- data model

- data node

The following terms are defined in {{!RFC6241}} and are not redefined
here:

- configuration data

- state data

The terminology for describing YANG data models is found in
{{!RFC7950}}.

## Tree Diagram

A simplified graphical representation of the data model is used in
{{eth-topology-tree}} of this document.  The meaning of the symbols in these
diagrams is defined in {{?RFC8340}}.

## Prefix in Data Node Names

In this document, the names of data nodes and other data model
objects are prefixed using the standard prefix associated with the
corresponding YANG imported modules, as shown in {{tab-prefixes}}.

  In this document, names of data nodes and other data model objects
  are prefixed using the standard prefix associated with the
  corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix     | YANG module           | Reference
| yang       | ietf-yang-types       | {{!RFC6991}}
| etht-types | ietf-eth-tran-types   | \[RFCYYYY]
| nw         | ietf-network          | {{!RFC8345}}
| nt         | ietf-network-topology | {{!RFC8345}}
| tet        | ietf-te-topology      | {{!RFC8795}}
| eth-tet    | ietf-eth-te-topology  | RFCXXXX
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note: Please replace YYYY and XXXX with the number
assigned to the RFC once this draft becomes an RFC.

{: #eth-topo-overview}

# Ethernet Topology Model Overview

This document aims to describe the data model for Ethernet topology.

As a classic Traffic-engineering (TE) technology, Ethernet can provide packet
switching in transport network {{ITU_G.8021}}.

Therefore, the YANG
module presented in this document augments from a more generic
Traffic Engineered (TE) network topology data model, i.e., the ietf-
te-topology, as specified in {{!RFC8795}}.  In section 6 of {{!RFC8795}},
the guideline for augmenting TE topology model was provided, and in
this draft, we augment the TE topology model to describe the topology
in Ethernet network.  Common types, identities and groupings defined in
{{!I-D.ietf-ccamp-client-signal-yang}} is reused in this document.  {{!RFC8345}}
describes a network topology model and provides the fundamental model
for {{!RFC8795}}.  However, this work is not directly augmenting
{{!RFC8345}}.  {{fig-eth-topo}} shows the augmentation relationship.

~~~~ ascii-art
                      +-------------------------+
         TE generic   |    ietf-te-topology     |
                      +------------+------------+
                                   ^
                                   |
                                   | Augments
                                   |
                      +------------+------------+
         Ethernet     |  ietf-eth-te-topology   |
                      +-------------------------+
~~~~
{: #fig-eth-topo title="Relationship between Ethernet and TE topology models"}

   The entities and TE attributes, such as node, termination points and
   links, are still applicable for describing an Ethernet topology and the
   model presented in this document only specifies technology-specific
   attributes/information.

## Attributes Augmentation

  Given the guidance for augmentation in {{!RFC8795}}, the following
  technology-specific augmentations need to be provided:

  - A network-type to indicate that the TE topology is an Ethernet
    Topology, as follow:

~~~~
       augment /nw:networks/nw:network/nw:network-types/tet:te-topology:
         +--rw eth-tran-topology!
~~~~

  - TE Bandwidth Augmentations as described in {{eth-bandwidth}}.

  - TE Label Augmentations as described in {{eth-label}}.

{: #eth-bandwidth}

## TE Bandwidth Augmentations

Following the guidelines in {{!RFC8795}}, the model augments
all the occurrences of the te-bandwidth container with the Ethernet technology
specific attributes using the eth-bandwidth grouping defined in {{!I-D.ietf-ccamp-client-signal-yang}}.

{: #eth-label}

## TE Label Augmentations

The model augments all the occurrences of the label-restriction list
with Ethernet technology specific attributes using the eth-label-restriction grouping defined in {{!I-D.ietf-ccamp-client-signal-yang}}.

Moreover, following the guidelines in {{!RFC8795}}, the model augments
all the occurrences of the te-label container with the Ethernet technology
specific attributes using the eth-label and
eth-label-step groupings defined in {{!I-D.ietf-ccamp-client-signal-yang}}.

{: #eth-topology-tree}

# YANG Tree for Ethernet Topology

~~~~ ascii-art
{::include ietf-eth-te-topology.tree}
~~~~
{: #fig-eth-topology-tree title="Ethernet topology YANG tree" artwork-name="ietf-eth-te-topology.tree"}

{: #eth-topology-yang}

# Ethernet Topology YANG Code

~~~~ yang
{::include ietf-eth-te-topology.yang}
~~~~
{: #fig-te-yang title="Ethernet topology YANG module"
sourcecode-markers="true" sourcecode-name="ietf-eth-te-topology@2023-09-08.yang"}

# IANA Considerations

   It is proposed that IANA should assign new URIs from the "IETF XML
   Registry" {{!RFC3688}} as follows:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-eth-te-topology
      Registrant Contact:  The IESG.
      XML: N/A, the requested URI is an XML namespace.
~~~~

   This document registers following YANG modules in the YANG Module
   Names registry {{!RFC7950}}.

~~~~
      name:      ietf-eth-te-topology
      namespace: urn:ietf:params:xml:ns:yang:ietf-eth-te-topology
      prefix:    eth-tet
      reference: RFC XXXX
~~~~

RFC Editor: Please replace XXXX with the RFC number assigned to this document.

# Manageability Considerations

   TBD.

# Security Considerations

   The data following the model defined in this document is exchanged
   via, for example, the interface between an orchestrator and a
   transport network controller.  The security concerns mentioned in
   {{!RFC8795}} for using ietf-te-topology.yang model also applies to this
   document.

   The YANG module defined in this document can be accessed via the
   RESTCONF protocol defined in {{!RFC8040}}, or maybe via the NETCONF
   protocol {{!RFC6241}}.

   There are a number of data nodes defined in the YANG module which are
   writable/creatable/deletable (i.e., config true, which is the
   default).  These data nodes may be considered sensitive or vulnerable
   in some network environments.  Write operations (e.g., POST) to these
   data nodes without proper protection can have a negative effect on
   network operations.

   Editors note: to list specific subtrees and data nodes and their
   sensitivity/vulnerability.

--- back

# Acknowledgments
{:numbered="false"}

   We would like to thank Igor Bryskin and Daniel King for their
   comments and discussions.
