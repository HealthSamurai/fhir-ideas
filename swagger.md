# FHIR as superset of Swagger

FHIR is disruptive standard for Health Interoperability based 
on modern web technologies and awesome community. 
[Swagger](http://swagger.io/) is a modern web technology for REST API documentation.
Starting January 1st 2016 the Swagger Specification has been moved 
to the [Open API Initiative](https://www.openapis.org/) and 
is the foundation of the OpenAPI Specification. 
Swagger has a good tooling support [official](http://swagger.io/tools/) and [community](http://swagger.io/open-source-integrations/).


Both was started about the same time and have many intersections. There are two
potential bridges between FHIR and Swagger:

* Generate swagger spec from  FHIR metadata
* Migrate FHIR core to swagger (Do not hit my fingers, i'm musician :)!)



## Comparison

FHIR specifies informational models (Resources) using StructureDefinitions and
REST operations by Operation, SearchParameter resources or in text of specification. 

```yaml
resourceType: StructureDefinition
type: Patient
...
snapshot:
  - ...
  - id: Patient.birthDate
    path: Patient.birthDate
    definition: A name associated with the individual.
    min: 0
    max: "1"
    type:
    - code: date
  - id: Patient.name
    path: Patient.name
    definition: A name associated with the individual.
    min: 0
    max: "*"
    type:
    - code: HumanName
  - ...
```

Swagger specify data model using [JSON schema](http://json-schema.org/) and REST API using swagger document.
Here is how FHIR API fragment will looks in swagger:

```yaml
type: object
properties:
  birthDate: 
    type: date
  name: 
    type: array
    items:
      $ref #/definitions/HumanName
      description: A name associated with the individual.
```

JSON schema is a [separate standard](http://json-schema.org/). The latest IETF published draft is v4 
and there is proposals for [version 5](https://github.com/json-schema/json-schema/wiki/v5-Proposals). 
There are plenty [JSON Schema validator engines](http://json-schema.org/implementations.html).

Last builds of FHIR contains JSON schema and there is some pilot projects to generate JSON schema
from FHIR metadata - https://github.com/BlackPearSw/fhir-schema-dstu2, https://github.com/niquola/fhir-schema. 
Also our [aidbox](http://aidbox.io) validation is completly build on top of extended JSON schema.

## REST API documentation

Basic FHIR operations like CRUD (Create, Read, Update, Delete), Search & History API 
sadly are not described in machine readable format. Here is how they could look in swagger:

```yaml
title: FHIR REST API
paths:
  /Patient":
    post:
      parameters: 
      - name: resource
        in: body 
        type: { $ref: '#/definitions/Patient' }
       ....
  /Patient/{id}:
    get:
      description "Read specific patient ..."
      - name: id
        in: path 
        type: { $ref: '#/definitions/id' }
      resposes:
        200:
          type: { $ref: '#/definitions/Patient' }
definitions:
  Patient: ....
```
....


## Polymorphic types problems


Observation.value[x] means  valueString or valueRation


```yaml
properties:
  value: 
    type: object
    properties: 
      type: { enum: ['string', 'date', 'number']}
      string: {}
      date: {}
      quantity: {}
```


## Swagger UI
