# Terminology Server Syndication Standard

As part of a strategy to move towards wider adoption of healthcare terminology servers which implement the HL7 FHIR Terminology Services x, a more effective way of distributing terminology would be from server to server through a syndication feed.

Based on existing work implemented by the [Australian Digital Health Agency](https://www.healthterminologies.gov.au/specs/v2/conformant-server-apps/syndication-api/syndication-feed/), this feed extends the [Atom Syndication Standard](https://tools.ietf.org/html/rfc4287). It is not specific to SNOMED CT and can be used for any relevant healthcare standard,

The additions here are from SNOMED International and are in the sct namespace for distributing SNOMED CT content. 

## Details

Example feed can be seen in this repo - [feed-example.xml](feed-example.xml)

The extensions to the specification are as follows:

```
<sct:packageDependency>
     <sct:editionDependency></sct:editionDependency>
     <sct:derivativeDependency></sct:derivativeDependency>
</sct:packageDependency>
```

These are SNOMED CT specific extensions to dictate any package dependency for a given release package. DDependencies an be on **editions** or other **derivatives**.

- **sct:editionDependency** states any necessary edition dependency and version using the SNOMED CT URI standard, e.g. `http://snomed.info/sct/900000000000207008/version/20220731`. It can have an empty value when there is no dependency as with the International Edition. Where there are multiple edition dependencies, only put the **next** dependency. Downloading packages would complete when there are no further dependencies.
- **sct:derivativeDependency** states any necessary derivative dependency, as they are often published outside of SNOMED CT editions. Similarly, this should also follow the SNOMED CT URI standard for module and version

## Authentication
The standard does not mandate any authentication and this is left to the implementer of the Atom feed provider to implement whatever is needed depending on any terminology product license requirements.

## Use Cases

Syndication of terminologies has a number of use cases. A few examples are:

Automatic distribution of content products by their owners:

- International content products
- National content products
- Regional content products

Automatic import of selected products and dependencies as updates become available:

- Automatic update of existing terminology server instances
  - Browser server containing both published content and daily builds

- Automatic provision of new terminology server instances
  - Autoscaling
