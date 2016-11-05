# FHIR standard ideas for considiration

### Patch & Diff Resources

Most of FHIR Operations are working on Resource's Level of Granularity, which brings
some problems (technical, concurrent updates) when you need change only specific data 
elements and do not want to update resource as a whole. 
Proposal is to introduce new Patch Resource which could represent
changes of specific elements in resource. This resource essentialy could be 
represented as a set of mutations of specific data elements.
Every mutation consist of: 
* *selector* (fluent/fhirpath)
* *operation* (replace, append, increment)
* *operation arguments* 

Here is an naive example: 

```yaml
resourceType: 'Patch'
target: 'Patient/<id>' 
changes:
- path: 'birthDate'
  operation: 'set'
  arguments: 
  - '1978-0102'
- path: 'name.first().given'
  operation: 'append'
  arguments: 
  - 'NewGivenName'
- path: 'contact'
  operation: 'append'
  arguments: 
  - {... new contanct ...}
```

Patch Resources could we written by hands using power of *fluentpath* 
and operations or generated automaticaly as a diff between new and old versions of resource.

Slightly modified *Patch Resource* could be used to represent *Diff* between two versions of 
resources - *Diff Resource*. 
*Diff Resource*  is a good candidate for alternative representation of resource updates history,
providing more compact and convenient form to inspect changes. 

*Diff Resource and/or Patch Resource* could be used to handle changes of FHIR Standard by themself

* Represent history of StructureDefinitions/Profiles
* Smart patches of standard (renames, etc)
* Represent Change Requests as a set of Patch Resources (aka Pull Requests)
* Autogenerate data migrations between different versions of FHIR 
* Patch Operation connected with Search could represent some batch updates rules - like RDBMS `update ... where ..` statement


More work is required to identify how to 

* apply Patch Resources in cases of 
  * was inspected one element, but collection or nothing was returned by selector
  * resource does not exists
* design of *operations* (like increment numbers, collections/timestamp specific ops)


### Transaction Log 

### Streams & Subscriptions

### Swagger integration

### Terminology

### TestScript

