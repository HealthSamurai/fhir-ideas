
FHIR is disruptive standard for Health Interoperability based 
on modern web technologies and awesome community. 
Swagger is a modern web technology for REST API documentation.
Both was started about the same time and have many intersections.

FHIR specify informational models (Resources) using StructureDefinitions and
REST operations by Operation and SearchParameter resources. 

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
Basic operations like CRUD on resources are not described in machine readable format, 
so here is human readable description:

....


Swagger specify data model using [JSON schema]() and REST API using swagger document.
Here is how FHIR API fragment will looks in swagger:

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
  Patient:
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

## JSON schema engines

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
