# Graph Explorer
A web application for exploring a knowledge graph.

The purpose of this webapp is (i) to provide an early demonstration of the widgets created in D3.1 and (ii) provide a useful tool for exploring a knowledge graph.

For the early demonstration, we use a description of experimental datasets for physical metallurgy produced in the Norwegian [SFI PhysMet](https://www.ntnu.edu/physmet) project.

The figure below shows how each experimental dataset in the
[knowledge graph](examples/kb.ttl) is defined and how it relates to other
resources.

```mermaid
---
config:
  theme: base
  themeVariables:
    background: '#ffffff'
    edgeLabelBackground: '#ffffff'
    lineColor: '#808080'
---
flowchart LR
  classDef default fill:#f8cecc,stroke:#b85450,color:#111827;
  classDef blueBox fill:#dae8fc,stroke:#6c8ebf,color:#111827;
  classDef lightBlueBox fill:#dae8fc,stroke:#6c8ebf,color:#111827,stroke-dasharray: 5 5;
  classDef grayBox fill:#ccc,stroke:#333,color:#111827;

  D(dataset):::blueBox -- contactPoint --> CP("project leader")
  D -- wasGeneratedBy --> PR("project")
  S(sample):::blueBox -- contactPoint --> CP
  S -- wasGeneratedBy --> PR
  %%S -. hasComposition .-> C("composition"):::lightBlueBox
  S -- creator --> ST("researcher")
  D -- rightsHolder --> RH("organisation")
  D -- license --> LD("license document")
  D -- creator --> ST
  D -- processedFrom --> S
  D -- distribution --> DI(distribution):::grayBox
  M(measurement):::blueBox -- hasInput --> S
  M -- hasOutput --> D
  M -- performedWith --> EQ("instrument")
  M -- hasOperator --> ST
  M -- hasTechnique --> TC("characterisation technique")
```

**Figure** The interrelations between the `sample`, `dataset` and `measurement` (blue boxes) and their relation to shared resources (red boxes).
Accessibility is provided via the dataset `distribution` (gray box), which is a blank node exposing a dcat:downloadURL or dcat:accessURL.
Literals relations are not shown for brevity.
