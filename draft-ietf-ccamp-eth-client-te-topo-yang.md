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
    org: Volta Networks
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

--- abstract

   A transport network is a server-layer network to provide connectivity
   services to its client.  In this draft the topology of Ethernet with
   TE is described with YANG data model.

--- middle

# Introduction

   A transport network is a server-layer network designed to provide
   connectivity services for a client-layer network to carry the client
   traffic transparently across the server-layer network resources.  The
   topology model in Traffic-Engineered network has been defined in both
   generic way and technology-specific way.  The generic model, which is
   the base TE YANG model, can be found at {{!RFC8795}}.  Technology-
   specific models, such as OTN/WSON topology model, have also been
   defined in {{!I-D.ietf-ccamp-otn-topo-yang}} and {{?RFC9094}} respectively.
   Corresponding topology on client-layer is also required, to have a
   complete topology view from the perspective of network controllers.

   This document defines a data model of all client-layer Topology,
   using YANG language defined in {{!RFC7950}}.  The model is augmenting
   the generic TE topology model, and can be used by either applications
   exposing to a network controller or among controllers.  Furthermore,
   it can be used by an application for topology description in client-
   layer network.

#  Terminology and Notations

   A simplified graphical representation of the data model is used in
   this document.  The meaning of the symbols in the YANG data tree
   presented later in this document is defined in {{?RFC8340}}.  They are
   provided below for reference.

-  Brackets "\[" and "]" enclose list keys.

-  Abbreviations before data node names: "rw" means configuration
  (read-write) and "ro" state data (read-only).

-  Symbols after data node names: "?" means an optional node, "!"
  means a presence container, and "*" denotes a list and leaf-list.

-  Parentheses enclose choice and case nodes, and case nodes are also
  marked with a colon (":").

-  Ellipsis ("...") stands for contents of subtrees that are not
  shown.

#  YANG Model for Topology of Client Layer

## YANG Tree for Ethernet Topology

~~~~ ascii-art
{::include ietf-eth-te-topology.tree}
~~~~
{: #fig-eth-topology-tree title="Ethernet topology YANG tree" artwork-name="ietf-eth-te-topology.tree"}

# YANG Code for Topology Client Layer

## The ETH Topology YANG Code

~~~~ yang
{::include ietf-eth-te-topology.yang}
~~~~
{: #fig-te-yang title="Ethernet topology YANG module"
sourcecode-markers="true" sourcecode-name="ietf-eth-te-topology@2019-11-18.yang"}

# Considerations and Open Issue

   Editor Notes: This section is used to note temporary discussion/
   conclusion that to be fixed in the future version, and will be
   removed before publication.

   Update in draft-zheng-ccamp-client-topo-yang-10: there is no open
   issue in this version.

   201902: we have noticed that Ethernet is the only client signal (on
   the perspective of OTN) which need a topology.  So it is possible
   that the title of this document will be changed to "A YANG Data Model
   for Ethernet Topology".  The proposal of this work is that the
   document will follow up the progress of draft-zheng-ccamp-client-
   signal-yang, with draft-zheng-ccamp-client-tunnel-yang together.
   (solved in -06)

   201902: will have to align with TE topology model, currently is a
   totally different format with necessary parameters, a big change is
   expected.  (solved in -06.)

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
      prefix:    ethtetopo
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
