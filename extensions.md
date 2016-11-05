### Extensions Representation


Now FHIR extensions is represented as collection of ... 

Semantic of extensions mostly imply key-value meaning, take a look at
popular extensions:

* us/race
* ....


### Proposal


Same scope only prefix

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
* Uniformity
* JSON schemas (Profiles)
