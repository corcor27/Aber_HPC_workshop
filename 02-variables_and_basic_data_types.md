---
title: Foundation & The FAIR Principles
teaching: 75
exercises: 0
---

::::::::::::::::::::::::::::::::::::::: objectives
- Articulate the Value of Active Data Stewardship: Explain how structured Data Management Plans mitigate research risks (data loss, non-reproducibility) and save time throughout the research lifecycle.
- Differentiate Project vs. Data Lifecycles: Recognize that while research grants have finite end dates, research datasets require long-term preservation and curation strategies.
- Deconstruct the FAIR Principles: Identify the core components of Findability, Accessibility, Interoperability, and Reusability within practical academic workflows.
- Identify Workflow Gaps: Evaluate their own research data practices against the FAIR principles to pinpoint areas needing immediate improvement.
 
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Findability: "Why is saving data on a lab server or personal Google Drive not enough to make it truly 'Findable' by the wider research community?"
- Accessibility: "Does making data FAIR mean it must be completely public and open to everyone? How do we handle sensitive clinical, commercial, or ecological data?"
- Interoperability: "What proprietary file formats do you rely on daily, and what open standards could you export to for long-term preservation?"
- Reusability: "If someone downloaded your raw dataset today without talking to you, what documentation would they need to replicate your analysis?"

::::::::::::::::::::::::::::::::::::::::::::::::::

## Module 1.1: The "Data Disaster" Hook

### The Reality Check
    
A Data Management Plan is not administrative paperwork—it is your insurance policy against lost time, corrupted files, and uninterpretable results.

Consider a common academic scenario:

- A researcher finishes a project or completes their degree and moves to another institution.
- Two years later, a journal editor or peer reviewer asks for raw data during a replication check or meta-analysis.
- The remaining research team finds an unindexed cloud folder containing unlabeled columns, proprietary file formats, and no codebook.

The result: The data is effectively dead, and months of labor are rendered unverified. Retrofitting documentation at the end of a project takes 3–5x more effort than logging metadata continuously.

## Module 1.2: Research Data Life Cycle vs. Project Life Cycle

Funding cycles usually last 1–3 years, but research data can have a lifespan of decades if properly curated.

!["Are we dealing with supervised or unsupervised
learning?"](fig/pillar_12.png){alt="Flow Diagram for determining supvervised vs unsupervised"}.

- Projects end; data persists. Major funding bodies (e.g., UKRI, NIH, Horizon Europe, Wellcome) treat research outputs as public goods.
- A living DMP bridges the gap between active research work and long-term data preservation.

## Module 1.3: Operationalizing the FAIR Data Principles

The FAIR Data Principles provide the framework for sustainable data stewardship.

1. Findable
- Requirement: Humans and automated tools can discover the dataset.
- Implementation:
  - Assign a Persistent Identifier (PID) such as a Digital Object Identifier (DOI) via repositories (e.g., Zenodo, Figshare, institutional repositories).
  - Link your personal ORCID iD to the dataset metadata.
  - Tag datasets with standardized discipline keywords.

2. Accessible
- Requirement: Clear conditions and protocols for retrieving the data.
- Implementation:
- Use open, standard communication protocols (e.g., HTTP, FTP).
- Remember: "As open as possible, as closed as necessary."
- Sensitive human subject data, protected species locations, or proprietary IP can remain FAIR by providing public metadata while placing raw files behind controlled access protocols (e.g., Data Access Committees).


3. Interoperable
- Requirement: Data can integrate with other datasets, workflows, and applications.
- Implementation:
  - Store data in non-proprietary formats (e.g., .csv alongside .xlsx, .flac alongside .mp3).
  - Utilize standard domain ontologies, controlled vocabularies, and ISO standards (e.g., ISO 8601 for dates: YYYY-MM-DD).

4. Reusable
- Requirement: Data contains rich context so others can build upon it safely.
- Implementation:
  - Apply an explicit machine-readable usage license (e.g., CC-BY 4.0 for data, MIT/GPL for software).
  - Attach comprehensive provenance documentation: experimental parameters, device calibration details, preprocessing scripts, and software version numbers.

## Module 1.4: Interactive Self-Assessment
### Quick Reflection Task

Think about a dataset you produced or analyzed over the past 12 months. Which element of FAIR represents the biggest gap in your current workflow?

[ ] Findable: My data lives on local drives or unindexed personal cloud storage.
[ ] Accessible: There is no documented pathway for external researchers to request access.
[ ] Interoperable: My files rely on specialized, proprietary software formats.
[ ] Reusable: I haven't attached a clear license or detailed README file.

### Common Bottlenecks & Solutions

- Challenge: "We rely on vendor-specific binary formats from lab equipment."
  - Fix: Retain raw binary files for active analysis, but export a open-standard copy (e.g., .csv, .tiff, .HDF5) for the archived deposit.
- Challenge: "I don't know which open license applies to my discipline."
  - Fix: We cover license selector tools and institutional guidance in Session 2.

:::::::::::::::::::::::::::::::::::::::: keypoints

- DMPs are Living Tools, Not Paperwork: A Data Management Plan is a dynamic roadmap that evolves with your project, serving as an insurance policy against data corruption and misinterpretation.
- Proactive Curation Saves Time: Documenting metadata, variable names, and folder structures during data collection takes a fraction of the effort required to reconstruct them at the end of a project.
- As Open as Possible, As Closed as Necessary: Accessibility under FAIR does not violate ethical or GDPR boundaries. Restricted access protocols can protect participant privacy while keeping dataset metadata fully discoverable.
- Persistent Identifiers Matter: Using DOIs for datasets and linking them to your ORCID iD ensures proper citation, academic credit, and long-term traceability.
- Prioritize Non-Proprietary Formats: Storing data in open formats (e.g., .csv, .tiff, .flac) ensures your files remain readable decades after proprietary software licenses expire.
::::::::::::::::::::::::::::::::::::::::::::::::::


