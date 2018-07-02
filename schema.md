# NDEx Common Network Schema
# NC 0.1 - DRAFT - July 2018

### Overview:
NDEx Common (NC) is a modular schema for biological networks to promote integration and interoperability in the Cytoscape Cyberinfrastructure. It is a recommended schema for biological networks published in NDEx, but not a requirement. 

It is important to distinguish the NC schema from the CX format. CX is a JSON network format used in the Cytoscape Cyberinfrastructure to exchange networks. CX is a data format: it does not specify any model for representing biology and related concepts. In contrast, NC specifies controlled vocabularies to annotate nodes and edges to represent biological entities and relationships between them. It also specifies a vocabulary for network meta information, such as the rightsHolder for a network. 

## NC Goals:
- Intuitive for a wide range of biologists
- Simple to use in programs
- Expressive enough for detailed pathway models

NC controlled vocabulary attributes are designed to be independent of each other, facilitating selective adoption of subsets of the schema. NC is intended to provide authors a framework for cooperation but not a straightjacket. A given network can conform to NC as long as it does not have conflicting schema elements where NC controlled vocabulary attributes are used for different meanings. 

# 1 Attribute Values
## 1.1 Attribute Value Data Types:
* string (default)
* boolean
* integer
* double
* long
* list_of_boolean
* list_of_double
* list_of_integer
* list_of_long
* list_of_string

