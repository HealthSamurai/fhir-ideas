### Extensions Representation


Now FHIR extensions is represented as collection of ... 

Semantic of extensions mostly imply key-value meaning, take a look at
popular extensions:

* us/race
* ....


### Proposal


Same scope only prefix

v1

```
resourceType: 'Patient'
$schema:
  us/race: {type: "string", uri: "http://us.gov/race"}
us/race "Something"
birthDate: "1966-01-01"
name:
- given: ["One", "Two"]

-- or
resourceType: 'Patient'
$schema:
  definitions: ['url', 'url']
us/race "Something"
birthDate: "1966-01-01"
name:
- given: ["One", "Two"]

```

Scope by extension

```
resourceType: 'Patient'
id: 'someid'
extension:
  $schema: 
    race: {type: "string", uri: "us.gov/race"}
  race "Something"
birthDate: "1966-01-01"
name:
- given: ["One", "Two"]

```

Primitives extensions:

```
resourceType: 'Patient'
birthDate: "1966-01-01"
_birthDate:
  extension: ....
ns/birthDate/some-primitive-extension:"value"

```


## Pros & Contra

* Key-Value semantic
* Easy access
  * DataBases
  * Frontend (JS, UI)
* Uniformity with core
* JSON schemas (Profiles)


$schema could be turned into definition property which could contain all definitions
including version or refer by uri. So we could get self contained resource with schema
and profiles. When you are serving Bundle definitions could be poped to Bundle root, so
you do not need to repeat them.

```yaml

resourceType: 'Patient'
definittions:
 core: StructureDefinition with FHIR version
 us: US extensions used in this resource
 some-profile:  ...
attr: Value
ext/attr: Valeu

```
