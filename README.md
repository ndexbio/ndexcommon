# NDEx Common Network Schema


# Overview:
NDEx Common (NC) is a modular schema for biological networks to promote integration and interoperability in the Cytoscape Cyberinfrastructure. It is a recommended schema for biological networks published in NDEx, but not a requirement. 

It is important to distinguish the NC schema from the CX format. CX is a JSON network format used in the Cytoscape Cyberinfrastructure to exchange networks. CX is a data format: it does not specify any model for representing biology and related concepts. In contrast, NC specifies controlled vocabularies to annotate nodes and edges to represent biological entities and relationships between them. It also specifies a vocabulary for network meta information, such as the rightsHolder for a network. 

# Design Goals:
- Intuitive for a wide range of biologists
- Simple to use in programs
- Expressive enough for detailed pathway models

NC controlled vocabulary attributes are designed to be independent of each other, facilitating selective adoption of subsets of the schema. NC is intended to provide authors a framework for cooperation but not a straightjacket. A given network can conform to NC as long as it does not have conflicting schema elements where NC controlled vocabulary attributes are used for different meanings. 

# Specification
## (NC 0.1 - DRAFT - July 2018)[https://github.com/ndexbio/ndexcommon/schema.md]
The draft release of NDEx Common. In use for new NDEx-managed network content.
In many cases, elements in this draft are treated specially by the NDEx web user interface at www.ndexbio.org.
## (NC Schema Development)[https://github.com/ndexbio/ndexcommon/blob/master/schema-dev]
NDEx Common attributes in testing or experimental use. Feedback welcome.