## 1.2 @context (CX Aspect)
@context is a CX aspect that specifies the namespaces and prefixes for identifiers used in the network. It corresponds to the JSON LD @context. (http://www.w3.org/TR/json-ld/#the-context) 

Use of the @context aspect enables applications to interpret prefixed identifiers in attribute values. Where appropriate, namespaces defined in identifiers.org are recommended. The structure of @context below is also described in the CX specification.

Example:
```
"@context": [
  {	
    "cas": "http://identifiers.org/cas/",
    "hprd: "http://identifiers.org/hprd/"
  }
]
```

# 2 Network Attributes
Note that "indexed" attributes are indexed for search by the NDEx server.
## 2.1 name
* name of the network. Less than 150 chars.
* required
* indexed
* data type:string
## 2.2 description
* recommended
* indexed
* data type:string
## 2.3 version 
* recommended for public networks
* conforms to semantic versioning standard (https://semver.org/)
* data type:string
## 2.4 author
* entities primarily responsible for making the network.
* same as multiple dc:creator assertions
* data type:list_of_string
## 2.5 rights
* recommended for public networks
* information about rights held in and over the resource.
* recommended 
* same as dc:rights
* data type:string
## 2.6 rightsHolder
* recommended for public networks
* person or organization owning or managing rights over the resource.
* same as dc:rightsHolder
* data type:string
## 2.7 labels
* optional
* indexed
* keywords describing the network.
* data type:list_of_string

# 3 Node Attributes
## 3.1 name
* Each node requires either a name attribute, a represents (ID) attribute, or both.
* name is a label for humans to read.
* A recommended practice is to use a standard vocabulary for name values.
  * Such as gene symbols, e.g. RBL2.
* data type:string
* name is special in CX: it is encoded in the “n” attribute of a CX node aspect element, not via a nodeAttribute aspect element.
## 3.2 represents
* Each node requires either a name attribute, a represents (ID) attribute, or both.
* represents specifies the primary identifier for entity represented by the node
* If a namespace for the identifier exists,
  * the namespace must be defined in the @context aspect
  * the represents value must use the prefix associated with the namespace 
    * e.g. 'ncbigene:5934'
* data type:string
* represents is special in CX: it is encoded as the “r” attribute of a CX node aspect element, not via a nodeAttribute aspect element.
## 3.3 alias
* optional
* a list of identifiers that reference the same entity as the value of represents
* non-standard identifiers are allowed, such as 'p53' for 'hgnc_symbol:TP53"
* If a namespace for the identifier exists,
  * the namespace must be defined in the @context aspect
  * the represents value must use the prefix associated with the namespace 
    * e.g. 'ncbigene:5934'
* the interpretation of "same entity" is subject to interpretation. In some cases, the equivalence may be approximate, such as mapping between disease ontologies. And a special case is the identifiers used to describe genes and gene products. Frequently gene identifiers are, for the purposes of a given network or dataset, treated as equivalent to protein identifiers. This is such a common practice that NC does not deprecate this use of the aliases attribute.
* data type:string
## 3.4 type
* recommended
* The type of entity represented by the node 
* e.g. "protein", "biological_process". 
* data type: string
* types:
  * gene or gene product
  * gene product
  * protein
  * gene
  * mrna
  * rna
  * phenotype
  * disease
  * chemical
  * drug
  * biological process
  * cellular component
Each term in the node type vocabulary corresponds to one or more terms in standardized vocabularies. If a network requires node types outside this vocabulary, the best practice is to adopt additional term names from standardized vocabularies and document their corresponding namespace identifiers in the network description, e.g. "non-protein coding RNA" is corresponds to 'SIO:000790'. (A human-readable definition is sufficient for most use cases and no computable structure has been defined as of this writing.)
## 3.5 link
* A list of links associated with the node. 
* formats:
  * URL
  * Markdown link
  * HTML link
* data type: list_of_string

# 4 Edge Attributes
The semantics of edges are expressed by the interaction and a mechanism attribute. The edge interaction types are very simple, very general. Edge attributes such as "mechanism" provide nuance in the expression of edge semantics. 
## 4.1 interaction
* optional
* The type of the edge, its primary meaning.
* types:
  * type-of
  * part-of
  * correlates-with
  * associates-with
  * interacts-with
  * regulates
* data type: list_of_string
* interaction is special in CX: it is encoded in the "i" attribute of a CX edge aspect element, not via a CX edgeAttribute aspect element.
## 4.2 citation
* optional
* a list of references to sources providing evidence supporting the edge. 
* references that are identifiers in standard namespaces such as PubMed must have a namespace prefix and the namespace must be defined in @context.  
  * i.e. pubmed:123456
* references can be:
  * ids in standard namespaces
  * URLs
  * URIs
  * DOIs
  * text in standard citation format
  * arbitrary strings
* data type: list_of_string
## 4.3 mechanism
* optional 
* The mechanism(s) by which the interaction is mediated
* data type: list_of_string
* mechanisms:
  * chemical reaction
  * small molecule catalysis
  * relocalization
  * binding
  * cleavage
  * stabilization
  * transcriptional regulation
  * gene methylation
  * gene acetylation
  * GAP reaction
  * GEF reaction
  * palmitoylation
  * neddylation
  * phosphorylation
  * trimethylation
  * ubiquitination
  * methylation
  * acetylation
  * glycosylation
  * hydroxylation
  * sumoylation
  * farnesylation
  * s-nitrosylation
  * tyrosination
## 4.4 polarity
* optional 
* polarity specifies whether the interaction is a positive or negative relationship, e.g. "upregulates" vs. "downregulates". 
* If not set, or set to 0, then the relationship has undefined sign, e.g. simply "regulates" 
* data type: integer
* values: 1| -1 | 0
## 4.5 evidence
* recommended
* evidence describes specific evidence supporting the edge, in contrast to the citation aspect which indicates the sources of evidence.
* The value is a list of strings where each element is either text or a string representation of a JSON object describing the evidence with the following fields:
  * source
    * same format as the values for the citation attribute
  * type
    * the type of the source of the evidence
      * journal
      * book
  * text
    * text from the source that specifically supports the edge.
* data type: list_of_strings
## 4.6 contact
* The interaction is mediated by direct physical contact. 
  * Phosphorylation of a substrate by a kinase implies contact = true.
* data type: boolean
* default: false



