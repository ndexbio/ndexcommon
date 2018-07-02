# NDEx Common Network Schema Specification
This is the draft release of NDEx Common. In use for new NDEx-managed network content. In many cases, elements in this draft are treated specially by the NDEx web user interface at www.ndexbio.org. For example, attributes marked as "indexed" are indexed for search by the NDEx server.
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
