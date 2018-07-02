# NDEx Common Network Schema Specification Development
# 3 Node Attributes
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


