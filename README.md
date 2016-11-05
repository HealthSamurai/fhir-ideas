# FHIR standard ideas for considiration

### Patch & Diff Resources

Most of FHIR Operations are working on Resource's Level of Granularity, which brings
some problems (technical, concurrent updates) when you need change only specific data 
elements and do not want to update resource as a whole. 
Proposal is to introduce new Patch Resource which could represent
changes of specific elements in resource. This resource essentialy could be 
represented as a set of mutations of specific data elements.
Every mutation consist of: 
* `selector` (fluent/fhirpath)
* `operation` (replace, append, increment)
* `operation arguments`  (values)

[Read more..](patch.md)

### Transaction Log 

### Alternative Extensions Representation

### Inlined References Representation for Bundles and Contained Resources

### Streams & Subscriptions

### Swagger integration

### Terminology

### TestScript

